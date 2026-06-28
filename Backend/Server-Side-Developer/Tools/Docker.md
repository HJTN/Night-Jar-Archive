# Docker

> 컨테이너 기반 애플리케이션 패키징·실행 도구

## Overview

Docker는 애플리케이션과 그 의존성을 컨테이너로 패키징해 어디서나 동일하게 실행할 수 있게 한다. 서버 개발자에게는 **"내 PC에서는 됐는데"** 문제를 해결하고, 개발·테스트·운영 환경의 일관성을 보장하는 핵심 도구다.

## 서버 개발자 관점의 핵심 활용

### 1. 개발 환경 일관성
팀원 모두가 동일한 버전의 DB, Redis, Kafka를 사용. `docker-compose.yml` 하나로 모든 인프라를 코드로 관리한다.

### 2. docker-compose로 로컬 인프라 실행

```yaml
# docker-compose.yml
version: '3.8'
services:
  mysql:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: myapp
      MYSQL_USER: appuser
      MYSQL_PASSWORD: apppass
    ports:
      - "3306:3306"
    volumes:
      - mysql-data:/var/lib/mysql  # 데이터 영속화

  redis:
    image: redis:7.2-alpine
    ports:
      - "6379:6379"
    command: redis-server --requirepass redispass

  kafka:
    image: confluentinc/cp-kafka:7.5.0
    environment:
      KAFKA_BROKER_ID: 1
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://localhost:9092
    ports:
      - "9092:9092"
    depends_on:
      - zookeeper

  zookeeper:
    image: confluentinc/cp-zookeeper:7.5.0
    environment:
      ZOOKEEPER_CLIENT_PORT: 2181

volumes:
  mysql-data:
```

### 3. Dockerfile 작성 (Spring Boot)

```dockerfile
# 멀티 스테이지 빌드: 빌드 환경과 실행 환경 분리
FROM eclipse-temurin:17-jdk AS builder
WORKDIR /app
COPY gradlew build.gradle settings.gradle ./
COPY gradle ./gradle
# 의존성 레이어 캐싱 (소스 변경 없으면 재다운로드 안 함)
RUN ./gradlew dependencies --no-daemon
COPY src ./src
RUN ./gradlew bootJar --no-daemon

FROM eclipse-temurin:17-jre
WORKDIR /app
# 보안: root 대신 전용 사용자 실행
RUN addgroup --system appgroup && adduser --system --group appuser
USER appuser
COPY --from=builder /app/build/libs/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

## 주요 명령어

| 명령어 | 설명 |
|--------|------|
| `docker compose up -d` | 백그라운드로 컨테이너 시작 |
| `docker compose down` | 컨테이너 중지 및 제거 |
| `docker compose down -v` | 컨테이너 + 볼륨 제거 (DB 초기화) |
| `docker compose logs -f [서비스명]` | 실시간 로그 확인 |
| `docker compose ps` | 컨테이너 상태 확인 |
| `docker exec -it [컨테이너명] bash` | 컨테이너 내부 셸 접속 |
| `docker exec -it mysql mysql -u root -p` | MySQL 컨테이너 접속 |
| `docker build -t myapp:latest .` | 이미지 빌드 |
| `docker images` | 로컬 이미지 목록 |
| `docker system prune` | 미사용 컨테이너/이미지 정리 |

## Tips

- `.dockerignore` 파일로 빌드 컨텍스트에서 불필요한 파일 제외 (`target/`, `node_modules/`, `.git/`)
- 레이어 캐싱 활용: 변경 빈도가 낮은 명령(`COPY dependencies`)을 앞에, 자주 변경되는 명령(`COPY src`)을 뒤에 배치
- 프로덕션 이미지는 JDK 대신 JRE 사용 (이미지 크기 최소화)
- 헬스체크 설정으로 컨테이너 준비 상태 확인

```yaml
healthcheck:
  test: ["CMD", "mysqladmin", "ping", "-h", "localhost"]
  interval: 10s
  timeout: 5s
  retries: 5
```

## References

- [Docker 공식 문서](https://docs.docker.com/)
- [Docker Compose 파일 레퍼런스](https://docs.docker.com/compose/compose-file/)
