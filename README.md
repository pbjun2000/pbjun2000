# 안녕하세요, 백엔드 개발자 박병준입니다.

Java·Spring Boot 기반으로 백엔드 API와 서비스 실행 구조를 구현해왔습니다.

최근 **Digital Twin 기반 자율 창고 프로젝트 LARO**에서 창고·로봇·이동 그래프 API를 담당했습니다.
PostgreSQL을 기준 데이터로 한 Neo4j 동기화, USER/GUEST별 Simulation 환경 분리, AI Planning과 Backend 실행 데이터 연동을 구현했습니다.

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

### 🤖 LARO — LLM Autonomous Robot Orchestration

**Digital Twin 기반 자율 창고 운영 및 다중 로봇 작업 최적화 시스템**

`2026.07 ~ 2026.08` · `Backend Developer`

창고·재고·로봇 상태를 Digital Twin으로 관리하고,
AI Planning과 경로 최적화를 활용해 다중 로봇의 작업 배정·이동 계획·재계획을 수행하는 팀 프로젝트입니다.

<p align="center">
  <img src="./assets/laro-live-view.png" width="100%" alt="LARO Warehouse Live View">
</p>

#### 담당 및 구현

* Warehouse / Zone / Node / Edge REST API와 관련 도메인 구현
* Shared Warehouse를 복제해 USER / GUEST별 독립적인 Simulation 환경 구성
* Simulation 실행 전 Warehouse 소유권을 검증해 다른 사용자의 실행 환경 접근 차단
* PostgreSQL 트랜잭션 완료 후 Neo4j Graph를 동기화하도록 `AFTER_COMMIT` 기반 Graph Sync 구조 구현
* AI Planning에서 사용할 Warehouse Graph API와 창고·로봇 데이터 연동

#### 프로젝트 결과

* 동일 Optimization Solver 조건의 팀 실험에서 Agent 방식이 Rule 방식 대비 작업 완료시간 **최대 64% 단축**

#### Tech Stack

`Spring Boot` `Spring Data JPA` `PostgreSQL` `Redis` `Neo4j`
`WebSocket` `Docker`

🔗 **Backend Portfolio**
https://github.com/pbjun2000/digital-twin-warehouse-backend

🔗 **Team Project**
https://github.com/kt-aivle-big-project

---

### 📚 Book Service — Backend & AWS Deployment

`2026.06` · `Backend / Cloud Project`

React 기반 도서 관리 서비스를 Spring Boot REST API로 전환하고,
AWS 환경에 배포해 CI/CD와 모니터링까지 연결한 팀 프로젝트입니다.

#### 담당 및 구현

* Spring Data JPA 기반 도서 CRUD·검색 REST API 구현
* DTO 기반 응답 구조와 `GlobalExceptionHandler`를 적용해 API 응답·예외 처리 분리
* Postman으로 정상·예외 API 동작 검증
* Docker 이미지 빌드 후 AWS ECR·EKS 환경에 애플리케이션 배포
* CodeBuild 기반 CI/CD 구성 및 CloudWatch를 통한 로그·운영 상태 확인

#### Tech Stack

`Spring Boot` `Spring Data JPA` `Docker` `AWS`
`CodeBuild` `ECR` `EKS` `Kubernetes` `CloudWatch`

🔗 **Backend Development**
https://github.com/pbjun2000/aivle-ai-book-service-review

🔗 **AWS CI/CD & Monitoring**
https://github.com/pbjun2000/aivle-book-service-aws-review

---

## 🎓 Education & Training

### 목원대학교 컴퓨터공학과

`2019.03 ~ 2026.02` · 졸업

### KT AIVLE School 9기

`2026.03 ~ 2026.09` · 2026.09.03 수료 예정

* AI·데이터 분석 및 IT 서비스 개발 과정
* Java·Spring Boot 기반 백엔드 개발 및 AI 서비스 연동 프로젝트 수행

---

## 🏆 Award

### AI융합페스티벌 × 컴퓨터공학과 제38회 학술제 최우수상

`2025.12` · 목원대학교 SW중심대학사업추진단

* Unity 기반 카드게임 **ARCANA** 팀 프로젝트로 최우수상 수상

---

## 📫 Contact

**Email**
[qudwns526@naver.com](mailto:qudwns526@naver.com)

**Tech Blog**
https://qudwns526.tistory.com

