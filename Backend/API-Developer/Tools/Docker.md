# Docker

> 컨테이너 기반 애플리케이션 패키징·실행 도구

## Overview

Docker는 애플리케이션과 그 의존성을 컨테이너로 묶어 어느 환경에서나 동일하게 실행할 수 있게 한다. API 개발자에게는 "내 PC에서는 됐는데"를 없애고, 로컬에서 DB·Redis·서버를 한 번에 실행하는 개발 환경 표준화 도구다.

## Key Features

- **이미지**: 실행 환경의 불변 스냅샷 (코드 + 런타임 + 의존성)
- **컨테이너**: 이미지의 실행 인스턴스 (격리된 프로세스)
- **Docker Compose**: 여러 컨테이너를 YAML로 정의하고 함께 실행
- **Docker Hub**: 공개 이미지 레지스트리 (mysql, redis, postgres 등 공식 이미지 제공)
- **Volume**: 컨테이너 외부에 데이터 영속화

## Installation & Setup

```bash
# Docker Desktop 설치 (Windows/Mac)
# https://www.docker.com/products/docker-desktop/

# 설치 확인
docker --version
docker compose version
```

## Common Usage (API 개발자 관점)

### docker-compose.yml — API 개발 환경 표준 구성

```yaml
version: '3.8'

services:
  # Spring Boot API 서버
  api:
    build: .
    ports:
      - "8080:8080"
    environment:
      - SPRING_DATASOURCE_URL=jdbc:mysql://db:3306/myapp
      - SPRING_REDIS_HOST=redis
    depends_on:
      - db
      - redis

  # MySQL DB
  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: myapp
    ports:
      - "3306:3306"
    volumes:
      - db_data:/var/lib/mysql

  # Redis (캐시 / Rate Limiting)
  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"

volumes:
  db_data:
```

### 주요 명령어

```bash
# 환경 시작 (백그라운드)
docker compose up -d

# 환경 중지 및 컨테이너 제거
docker compose down

# 로그 확인
docker compose logs -f api

# 컨테이너 내부 접속
docker compose exec api bash
docker compose exec db mysql -u root -p

# 이미지 재빌드 후 시작
docker compose up -d --build

# 실행 중인 컨테이너 목록
docker ps

# 이미지 목록
docker images

# 중지된 컨테이너 포함 전체 목록
docker ps -a
```

### Dockerfile 예시 (Spring Boot)

```dockerfile
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY build/libs/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

## Tips & Shortcuts

- `.env` 파일로 환경변수 관리: `docker compose`가 자동으로 읽음
- `docker compose exec db mysql` 대신 DBeaver에서 `localhost:3306`으로 접속 가능
- 컨테이너 간 통신은 서비스 이름으로 (예: `http://api:8080`)
- `docker system prune -f`로 미사용 이미지·컨테이너 일괄 정리

## References

- [Docker 공식 문서](https://docs.docker.com/)
- [Docker Compose 스펙](https://docs.docker.com/compose/compose-file/)
