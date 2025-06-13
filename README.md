# 개발 환경용 Docker 인프라

이 레포지토리는 로컬 개발을 위한 Docker 기반 인프라 환경 구성을 위한 것입니다.  
PostgreSQL, Redis, Mailhog, MinIO, Adminer, Nginx 등 개발 환경에서 자주 사용하는 기본 서비스들이 포함되어 있습니다. 

**웹 애플리케이션은 별도의 프로젝트에서 이 인프라와 네트워크를 공유해 연결하는 구조를 전제로 합니다.**

---

## 📦 포함된 서비스 목록

| 서비스       | 설명                                 | 포트         |
| ------------ | ------------------------------------ | ------------ |
| PostgreSQL   | 데이터베이스                         | 5432         |
| Redis        | 캐시 서버                            | 6379         |
| Mailhog      | 테스트용 SMTP 서버 및 UI             | 1025 / 8025  |
| MinIO        | S3 호환 오브젝트 스토리지           | 9000 / 9001  |
| Adminer      | DB 관리 웹 UI                        | 8080         |
| Nginx        | Reverse Proxy 및 라우팅              | 80           |

---

## 🛠 사용법

### 1. 레포지토리 클론

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
````

---

### 2. `.env` 파일 생성

`.env.template` 파일을 참고하여 `.env` 파일을 작성하세요.

```bash
cp .env.template .env
```

---

### 3. Nginx 설정 파일 생성

`nginx/conf.d/default.conf.template` 파일을 참고하여 `nginx/conf.d/default.conf` 파일을 생성하세요.

**이 때 개별 어플리케이션 서버에 대한 경로도 함께 추가하세요.**

```bash
cp nginx/conf.d/default.conf.template nginx/conf.d/default.conf
```

---

### 4. Docker 인프라 실행

```bash
docker-compose up -d
```

정상 실행 여부를 확인하려면:

```bash
docker ps
```

---

## 🧼 종료 및 정리

```bash
docker-compose down
```

---

## 📁 폴더 구조

```
.
├── docker-compose.yml
├── .env.template
├── nginx/
│   ├── nginx.conf
│   ├── conf.d
│   ├── ├── default.conf.template
├── .gitignore
├── README.md
```

---

## 📌 주의사항
- 본 레포지토리는 FastAPI, NestJS 등과 같은 애플리케이션 서버를 포함하지 않습니다.
- 모든 서비스는 내부 공유 네트워크(`shared_net`)를 통해 통신합니다. 별도 애플리케이션도 해당 네트워크에 연결해야 합니다.