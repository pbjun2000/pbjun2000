# 안녕하세요, 백엔드 개발자 박병준입니다.

Java와 Spring Boot를 중심으로 백엔드 개발을 준비하고 있습니다.

최근 **Digital Twin 기반 자율 창고 프로젝트 LARO**에서
창고·로봇·이동 그래프 도메인의 API와 데이터 모델을 구현하고,
PostgreSQL·Neo4j 데이터 동기화 및 AI Planning 서버와의 연동을 담당했습니다.

---

## 🛠 Tech Stack

### Backend

`Java` `Spring Boot` `Spring Data JPA` `Spring Security`
`REST API` `WebSocket`

### Database / Cache

`PostgreSQL` `MySQL` `Neo4j` `Redis`

### Infra / Tools

`Docker` `AWS` `Git` `GitHub` `Postman`

---

## 📌 Featured Projects

### 🤖 LARO — Digital Twin 기반 자율 창고 운영 및 다중 로봇 작업 최적화

**2026.07 ~ 2026.08 | Backend Developer**

창고·재고·로봇 상태를 Digital Twin으로 관리하고,
AI Planning과 경로 최적화를 활용해 다중 로봇의 작업 배정·이동 계획·재계획을 수행하는 팀 프로젝트입니다.

**담당 및 구현**

* Warehouse / Zone / Node / Edge API 및 창고·로봇·그래프 도메인 구현
* Shared Warehouse의 실행 데이터를 복제하여 USER / GUEST별 독립적인 Simulation 환경 구성
* Warehouse Resource 소유권 검증 및 사용자별 데이터 접근 제어
* PostgreSQL을 기준 데이터로 두고 `AFTER_COMMIT` 이후 Neo4j를 동기화하는 Graph Sync 구조 구현
* AI 서버의 작업 계획을 Backend Task · Robot Plan · Simulation 실행 데이터와 연동
* 장애물 발생 시 기존 실행 상태를 기반으로 경로를 다시 계산하는 동적 재계획 흐름 구현

**프로젝트 결과**

* 팀 프로젝트 실험에서 Agent 기반 작업 분산을 통해 Rule 방식 대비 작업 완료시간 **최대 64% 단축**

**Tech**

`Spring Boot` `JPA` `PostgreSQL` `Redis` `Neo4j`
`WebSocket` `FastAPI Integration` `Docker`

🔗 **Backend Portfolio**
https://github.com/pbjun2000/digital-twin-warehouse-backend

🔗 **Team Project**
https://github.com/kt-aivle-big-project

---

### ☁️ BookService AWS CI/CD & Monitoring

**2026.06 | Backend / Cloud Project**

React + Spring Boot 서비스를 AWS 환경에 배포하고
CI/CD와 모니터링 흐름을 경험한 팀 프로젝트입니다.

* Docker 기반 Spring Boot 애플리케이션 이미지 구성
* AWS CodeBuild · ECR 기반 Build 및 Container Image 관리
* EKS 기반 Container 배포
* Kubernetes Deployment / Service 구성
* CloudWatch를 활용한 애플리케이션 로그 및 운영 상태 확인

🔗 https://github.com/pbjun2000/aivle-book-service-aws-review

---

### 📚 AI Book Service

**2026.06 | Backend Developer**

React 기반 도서 관리 서비스를 Spring Boot REST API 구조로 전환한 팀 프로젝트입니다.

* Spring Data JPA 기반 도서 CRUD 및 검색 API 구현
* Entity 직접 반환 대신 DTO 기반 응답 구조 적용
* `GlobalExceptionHandler`를 활용한 공통 예외 처리
* Postman을 활용한 정상·예외 API 테스트

🔗 https://github.com/pbjun2000/aivle-ai-book-service-review

---

## 🎓 Education & Training

### 목원대학교 컴퓨터공학과

**2019.03 ~ 2026.02 | 졸업**

### KT AIVLE School 9기

**2026.09.03 수료 예정**

* AI·데이터 분석 및 IT 서비스 개발 교육 과정 이수 중
* 빅프로젝트 LARO에서 Java / Spring Boot 기반 Backend Developer로 참여

---

## 📫 Contact

**Email**
[qudwns526@naver.com](mailto:qudwns526@naver.com)

**Tech Blog**
https://qudwns526.tistory.com

