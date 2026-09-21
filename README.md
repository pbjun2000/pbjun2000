# 안녕하세요, AI 서비스와 Backend를 개발하는 박병준입니다.

데이터의 흐름을 따라 문제의 원인을 찾고,  
**Python 기반 LLM·RAG·Agent 서비스와 Java/Spring Boot Backend를 함께 경험했습니다.**

LangGraph 기반 Agent Workflow와 Chroma 기반 RAG Pipeline을 실습했고,  
LARO 프로젝트에서는 Backend 데이터와 AI Planning이 연결되는 구조를 구현했습니다.

기능 구현에 그치지 않고,  
데이터가 생성·저장·전달되는 흐름과 기술 선택의 이유, 실패 상황까지 확인하며 개발합니다.

---

## 🛠 Tech Stack

### AI / Data

`Python` `LangChain` `LangGraph` `RAG` `Chroma` `Pandas` `scikit-learn` `Keras`

### Backend

`Java` `Spring Boot` `Spring Data JPA` `REST API`

### Database / Data Store

`PostgreSQL` `Neo4j` `Redis`

### Cloud / Infra

`Docker` `AWS` `EKS` `Kubernetes` `CloudWatch`

---

## 📌 Featured Projects

### 🤖 LARO — LLM Autonomous Robot Orchestration

**Digital Twin 기반 자율 창고 운영 및 다중 로봇 작업 최적화 시스템**

`2026.07 ~ 2026.08` · `Backend Developer`

KT AIVLE School 9기에서 2개월간  
**Backend 3명 · AI 2명 · Frontend 1명으로 구성된 6인 팀**이 개발한 B2B형 MVP 프로젝트입니다.

운영자의 자연어 명령을 AI가 작업 계획으로 변환하고,
Digital Twin 환경에서 다중 로봇의 작업 배정·경로 계획·재계획을 수행하는
자율 창고 시뮬레이션 플랫폼입니다.

<p align="center">
  <img src="./assets/simulation-live-view-readme.png" width="100%" alt="LARO Warehouse Live View">
</p>

#### 담당 및 구현

- Warehouse / Zone / Node / Edge REST API 및 관련 도메인 구현
- USER / GUEST별 Personal Warehouse 기반 Simulation 실행 환경 분리
- Simulation 실행 전 Warehouse 소유권 검증을 통한 사용자 실행 환경 접근 분리
- PostgreSQL Transaction 완료 후 Neo4j Graph를 동기화하는 `AFTER_COMMIT` 기반 Graph Sync 구현
- AI Planning에서 사용할 Warehouse Graph API 및 Node·Edge 데이터 제공

#### 주요 기술 결정

**Simulation 상태 격리**

초기에는 여러 사용자가 하나의 Shared Warehouse를 대상으로
Simulation을 실행하는 구조였습니다.

여러 사용자가 동시에 실행할 경우 Robot·재고·Scenario 등
실행 중 변경되는 상태가 서로 섞이면서,
Simulation Run이 정상적으로 진행되지 않는 상태 충돌이 발생했습니다.

단순히 사용자별 조회 조건을 추가하는 것으로는
실행 상태 자체의 간섭을 막기 어렵다고 판단했습니다.

따라서 Shared Warehouse는 Template으로 유지하고,
USER / GUEST별 Personal Warehouse를 Deep Clone해
각 사용자가 독립된 Warehouse 환경에서 Simulation을 실행하도록 변경했습니다.

2개월 MVP에서는 명확한 실행 상태 격리를 우선했으며,
규모가 커질 경우 Runtime State 분리 또는 Copy-on-write 방식으로
복제 비용을 줄이는 방향을 고려했습니다.

**PostgreSQL / Neo4j 역할 분리**

Node와 Edge를 PostgreSQL에 저장하고
필요할 때 NetworkX로 Graph를 구성하는 방식도 검토했습니다.

하지만 프로젝트에서는 Graph를 일회성 알고리즘 계산에만 사용하는 것이 아니라,
Warehouse의 Node–Edge 관계를 지속적으로 관리하고
Backend와 AI Planning에서 반복적으로 조회할 필요가 있었습니다.

따라서 관계를 Graph 구조로 저장하고 조회할 수 있는 Neo4j를 사용했습니다.

데이터를 두 DB에서 함께 관리하면서 발생할 수 있는 일관성 문제를 줄이기 위해

- **PostgreSQL → Source of Truth**
- **Neo4j → Graph Projection**

으로 역할을 분리했습니다.

#### Troubleshooting

**Personal Warehouse 생성 이후 Scenario 참조 불일치 해결**

Personal Warehouse 생성 → Scenario 복제 → SimulationRun 생성 흐름을 추적해
SimulationRun이 기존 Template Scenario ID를 참조하고 있던 문제를 확인했습니다.

복제된 Personal Scenario를 다시 매칭하도록 수정해
사용자별 Simulation 데이터의 참조 일관성을 확보했습니다.

#### 프로젝트 결과

- 동일 Optimization Solver 조건의 팀 실험에서
  Agent 방식이 Rule 방식 대비 작업 완료시간 **최대 64% 단축**

#### Tech Stack

`Java` `Spring Boot` `Spring Data JPA`  
`PostgreSQL` `Neo4j` `Redis` `Docker`

🔗 **Backend Portfolio**  
[github.com/pbjun2000/digital-twin-warehouse-backend](https://github.com/pbjun2000/digital-twin-warehouse-backend)

🔗 **Team Project**  
[github.com/kt-aivle-big-project](https://github.com/kt-aivle-big-project)

---

### 📚 Book Service — Spring Boot REST API / AWS Deployment

`2026.06` · `Backend / Cloud Project`

React·json-server 기반 도서 관리 서비스를
Spring Boot REST API 구조로 전환하고,
Docker·AWS 환경에 배포한 팀 프로젝트입니다.

#### Backend

- Spring Data JPA 기반 도서 CRUD·검색 REST API 구현
- Entity 직접 반환 대신 DTO 기반 응답 구조 적용
- `GlobalExceptionHandler` 기반 공통 예외 처리
- 존재하지 않는 도서 요청을 Resource 예외로 분리해 `404` 응답 처리
- Postman을 활용한 정상·예외 API 요청 검증

#### AWS Deployment

- Docker 이미지 빌드 후 AWS ECR·EKS 환경에 애플리케이션 배포
- `deployment.yaml` / `service.yaml` 작성 및 Kubernetes Manifest 검증
- CodeBuild·EKS·ELB 지표를 CloudWatch Dashboard로 구성

#### Troubleshooting

- buildspec의 실제 Source 경로와 `cd` 경로 불일치 수정
- Artifact 수집 경로를 실제 JAR 생성 위치인 `build/libs/*.jar`로 수정
- CodeBuild의 ECR 접근 권한 오류를 IAM 권한 설정으로 해결

#### Tech Stack

`Java` `Spring Boot` `Spring Data JPA` `H2`  
`Docker` `AWS` `CodeBuild` `ECR` `EKS` `Kubernetes` `CloudWatch`

🔗 **Backend Development**  
[github.com/pbjun2000/aivle-ai-book-service-review](https://github.com/pbjun2000/aivle-ai-book-service-review)

🔗 **AWS Deployment & Monitoring**  
[github.com/pbjun2000/aivle-book-service-aws-review](https://github.com/pbjun2000/aivle-book-service-aws-review)

---

## 📫 Contact

**Email**  
[qudwns526@naver.com](mailto:qudwns526@naver.com)

**Tech Blog**  
[qudwns526.tistory.com](https://qudwns526.tistory.com)
