# 🗳️ Voteland

> **Voteland**는 사용자가 주제에 대해 투표하고 결과를 실시간으로 확인할 수 있는 **투표 플랫폼**입니다.
> MSA(Microservices Architecture)를 지향하여 멀티 모듈로 구성된 Spring Boot 백엔드와 Vue.js 프론트엔드, 그리고 **GitOps(App of Apps)** 기반의 CI/CD 파이프라인을 구축한 것이 특징입니다.

## 📑 목차 (Table of Contents)
1. [팀원 소개 (Team Info)](#team-info)
2. [기획 의도 (Context)](#context)
3. [핵심 기능 (Key Features)](#key-features)
4. [Tech Stack](#tech-stack)
5. [System Architecture (시스템 아키텍처)](#system-architecture)
6. [Project Structure (프로젝트 구조)](#project-structure)
7. [Getting Started (시작하기)](#getting-started)
8. [Deployment (배포)](#deployment)

---

## 1. 👥 팀원 소개 (Team Info) <a id="team-info"></a>

| <img src="https://github.com/Steve.png" width="100"> | <img src="https://github.com/Alo.png" width="100"> | <img src="https://github.com/steven.png" width="100"> | <img src="https://github.com/johnmayer.png" width="100"> | <img src="https://github.com/chris.png" width="100"> |
| :---: | :---: | :---: | :---: | :---: |
| **강윤혜** | **송형욱** | **이관호** | **이인재** | **진희헌** |
| [@ChoiKYH](https://github.com/ChoiKYH) | [@haengguk](https://github.com/haengguk) | [@Apeirogon99](https://github.com/Apeirogon99) | [@INJAELEE99](https://github.com/INJAELEE99) | [@ucb1122](https://github.com/ucb1122) |

---

## 2. 🎯 기획 의도 (Context) <a id="context"></a>
- **확장성**: 트래픽 증가와 서비스 확장에 유연하게 대응할 수 있는 아키텍처 설계
- **자동화**: 반복적인 빌드/배포 과정을 자동화하여 개발 생산성 향상 (DevOps)
- **사용자 경험**: 직관적인 UI와 실시간 데이터 반영을 통한 몰입감 있는 서비스 제공

---

## 3. 💡 핵심 기능 (Key Features) <a id="key-features"></a>

### 🔐 1. 사용자 인증 (User Authentication)
- **회원가입 및 로그인**: JWT(JSON Web Token) 기반의 보안 인증 시스템
- **접근 제어**: 로그인한 사용자만 투표 생성 및 참여 가능

### 🗳️ 2. 투표 서비스 (Vote Service)
- **투표 목록 조회**: 진행 중인 다양한 투표 주제를 한눈에 확인
- **투표 생성**: 사용자가 직접 제목, 선택지 등을 설정하여 새로운 투표 개설
- **투표 참여**: 직관적인 UI를 통해 원하는 항목에 투표
- **실시간 결과 확인**: 투표 직후 그래프 등을 통해 현재 득표 현황 시각적 확인

---

## 4. 🛠️ Tech Stack <a id="tech-stack"></a>

### Frontend
![Vue.js](https://img.shields.io/badge/vuejs-%2335495e.svg?style=for-the-badge&logo=vuedotjs&logoColor=%234FC08D)
![Vite](https://img.shields.io/badge/vite-%23646CFF.svg?style=for-the-badge&logo=vite&logoColor=white)
![Axios](https://img.shields.io/badge/axios-%235A29E4.svg?style=for-the-badge&logo=axios&logoColor=white)

### Backend
![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/spring%20boot-%236DB33F.svg?style=for-the-badge&logo=springboot&logoColor=white)
![Gradle](https://img.shields.io/badge/Gradle-02303A.svg?style=for-the-badge&logo=Gradle&logoColor=white)
![MySQL](https://img.shields.io/badge/mysql-%2300f.svg?style=for-the-badge&logo=mysql&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring%20Security-6DB33F?style=for-the-badge&logo=Spring%20Security&logoColor=white)

### DevOps & Infrastructure
![Jenkins](https://img.shields.io/badge/jenkins-%232C5263.svg?style=for-the-badge&logo=jenkins&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white)
![ArgoCD](https://img.shields.io/badge/argocd-%23eb5b46.svg?style=for-the-badge&logo=argo&logoColor=white)
![GitLab](https://img.shields.io/badge/gitlab-%23181717.svg?style=for-the-badge&logo=gitlab&logoColor=white)

---

## 5. 🏗️ System Architecture (시스템 아키텍처) <a id="system-architecture"></a>

### 서비스 흐름 (Service Flow)
1. **Client**: 사용자의 요청이 **Ingress Controller**로 전달됩니다.
2. **Ingress**: 요청 경로(Path)에 따라 트래픽을 `frontend` 또는 `backend` 서비스로 라우팅합니다.
3. **Backend**: `core` 모듈에서 비즈니스 로직을 처리하며, `storage` 모듈을 통해 데이터베이스에 접근합니다.

### ☁️ CI/CD & GitOps (App of Apps)
본 프로젝트는 **ArgoCD App of Apps** 패턴을 적용하여, 하나의 Root Application이 다수의 서비스(Backend, Frontend)를 관리하는 계층적 구조를 가집니다.

1. **Developer**: 개발자가 코드를 `dev` 브랜치에 푸시(Push)합니다.
2. **Jenkins**: 변경 사항을 감지하여 빌드(`Gradle` & `npm`) 및 테스트를 수행합니다.
3. **Build & Push**: Docker 이미지를 빌드하고 **Docker Hub**에 푸시합니다.
4. **Update Manifest**: Jenkins가 **Kubernetes Manifest Repository (본 저장소)**의 이미지 태그 버전을 자동으로 업데이트합니다.
5. **ArgoCD Sync**:
   - **Root App**: `apps` 디렉토리를 감시하며 하위 애플리케이션(`frontend`, `backend`)을 생성/동기화합니다.
   - **Child Apps**: 생성된 앱들은 `k8s` 디렉토리 내의 매니페스트(`deployment`, `service` 등)를 클러스터에 배포합니다.

---

## 6. 📂 Project Structure (프로젝트 구조) <a id="project-structure"></a>

이 프로젝트는 **애플리케이션 코드 저장소**와 **설정(Config) 저장소**로 역할이 나뉘어 있으며, 본 레포지토리는 설정 저장소에 해당합니다.

### 1. Infra/Config Repository (Current)
**App of Apps** 구성을 위한 ArgoCD 및 Kubernetes 매니페스트 구조입니다.

```bash
.
├── apps
│   └── dev
│       ├── backend.yaml   
│       └── frontend.yaml 
└── k8s
    ├── backend
    │   ├── deployment.yaml
    │   └── service.yaml
    └── frontend
        ├── deployment.yaml
        ├── service.yaml
        └── ingress.yaml
```

| 디렉토리 (Directory) | 설명 (Description) |
| :--- | :--- |
| **`apps/`** | **ArgoCD Applications**: 마이크로서비스(`backend`, `frontend`)를 정의하는 ArgoCD Application 매니페스트가 위치합니다. (App of Apps 패턴의 핵심) |
| **`k8s/`** | **Kubernetes Manifests**: 실제 배포되는 리소스(`Deployment`, `Service`, `Ingress`) 정의 파일들이 각 서비스별로 위치합니다. |

### 2. Application Repository (Source Code)
멀티 모듈 구조로 설계된 실제 애플리케이션 코드입니다.

```bash
.
├── clients    
├── core       
├── frontend   
├── storage    
└── support    
```

| 모듈 (Module) | 설명 (Description) |
| :--- | :--- |
| **`clients`** | 외부 시스템과의 HTTP 통신 등을 담당합니다. (`client-example` 등) |
| **`core`** | 비즈니스 로직과 도메인 핵심 기능을 담당합니다. (`core-api`, `domain-user`, `domain-vote` 등) |
| **`frontend`** | Vue.js 기반의 프론트엔드 애플리케이션 코드가 위치합니다. |
| **`storage`** | 데이터베이스와의 연결 및 Entity 정의를 담당합니다. (`db-core` 등) |
| **`support`** | 로깅, 모니터링, 보안 등 공통적으로 사용되는 지원 기능을 담당합니다. (`logging`, `security`, `monitoring`) |


---

## 7. 🚀 Getting Started (시작하기) <a id="getting-started"></a>

### 필수 요구사항 (Prerequisites)
- Java 17+
- Node.js 20+
- Docker
- Kubernetes Cluster & ArgoCD

### Backend 설정 및 실행
1. **환경 변수 설정**:
   프로젝트 `root` 경로에 `.env` 파일을 생성하거나 환경 변수를 설정합니다. (`.env.example` 파일을 참고하세요.)
   
2. **빌드 및 실행**:
   ```bash
   # Windows
   ./gradlew clean build
   java -jar core/core-api/build/libs/core-api-0.0.1-SNAPSHOT.jar
   
   # Linux/Mac
   ./gradlew clean build
   java -jar core/core-api/build/libs/core-api-0.0.1-SNAPSHOT.jar
   ```

### Frontend 설정 및 실행
1. **의존성 설치**:
   ```bash
   cd frontend
   npm install
   ```

2. **개발 서버 실행**:
   ```bash
   npm run dev
   ```
   브라우저에서 `http://localhost:5173` (기본 포트)으로 접속하여 확인합니다.

---

## 8. 🚢 Deployment (배포) <a id="deployment"></a>

**GitOps (ArgoCD)** 를 통해 배포가 자동화되어 있습니다.

- **App of Apps**: `apps/` 디렉토리에 정의된 설정에 따라 ArgoCD가 클러스터의 상태를 Git 저장소와 동일하게 유지합니다.
- `Jenkinsfile`에 정의된 파이프라인이 빌드 및 이미지 푸시 후, 본 저장소의 매니페스트(이미지 태그)를 업데이트하면 자동으로 배포가 수행됩니다.

---
