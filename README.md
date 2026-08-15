# 안녕하세요, Backend 개발자 박병준입니다.

Java와 Spring Boot를 기반으로  
**서비스 데이터와 실행 상태를 안정적으로 연결하는 Backend 개발**에 관심을 가지고 있습니다.

프로젝트를 통해 REST API 구현을 넘어  
다중 사용자 데이터 격리, 실시간 상태 관리, Graph DB 동기화,
AI Planning Server 연동과 같은 Backend 문제를 설계하고 해결했습니다.

특히 최근에는 **Digital Twin 기반 자율 창고 운영 시스템 LARO**에서  
Warehouse · Robot · Graph 영역과 AI 실행 환경 연동을 담당했습니다.

---

## Tech Stack

### Backend

`Java` `Spring Boot` `Spring Data JPA` `Spring Security`  
`REST API` `WebSocket / STOMP`

### Database

`PostgreSQL` `MySQL` `Redis` `Neo4j`

### Cloud / Infra

`AWS` `Docker` `ECR` `ECS` `EKS` `CloudWatch`

### Tools

`Git` `GitHub` `Postman`

---

## Featured Projects

### LARO — Digital Twin 기반 자율 창고 운영 및 다중 로봇 작업 최적화

창고·재고·로봇 상태를 Digital Twin으로 관리하고,
AI Planning과 최적화 Solver를 통해 다중 로봇의 작업 배정·이동 계획·재계획을 수행하는 시스템입니다.

**Backend 담당**

- Warehouse / Zone / Node / Edge API 설계 및 구현
- USER / GUEST별 Personal Warehouse 실행 환경 격리
- PostgreSQL → Neo4j `AFTER_COMMIT` Graph Sync
- Warehouse Resource 소유권 검증 및 접근 제어
- AI Plan과 Backend Simulation 실행 데이터 연동

**주요 기술**

`Spring Boot` `PostgreSQL` `Redis` `Neo4j`  
`WebSocket` `FastAPI Integration` `Docker` `AWS`

🔗 **Portfolio**  
https://github.com/pbjun2000/digital-twin-warehouse-backend

🔗 **Team Project**  
https://github.com/kt-aivle-big-project

---

### AI Book Service

React 기반 도서관리 서비스를 Spring Boot Backend API로 전환한 팀 프로젝트입니다.

- Entity 직접 반환 대신 DTO 응답 구조 적용
- `GlobalExceptionHandler` 기반 공통 예외 처리
- Spring Data JPA 기반 CRUD / 검색 API 구현
- Postman 기반 성공·실패 API 테스트

🔗 https://github.com/pbjun2000/aivle-ai-book-service-review

---

### BookService AWS CI/CD & Monitoring

React + Spring Boot 서비스를 AWS 환경에 배포하고
CI/CD 및 모니터링 흐름을 구성한 프로젝트입니다.

- AWS CodeBuild · ECR 기반 Build / Image 관리
- EKS 기반 Container 배포
- Kubernetes Deployment / Service 구성
- CloudWatch 기반 서비스 상태 및 인프라 지표 확인

🔗 https://github.com/pbjun2000/aivle-book-service-aws-review

---

## What I Focus On

Backend 개발에서 단순한 기능 구현보다

- **서비스 간 책임을 어떻게 분리할 것인지**
- **여러 저장소의 데이터 일관성을 어떻게 유지할 것인지**
- **사용자별 실행 상태와 Resource를 어떻게 격리할 것인지**
- **외부 AI 서비스의 결과를 실제 서비스 데이터와 어떻게 연결할 것인지**

를 고민하며 구현하고 있습니다.

---

## Contact

**Email**  
qudwns526@naver.com

**Tech Blog**  
https://qudwns526.tistory.com
