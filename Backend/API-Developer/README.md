# API Developer

> REST/GraphQL API 설계 및 구현

## Overview

API Developer는 클라이언트(앱·웹·파트너)와 서버 간 통신 인터페이스를 설계하고 구현하는 전문가다. HTTP 기반 [[REST]] 및 [[GraphQL]] API를 설계하고, OpenAPI 명세로 문서화하며, 인증·버전 관리·성능 최적화까지 책임진다. 현대 소프트웨어에서 API는 제품의 공개 계약(Contract)이므로, 한 번 잘못 설계된 API는 수정 비용이 크다. [[API-First-Design]] 원칙에 따라 구현보다 설계를 먼저 한다.

## Key Responsibilities

- **API 설계**: 리소스 모델링, HTTP 메서드·URI 설계, Request/Response 스펙 정의
- **구현**: Controller/Service/Repository 레이어 구현, 비즈니스 로직 적용
- **문서화**: OpenAPI 3.0 스펙 작성, [[Swagger]] UI로 인터랙티브 문서 제공
- **버전 관리**: [[Versioning|Breaking Change 없이 API 발전]], Deprecation 정책 운영
- **보안**: JWT/OAuth2 인증·인가, [[Rate-Limiting]], 입력 검증
- **성능 최적화**: [[Pagination]], 캐싱 전략, DB 쿼리 최적화

## Core Skills

| 영역 | 핵심 역량 |
|---|---|
| **API 설계** | [[REST]] 아키텍처, Richardson Maturity Model, URI 설계 원칙 |
| **API 구현** | Spring Boot, Controller/Service/Repository 패턴, 예외 처리 |
| **문서화** | OpenAPI 3.0, [[Swagger]], springdoc-openapi 연동 |
| **인증·보안** | JWT, OAuth2, [[Rate-Limiting]], CORS, HTTPS |
| **테스트** | [[Postman]] Collection, 단위·통합 테스트, Newman CI 연동 |
| **데이터** | [[Pagination]], [[Idempotency]], DB 쿼리 확인([[DBeaver]]) |
| **버전 관리** | [[Versioning]], Semantic Versioning, Deprecation |
| **도구** | [[IntelliJ-IDEA]], [[Docker]], [[Git]] |

## Related Notes

### Terminology
- [[REST]] — REST 아키텍처 스타일, 6가지 제약조건, Richardson Maturity Model
- [[GraphQL]] — Facebook의 API 쿼리 언어, N+1 문제와 DataLoader
- [[HTTP-Status-Code]] — 1xx~5xx 분류, API 주요 코드 상세
- [[Idempotency]] — 멱등성, HTTP 메서드별 특성, Idempotency-Key 패턴
- [[Pagination]] — Offset/Cursor/Keyset 방식 비교
- [[Rate-Limiting]] — Token Bucket 등 알고리즘, 응답 헤더
- [[Versioning]] — URI/헤더 버전 방식, Breaking Change 기준, Deprecation

### Tools
- [[Postman]] — API 테스트, Collection/Environment/Test Script
- [[Swagger]] — OpenAPI 문서화, springdoc-openapi 연동
- [[IntelliJ-IDEA]] — 내장 HTTP Client, Spring Boot 개발
- [[Docker]] — 로컬 개발 환경 구성, docker-compose
- [[Git]] — 브랜치 전략, Conventional Commits, PR 흐름
- [[DBeaver]] — DB 데이터 확인, ERD 시각화, 쿼리 튜닝

### Core Tasks
- [[API-Design-Process]] — 요구사항 파악 → OpenAPI 스펙 확정
- [[API-Development-Flow]] — 구현 → 테스트 → 배포 전체 흐름
- [[API-Review-Checklist]] — URI·HTTP 메서드·보안·응답 구조 리뷰 기준
- [[API-Release-Checklist]] — 배포 전 보안·성능·하위 호환성 최종 점검

### Domain Knowledge
- [[API-First-Design]] — 명세 먼저, 구현 나중 — API First 원칙
- [[RESTful-Design]] — RESTful 설계 규칙, URI/메서드 가이드
- [[API-Security]] — 인증 방법 비교, JWT 구조, OAuth2 플로우
