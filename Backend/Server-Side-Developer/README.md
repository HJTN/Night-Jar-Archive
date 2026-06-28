# Server-Side Developer

> 비즈니스 로직 및 서버 애플리케이션 개발 (Java/Spring, Python, Node.js, Go 등)

## Overview

서버 사이드 개발자는 비즈니스 로직·데이터 처리·API 제공 등 애플리케이션의 서버 측을 구현하는 전문가다. 클라이언트(웹/앱)가 요청하면 서버는 비즈니스 규칙을 수행하고 DB에서 데이터를 조회·가공해 응답한다. 성능, 안정성, 보안을 고려한 서버 코드를 작성하는 것이 핵심 역할이다.

서버 사이드 개발자는 단순히 동작하는 코드를 넘어, 수천~수만 건의 동시 요청을 안정적으로 처리하고 장애 상황에서도 서비스가 지속될 수 있도록 설계한다.

## Key Responsibilities

- **비즈니스 로직 구현**: 도메인 규칙을 코드로 표현하고 서비스 레이어를 설계한다
- **DB 설계 및 쿼리 최적화**: 스키마 설계, 인덱스 전략, 슬로우 쿼리 개선
- **API 제공**: RESTful 또는 GraphQL API 설계 및 구현, API 문서화
- **캐싱 전략**: Redis 등을 활용해 DB 부하를 줄이고 응답 속도를 높인다
- **메시지 큐 연동**: Kafka/RabbitMQ로 서비스 간 비동기 통신 구현
- **성능 튜닝**: 프로파일링, 병목 탐지, 쿼리 최적화, 리소스 관리
- **코드 리뷰**: 팀 코드 품질 유지, 보안·성능·가독성 관점에서 리뷰

## Core Skills

| 분야 | 핵심 기술 | 도구/프레임워크 |
|------|-----------|----------------|
| 언어 | Java, Kotlin, Python, Go, Node.js | - |
| 프레임워크 | Spring Boot, FastAPI, Express, Gin | Maven/Gradle |
| 데이터베이스 | SQL 작성, 인덱스 설계, 트랜잭션 | MySQL, PostgreSQL |
| 캐싱 | Cache-Aside, Write-Through, TTL 관리 | Redis, Memcached |
| 메시지 큐 | Producer/Consumer 패턴, 전달 보장 | Kafka, RabbitMQ |
| 인증/인가 | JWT, OAuth2, 세션 관리 | Spring Security |
| 컨테이너 | Dockerfile 작성, docker-compose | Docker |
| 버전 관리 | Git Flow, Trunk-Based, 코드 리뷰 | Git, GitHub/GitLab |
| 운영체제 | Linux 명령어, 프로세스·로그 관리 | Linux |
| IDE | 디버거, 단축키, 플러그인 활용 | IntelliJ IDEA |

## Related Notes

### Terminology (용어)
- [[Caching]] - 캐싱 전략 (Cache-Aside, Write-Through, TTL)
- [[Concurrency]] - 동시성, Race Condition, 락 메커니즘
- [[Connection-Pool]] - DB 커넥션 풀, HikariCP
- [[JWT]] - JSON Web Token, 인증 토큰 구조와 보안
- [[Message-Queue]] - 메시지 큐, Kafka vs RabbitMQ
- [[Middleware]] - 미들웨어, 요청-응답 파이프라인
- [[ORM]] - ORM, N+1 문제, JPA/Hibernate

### Tools (도구)
- [[Docker]] - 컨테이너화, docker-compose 환경 구성
- [[Git]] - 버전 관리, 브랜치 전략
- [[IntelliJ-IDEA]] - Java/Spring 개발 IDE
- [[Linux]] - 서버 운영에 필요한 Linux 명령어
- [[Maven]] - Java 빌드 도구
- [[Postman]] - API 테스트 및 자동화
- [[VS-Code]] - 경량 에디터, REST Client 플러그인

### Core Tasks (핵심 업무)
- [[Feature-Development-Flow]] - 기능 개발 전체 흐름 (요구사항 → 배포)
- [[Performance-Tuning-Process]] - 성능 튜닝 프로세스
- [[Code-Review-Checklist]] - 코드 리뷰 체크리스트
- [[Deployment-Checklist]] - 배포 전 체크리스트

### Guide & Templates
- [[Server-Side-Developer-Guide]] - 종합 가이드 및 마인드맵
- [[Feature-Spec-Template]] - 기능 개발 스펙 문서 템플릿
