# 마음나루 — 감정 일기 플랫폼

> **"오늘 나의 감정을 기록하고, 나를 더 잘 이해하세요."**  
> 감정 일기 작성, KoBERT 기반 감정 분류, 명상 음원, 그림 치료, 실시간 채팅까지  
> 마음 건강을 위한 올인원 웹 서비스입니다.

<p>
  <img alt="Spring Boot" src="https://img.shields.io/badge/Spring%20Boot-3.x-6DB33F?style=flat&logo=springboot&logoColor=white">
  <img alt="React" src="https://img.shields.io/badge/React-18-61DAFB?style=flat&logo=react&logoColor=black">
  <img alt="KoBERT" src="https://img.shields.io/badge/KoBERT-감정분석-FF69B4?style=flat">
  <img alt="MySQL" src="https://img.shields.io/badge/MySQL-8.0-4479A1?style=flat&logo=mysql&logoColor=white">
  <img alt="Redis" src="https://img.shields.io/badge/Redis-캐시-DC382D?style=flat&logo=redis&logoColor=white">
  <img alt="AWS" src="https://img.shields.io/badge/AWS-EC2%20%7C%20RDS%20%7C%20S3-FF9900?style=flat&logo=amazonaws&logoColor=white">
  <img alt="GCP" src="https://img.shields.io/badge/Google%20Cloud-KoBERT%20서버-4285F4?style=flat&logo=googlecloud&logoColor=white">
  <img alt="Docker" src="https://img.shields.io/badge/Docker-배포-2496ED?style=flat&logo=docker&logoColor=white">
</p>

---

## 👀 주요 기능

| 기능 | 설명 |
|------|------|
| **감정 일기** | 오늘의 감정을 텍스트로 기록, KoBERT가 자동으로 감정을 분류 |
| **명상** | 명상 음원 재생 및 타이머 설정으로 마음 챙김 |
| **그림 치료** | 직접 그린 그림을 S3에 저장, 그림 치료 기록으로 활용 |
| **실시간 채팅** | WebSocket 기반 실시간 소통 |
| **의료 정보** | 심리/의료 관련 정보 제공 |
| **회원 관리** | JWT 기반 로그인/회원가입, Redis 세션 관리 |

---

## 🏗️ 시스템 아키텍처

<img width="1178" height="710" alt="image" src="https://github.com/user-attachments/assets/03c684b9-dffa-421d-8248-731976e4a244" />


### 기술 스택

**Frontend**
- React 18

**Backend**
- Spring Boot (REST API, WebSocket, JWT 인증)
- Redis (세션 캐시)

**AI**
- KoBERT — 한국어 감정 분류 모델 (Google Cloud 별도 서버, REST API 연동)

**Database / Storage**
- AWS RDS (MySQL)
- AWS S3 (그림, 음원 파일)

**Infra / CI·CD**
- AWS EC2
- Docker
- GitHub Actions (자동 빌드 & 배포)

---

## 📁 프로젝트 구조

```
src/main/java/com/oss/maeumnaru/
├── diary/          # 감정 일기 CRUD, KoBERT 연동
├── global/         # 공통 설정 (보안, 예외처리 등)
├── medical/        # 의료·심리 정보
├── meditation/     # 명상 음원 목록 및 타이머
├── paint/          # 그림 저장 (S3 업로드)
├── user/           # 회원가입, 로그인, JWT
└── Application.java
```

---

## 🚀 실행 방법

### 사전 요구사항

- Java 17+
- Node.js 18+
- Docker & Docker Compose
- AWS 자격증명 설정 (S3, RDS 접근용)

### 백엔드

```bash
# 환경변수 설정
cp .env.example .env
# application.yml에 DB, Redis, JWT, S3, KoBERT 서버 주소 설정

# 빌드 & 실행
./gradlew build
./gradlew bootRun

# 또는 Docker
docker-compose up --build
```

### 프론트엔드

```bash
cd frontend
npm install
npm start
```

### KoBERT 서버 (Google Cloud)

KoBERT 감정 분류 서버는 Google Cloud에 별도 배포되어 있습니다.  
로컬 개발 시에는 `application.yml`의 `kobert.server.url`을 GCP 서버 주소로 설정하세요.

---

## ⚙️ 환경변수

`application.yml` 또는 `.env`에 아래 값을 설정하세요.

```yaml
spring:
  datasource:
    url: jdbc:mysql://<RDS_ENDPOINT>:3306/maeumnaru
    username: <DB_USER>
    password: <DB_PASSWORD>
  redis:
    host: <REDIS_HOST>
    port: 6379

jwt:
  secret: <JWT_SECRET_KEY>

aws:
  s3:
    bucket: <S3_BUCKET_NAME>
    region: ap-northeast-2

kobert:
  server:
    url: https://<GCP_KOBERT_SERVER_URL>  # Google Cloud에 배포된 KoBERT 서버
```

---

## 🔄 CI/CD

GitHub Actions를 통해 `main` 브랜치 push 시 자동으로 빌드 → Docker 이미지 생성 → EC2 배포가 진행됩니다.

```
push to main
    │
    ▼
GitHub Actions
    │
    ├── 테스트 실행
    ├── Docker 이미지 빌드
    └── EC2 배포 (docker-compose up)
```

---

## 🤝 기여 방법

1. 이 레포를 Fork 합니다.
2. 새 브랜치를 생성합니다. (`git checkout -b feature/기능명`)
3. 변경사항을 커밋합니다. (`git commit -m "feat: 기능 설명"`)
4. 브랜치에 Push합니다. (`git push origin feature/기능명`)
5. Pull Request를 생성합니다.

---

## 📄 라이센스

This project is licensed under the MIT License.
