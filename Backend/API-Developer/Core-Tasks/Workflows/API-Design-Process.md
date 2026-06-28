# API Design Process

> 요구사항 분석부터 OpenAPI 스펙 확정까지 API 설계 흐름

## Overview

API 설계는 구현보다 먼저 이루어지는 계약(Contract) 수립 과정이다. 잘못 설계된 API는 이후 수정 비용이 크므로, 코드를 한 줄도 작성하기 전에 스펙을 확정하고 이해관계자 리뷰를 받는 것이 핵심이다. [[API-First-Design]] 원칙에 따라 명세 → 구현 순서를 지킨다.

## Steps

1. **요구사항 파악**
   - 어떤 클라이언트가(앱/웹/파트너), 어떤 데이터를, 어떤 행위로 필요로 하는지 명확화
   - 유즈케이스 목록 작성: "사용자가 상품 목록을 필터링해서 조회한다"
   - 비기능 요구사항 확인: 예상 TPS, 응답 시간 목표, 인증 방식

2. **리소스 식별**
   - 명사(Noun)로 핵심 리소스 추출: `User`, `Order`, `Product`, `Payment`
   - DB 테이블과 1:1 매핑하지 않음 — 도메인 관점의 리소스 정의
   - [[DBeaver]]로 기존 데이터 모델 파악 참조

3. **HTTP 메서드·URI 설계**
   - [[REST]] 원칙에 따라 리소스별 CRUD 엔드포인트 설계
   - 계층 관계 표현: `/users/{userId}/orders`
   - URI 명사 복수형, 소문자, 하이픈 사용

4. **Request / Response 스펙 정의**
   - 요청: Path parameter, Query parameter, Request body 필드 및 타입 정의
   - 응답: 성공 응답 구조, [[HTTP-Status-Code]] 매핑, 에러 응답 형식 통일
   - [[Pagination]] 방식 결정 (Offset vs Cursor)
   - 인증 방식 확인: Bearer Token, API Key

5. **OpenAPI 문서 작성**
   - OpenAPI 3.0 YAML로 정식 스펙 문서 작성
   - [[Swagger]] Editor나 [[IntelliJ-IDEA]]에서 작성
   - 각 엔드포인트에 summary, description, example 값 포함

6. **이해관계자 리뷰**
   - 프론트엔드·앱 개발자, 백엔드 팀원, PM과 스펙 리뷰
   - [[API-Review-Checklist]] 기준으로 체크
   - 피드백 반영 후 스펙 확정 (이 시점 이후 Breaking Change는 버전 증가 필요)

7. **구현 시작**
   - 확정된 스펙을 기준으로 [[API-Development-Flow]] 진행
   - Spring Boot 기준: Controller → Service → Repository 순서

## Inputs

- 기획 문서, 유저 스토리
- 기존 DB 스키마 (ERD)
- 유사 API 레퍼런스 (사내 기존 API, REST API 가이드라인)

## Outputs

- OpenAPI 3.0 스펙 문서 (YAML/JSON)
- API 엔드포인트 목록 (Confluence, Notion 등)
- Swagger UI 미리보기 URL

## Notes

- 설계 단계에서 프론트엔드와 함께 리뷰하면 "이 데이터가 왜 없어요?"를 구현 후가 아닌 설계 중에 잡을 수 있음
- Mock 서버(Prism, Stoplight)를 만들면 프론트엔드가 구현 전부터 병렬 개발 가능
- [[Versioning]] 전략을 초기에 결정해두어야 나중에 혼란이 없음
