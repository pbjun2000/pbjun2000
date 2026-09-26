# 안녕하세요, AI 서비스와 Backend를 개발하는 박병준입니다.

데이터의 흐름을 따라 문제의 원인을 찾고,  
**Python 기반 LLM·RAG·Agent와 Java/Spring Boot Backend를 함께 경험했습니다.**

LangGraph 기반 Agent Workflow, Chroma 기반 RAG Pipeline,  
BERT Fine-tuning·LoRA/PEFT 등 AI 모델 활용 과정을 실습했습니다.

LARO 프로젝트에서는  
**AI Planning이 실제 창고 구조를 참조할 수 있도록 Warehouse Graph API와 Node·Edge 데이터를 제공**하고,  
PostgreSQL–Neo4j 데이터 동기화와 사용자별 시뮬레이션 환경 분리를 구현했습니다.

기능이 동작하는 것에서 끝내지 않고,  
데이터가 생성·저장·전달되는 흐름과 문제 발생 원인을 함께 확인하며 개발합니다.

---

## 🛠 Tech Stack

### AI / Data
`Python` `LangChain` `LangGraph` `RAG` `Chroma`  
`Hugging Face` `BERT` `LoRA/PEFT`  
`Pandas` `scikit-learn` `Keras`

### Backend
`Java` `Spring Boot` `Spring Data JPA` `REST API`

### Database
`PostgreSQL` `Neo4j` `Redis` `H2` `SQLite`

### Cloud / Infra
`Docker` `AWS` `CodeBuild` `ECR` `EKS` `Kubernetes` `CloudWatch`

---

## 📌 Featured Projects

### 🤖 LARO — LLM Autonomous Robot Orchestration

**Digital Twin 기반 자율 창고 운영 및 다중 로봇 작업 최적화 플랫폼**

`2026.07 ~ 2026.08` · `6인 팀` · `Team Leader / Backend Developer`

운영자의 자연어 요청을 AI Planning과 최적화·경로계획으로 연결해  
Digital Twin 환경에서 다중 로봇 작업을 수행하는 B2B형 자율 창고 시뮬레이션 플랫폼입니다.

<p align="center">
  <img src="./assets/simulation-live-view-readme.png" width="100%" alt="LARO Warehouse Live View">
</p>

**담당 경험**
- Warehouse / Zone / Node / Edge REST API 및 도메인 구현
- USER / GUEST별 Personal Warehouse 기반 시뮬레이션 실행 환경 분리
- PostgreSQL `Source of Truth` → Neo4j `Graph Projection` 동기화 구현
- AI Planning용 Warehouse Graph API 및 Node·Edge 데이터 제공
- 개인 창고 생성 후 Scenario 참조 불일치 문제를 데이터 생성 흐름부터 추적해 해결
- 6인 팀 조장으로 개발 진행 상황과 Backend·AI 데이터 구조 협의

**Tech Stack**  
`Java` `Spring Boot` `Spring Data JPA` `PostgreSQL` `Neo4j` `Redis` `Docker`

**Result**
- KT AIVLE School 9기 Big Project **우수상**
- 동일 Optimization Solver 조건의 팀 실험에서 Agent 방식 작업 완료시간 **최대 64% 단축**

🔗 [Backend Portfolio](https://github.com/pbjun2000/digital-twin-warehouse-backend)

---

### 📚 AI Books — AI 표지 생성 기반 창작·도서 관리 플랫폼

`2026.05 ~ 2026.06` · `Frontend / Backend Integration / Cloud`

사용자가 글과 도서 정보를 등록·관리하고,  
**OpenAI 기반 AI 표지를 생성해 자신의 작품을 완성할 수 있는 웹 플랫폼**입니다.

**담당 경험**
- React/Vite 기반 화면 스타일링·QA 및 AI 표지 생성 옵션 UI 구현
- React 요청과 Spring Boot REST API 간 연동 흐름 점검
- CORS 설정, `GlobalExceptionHandler` 기반 공통 예외 처리
- DTO 분리 및 Postman·H2 기반 요청/응답·저장 결과 검증
- Docker → CodeBuild → ECR → EKS 배포 흐름 구성 참여
- CloudWatch Dashboard 구성 및 CodeBuild·EKS·ELB·로그 상태 모니터링
- buildspec 경로, JAR Artifact 경로, ECR IAM 권한 오류 해결

**Tech Stack**  
`React` `Java` `Spring Boot` `Spring Data JPA` `H2`  
`Docker` `AWS` `CodeBuild` `ECR` `EKS` `Kubernetes` `CloudWatch`

🔗 [Service Development · API Integration](https://github.com/pbjun2000/aivle-ai-book-service-review)

🔗 [AWS Deployment · Monitoring](https://github.com/pbjun2000/aivle-book-service-aws-review)

---

## 📫 Contact

**Email**  
[qudwns526@naver.com](mailto:qudwns526@naver.com)

**Tech Blog**  
[qudwns526.tistory.com](https://qudwns526.tistory.com)
