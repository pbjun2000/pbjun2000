# 안녕하세요, AI 서비스와 Backend를 개발하는 박병준입니다.

데이터의 흐름을 따라 문제의 원인을 찾고,  
**Python 기반 LLM·RAG·Agent와 Java/Spring Boot Backend를 함께 경험했습니다.**

LangGraph 기반 Agent Workflow, Chroma 기반 RAG Pipeline,  
BERT Fine-tuning·LoRA/PEFT 등 AI 모델 활용 과정을 실습했습니다.

LARO 프로젝트에서는  
**AI Planning이 실제 창고 구조를 참조할 수 있도록 Warehouse Graph API와 Node·Edge 데이터를 제공**하고,  
Backend 데이터가 안정적으로 관리될 수 있도록 PostgreSQL–Neo4j 동기화 구조를 구현했습니다.

기능이 동작하는 것에서 끝내지 않고,  
데이터가 생성·저장·전달되는 흐름과 기술 선택의 이유, 실패 상황까지 확인하며 개발합니다.

---

## 🛠 Tech Stack

### AI / Data

`Python` `LangChain` `LangGraph` `RAG` `Chroma`  
`Hugging Face` `BERT` `LoRA/PEFT`  
`Pandas` `scikit-learn` `Keras`

### Backend

`Java` `Spring Boot` `Spring Data JPA` `REST API`

### Database / Data Store

`PostgreSQL` `Neo4j` `Redis` `H2` `SQLite`

### Cloud / Infra

`Docker` `AWS` `CodeBuild` `ECR` `EKS` `Kubernetes` `CloudWatch`

---

## 📌 Featured Projects

### 🤖 LARO — LLM Autonomous Robot Orchestration

**Digital Twin 기반 자율 창고 운영 및 다중 로봇 작업 최적화 플랫폼**

`2026.07 ~ 2026.08` · `6인 팀` · `Team Leader / Backend Developer`

KT AIVLE School 9기 Big Project에서  
**Backend 3명 · AI 2명 · Frontend 1명으로 구성된 6인 팀**이 개발한 B2B형 MVP 프로젝트입니다.

운영자의 자연어 요청을 Rule / Agent 경로로 분기하고,  
실행 가능한 Mission으로 정식화한 뒤 최적화·경로계획으로 연결해  
Digital Twin 환경에서 다중 로봇 작업을 수행하는 자율 창고 시뮬레이션 플랫폼입니다.

<p align="center">
  <img src="./assets/simulation-live-view-readme.png" width="100%" alt="LARO Warehouse Live View">
</p>

#### 담당 및 구현

- Warehouse / Zone / Node / Edge REST API 및 관련 도메인 구현
- USER / GUEST별 Personal Warehouse 기반 Simulation 실행 환경 분리
- Simulation 실행 전 Warehouse 소유권 검증을 통한 사용자별 접근 분리
- PostgreSQL Transaction 완료 후 Neo4j Graph를 동기화하는 `AFTER_COMMIT` 기반 Graph Sync 구현
- AI Planning이 실제 창고 구조를 참조할 수 있도록 Warehouse Graph API 및 Node·Edge 데이터 제공
- 개인 창고 생성 이후 Scenario 참조 불일치 문제 추적 및 수정
- 6인 팀 조장으로 Backend·AI 간 데이터 구조와 개발 진행 상황 조율

> AI Agent, 최적화 알고리즘, WebSocket 실시간 전송 기능은  
> 팀 내 다른 담당자가 구현했으며, 저는 Backend와 AI Planning용 데이터 제공 영역을 중심으로 담당했습니다.

---

#### 주요 기술 결정

##### 1. Simulation 상태 격리

초기에는 여러 사용자가 하나의 Shared Warehouse를 대상으로  
Simulation을 실행하는 구조였습니다.

하지만 여러 사용자가 동시에 실행하면  
Robot·재고·Scenario 등 실행 중 변경되는 상태가 서로 영향을 줄 수 있었습니다.

단순히 조회 조건에 `userId`를 추가하는 방식만으로는  
실행 중 변경되는 상태 자체의 간섭을 막기 어렵다고 판단했습니다.

따라서 Shared Warehouse는 Template으로 유지하고,  
USER / GUEST별 Personal Warehouse를 Deep Clone하여  
각 사용자가 독립된 환경에서 Simulation을 실행하도록 구성했습니다.

2개월 MVP에서는 명확한 상태 격리를 우선했고,  
서비스 규모가 커질 경우 Runtime State 분리 또는 Copy-on-Write 방식으로  
복제 비용을 줄이는 방향도 고려했습니다.

---

##### 2. PostgreSQL / Neo4j 역할 분리

Node와 Edge 관계를 PostgreSQL에 저장한 뒤  
필요할 때 NetworkX로 Graph를 생성하는 방식도 검토했습니다.

하지만 프로젝트에서는 Graph를 일회성 알고리즘 계산에만 사용하는 것이 아니라,  
Warehouse의 Node–Edge 관계를 지속적으로 관리하고  
Backend와 AI Planning에서 반복적으로 조회할 필요가 있었습니다.

이에 관계 데이터를 Graph 구조로 저장·조회할 수 있는 Neo4j를 사용했습니다.

두 저장소를 함께 사용하면서 발생할 수 있는 데이터 일관성 문제를 줄이기 위해

- **PostgreSQL → Source of Truth**
- **Neo4j → Graph Projection**

으로 역할을 분리했습니다.

PostgreSQL Transaction이 정상적으로 완료된 이후에만  
Neo4j Graph를 갱신하도록 `AFTER_COMMIT` 기반 동기화 구조를 적용했습니다.

---

#### Troubleshooting

##### Personal Warehouse 생성 이후 Scenario 참조 불일치

Personal Warehouse 생성 과정에서 Scenario 자체는 정상적으로 복제됐지만,  
SimulationRun이 복제된 Scenario가 아닌 기존 Template Scenario를 참조하는 문제가 발생했습니다.

다음 흐름을 처음부터 다시 추적했습니다.

```text
Personal Warehouse 생성
        ↓
Scenario 복제
        ↓
SimulationRun 생성
        ↓
Scenario 참조 확인
```

각 단계에서 전달되는 객체와 ID를 확인한 결과,  
SimulationRun 생성 과정에 기존 Scenario ID가 남아 있는 지점을 발견했습니다.

복제된 Personal Scenario를 다시 조회해 연결하도록 수정하여  
사용자별 Simulation 데이터의 참조 일관성을 확보했습니다.

---

#### 프로젝트 결과

- KT AIVLE School 9기 Big Project **우수상**
- 동일 Optimization Solver 조건의 팀 실험에서  
  Agent 방식이 Rule 방식 대비 작업 완료시간 **최대 64% 단축**

> 성능 결과는 팀 프로젝트 전체 실험 결과입니다.

---

#### Tech Stack

`Java` `Spring Boot` `Spring Data JPA`  
`PostgreSQL` `Neo4j` `Redis`  
`FastAPI` `Docker`

🔗 **Backend Portfolio**  
[github.com/pbjun2000/digital-twin-warehouse-backend](https://github.com/pbjun2000/digital-twin-warehouse-backend)

---

### 📚 AI Books — AI 표지 생성 기반 창작·도서 관리 플랫폼

**사용자가 글과 도서 정보를 등록·관리하고, AI 이미지 생성으로 자신만의 도서 표지를 제작할 수 있는 웹 플랫폼**

`2026.05 ~ 2026.06` · `Frontend / Backend Integration / Cloud Project`

KT AIVLE School 미니프로젝트에서 진행한 팀 프로젝트입니다.

초기에는 React와 `json-server`를 이용해 도서관리 서비스를 구현했고,  
이후 Spring Boot REST API 기반 Backend와 연동했습니다.

다음 단계에서는 동일 서비스를 Docker로 컨테이너화하고  
AWS CodeBuild → ECR → EKS 환경에 배포한 뒤  
CloudWatch로 운영 상태를 확인했습니다.

---

#### 서비스 주요 기능

- 도서 등록·조회·수정·삭제
- OpenAI API 기반 AI 도서 표지 이미지 생성
- 장르별 도서 필터링
- 좋아요·조회수 기반 정렬
- 도서 상세 정보 및 작성 콘텐츠 관리
- 로그인 사용자 기준 수정·삭제 권한 처리

---

#### Frontend · Service Integration

4차 미니프로젝트에서는 React 기반 도서관리 화면에서  
**스타일링·QA와 AI 표지 생성 옵션 UI**를 담당했습니다.

AI 표지 생성 과정에서 사용자가 다음 옵션을 입력할 수 있도록 구성했습니다.

- API Key 입력
- 생성 모델 선택
- 이미지 크기 선택
- 필수값 검증
- AI 표지 생성 요청

이후 Spring Boot Backend 연동 프로젝트에서는  
기존 React의 요청 URL·Method·응답 구조와 Backend API를 비교하며  
Frontend–Backend 연결 흐름을 확인했습니다.

---

#### Backend 담당 경험

- React 요청과 Spring Boot REST API 간 연동 흐름 점검
- `WebConfig` 기반 CORS 설정
- `GlobalExceptionHandler` 기반 공통 예외 처리
- 존재하지 않는 도서 요청을 별도 Resource 예외로 구분
- 실패 상황에 따라 `400 / 404 / 500` 응답 구조 정리
- `BookFavoriteResponseDto` 구현 및 DTO 기반 응답 구조 적용
- Postman을 활용한 정상·예외 요청 검증
- H2 Console에서 저장 데이터와 API 응답 결과 비교

---

#### Troubleshooting

##### 1. 존재하지 않는 도서 요청이 500으로 처리되는 문제

존재하지 않는 도서 ID를 조회하거나 삭제했을 때  
클라이언트 요청 오류임에도 `500 Internal Server Error`가 반환되는 문제가 있었습니다.

`BookNotFoundException`을 별도로 정의하고  
`GlobalExceptionHandler`에서 처리하도록 변경하여

```text
500 Internal Server Error
        ↓
404 Not Found
```

로 응답 구조를 정리했습니다.

이를 통해 내부 Stack Trace가 클라이언트에 노출되지 않도록 하고  
실패 원인에 맞는 상태코드를 반환하도록 개선했습니다.

---

##### 2. Entity 직접 반환 구조 개선

초기에는 Entity 객체가 API 응답으로 직접 반환되는 구조였습니다.

이 경우

- 프론트엔드에 불필요한 필드가 전달될 수 있고
- Entity 구조 변경이 API 응답 구조에 직접 영향을 줄 수 있으며
- 화면별 필요한 데이터가 명확하지 않은 문제가 있었습니다.

기능별 DTO를 분리하고  
화면에 필요한 값만 반환하도록 응답 구조를 정리했습니다.

특히 좋아요 기능에서는

```text
bookId
likeCount
```

등 화면 갱신에 필요한 데이터만 반환하도록 구성했습니다.

---

### ☁️ AI Books — AWS CI/CD · EKS Deployment · Monitoring

**AI Books 서비스를 Docker·AWS 기반 배포 환경으로 확장한 프로젝트**

`2026.06` · `Cloud / Deployment Project`

앞서 개발한 React + Spring Boot 기반 AI Books 서비스를 대상으로  
GitHub → CodeBuild → ECR → EKS → CloudWatch로 이어지는  
빌드·배포·운영 흐름을 구성했습니다.

```text
GitHub
   ↓
AWS CodeBuild
   ↓
Docker Image Build
   ↓
Amazon ECR
   ↓
Amazon EKS
   ↓
CloudWatch Monitoring
```

---

#### 담당 경험

- Backend 배포 단계 구성 및 명령 흐름 확인
- `deployment.yaml` / `service.yaml` 작성 및 Kubernetes Manifest 검증 참여
- ECR 로그인 → Docker Build / Push → EKS 배포 흐름 확인
- CodeBuild의 ECR / EKS 접근 권한 문제 확인
- CloudWatch Dashboard 구성
- CodeBuild·EKS·ELB·EC2·Logs 기반 모니터링 지표 정리
- 배포 흐름과 트러블슈팅 내용을 README 및 발표 자료로 문서화

---

#### CloudWatch Monitoring

배포 이후 서비스 상태를 한 화면에서 확인할 수 있도록  
CloudWatch Dashboard에 다음 지표를 구성했습니다.

| 구분 | 확인 지표 |
| --- | --- |
| CodeBuild | Build Status, Build Duration |
| EKS | Running Pods, Node / Backend Memory |
| ELB | Request Count, Latency, Target Health |
| Network | EC2 Network In / Out |
| Logs | Log Count, Error Count, Build Logs |

단순히 지표를 나열하기보다  
문제가 발생했을 때 어느 구간에서 이상이 발생했는지 좁힐 수 있도록 구성했습니다.

---

#### Troubleshooting

##### 1. buildspec 경로 불일치

**문제**

```text
cd BackEnd-main
```

명령이 실행 환경에서 실패했습니다.

**원인**

GitHub Repository의 실제 Source 구조와  
`buildspec.yml`에 작성된 상대 경로가 일치하지 않았습니다.

**해결**

실제 Repository 구조를 다시 확인한 뒤  
루트 기준으로 빌드가 수행되도록 경로를 수정했습니다.

---

##### 2. Artifact 경로 오류

Gradle Build 자체는 성공했지만

```text
no matching artifact paths found
```

오류가 발생했습니다.

실제 JAR 생성 위치와 CodeBuild Artifact 설정을 비교한 결과  
경로가 이전 프로젝트 구조를 기준으로 작성돼 있었습니다.

Artifact 경로를

```text
build/libs/*.jar
```

로 수정해 실제 생성 파일을 인식하도록 변경했습니다.

---

##### 3. ECR 접근 권한 오류

CodeBuild에서 ECR 로그인 과정 중

```text
ecr:GetAuthorizationToken
```

권한 부족 오류가 발생했습니다.

CodeBuild Service Role의 IAM 권한을 확인하고  
필요한 ECR 접근 권한을 추가하여 Docker Image Push가 가능하도록 수정했습니다.

---

#### Tech Stack

`React` `Java` `Spring Boot` `Spring Data JPA`  
`H2` `Postman`  
`Docker` `AWS` `CodeBuild` `ECR` `EKS`  
`Kubernetes` `CloudWatch`

🔗 **Service Development · API Integration**  
[github.com/pbjun2000/aivle-ai-book-service-review](https://github.com/pbjun2000/aivle-ai-book-service-review)

🔗 **AWS Deployment · EKS · Monitoring**  
[github.com/pbjun2000/aivle-book-service-aws-review](https://github.com/pbjun2000/aivle-book-service-aws-review)

---

## 📫 Contact

**Email**  
[qudwns526@naver.com](mailto:qudwns526@naver.com)

**GitHub**  
[github.com/pbjun2000](https://github.com/pbjun2000)

**Tech Blog**  
[qudwns526.tistory.com](https://qudwns526.tistory.com)
