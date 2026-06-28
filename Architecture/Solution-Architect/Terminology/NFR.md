# NFR (Non-Functional Requirements, 비기능 요구사항)

## Definition

시스템이 "무엇을 해야 하는가"(기능 요구사항)가 아닌, "얼마나 잘 해야 하는가"를 정의하는 요구사항.

아키텍처 결정에 가장 큰 영향을 미치는 요구사항이며, 솔루션 설계의 출발점이다.

## Context / When to Use

솔루션 설계 초기 단계에서 고객과 함께 정의. 이후 [[Solution-Review-Checklist]]와 아키텍처 리뷰의 기준이 된다.

## 주요 NFR 카테고리

| 카테고리 | 예시 측정 목표 | 관련 용어 |
|---|---|---|
| **성능 (Performance)** | p95 응답시간 < 200ms, TPS > 1,000 | |
| **가용성 (Availability)** | 99.9% SLO, MTTR < 30분 | [[High-Availability]] |
| **확장성 (Scalability)** | 트래픽 10배 수용 시 응답시간 유지 | [[Scalability]] |
| **보안 (Security)** | OWASP Top 10 충족, 데이터 암호화 | |
| **재해 복구 (DR)** | RTO < 4시간, RPO < 1시간 | |
| **유지보수성 (Maintainability)** | 배포 빈도 주 1회 이상 | |
| **규정 준수 (Compliance)** | GDPR, 개인정보보호법, ISO 27001 | |

## NFR 정의 방법

좋은 NFR은 **측정 가능**해야 한다. 모호한 NFR은 검증할 수 없다.

| 나쁜 NFR | 좋은 NFR |
|---|---|
| "시스템은 빠르게 응답해야 한다" | "p95 API 응답시간 200ms 이하" |
| "높은 가용성을 보장해야 한다" | "연간 가용성 99.9% 이상 (다운타임 < 8.76시간)" |
| "보안이 강해야 한다" | "OWASP Top 10 모든 항목 충족, 연 1회 침투 테스트" |

## NFR vs 기능 요구사항 (FR)

| 구분 | 기능 요구사항 (FR) | 비기능 요구사항 (NFR) |
|---|---|---|
| **초점** | 무엇을 하는가 | 얼마나 잘 하는가 |
| **예시** | "사용자는 로그인할 수 있다" | "로그인 응답시간 < 500ms" |
| **영향** | 기능 구현 방식 결정 | 아키텍처 패턴·인프라 결정 |

## Related Terms

- [[High-Availability]] — 가용성 NFR 상세
- [[Scalability]] — 확장성 NFR 상세
- [[Trade-off]] — NFR 간 트레이드오프
- [[Solution-Review-Checklist]] — NFR 충족 여부 체크

## References

- TOGAF, "Non-Functional Requirements"
- ISO/IEC 25010 — 소프트웨어 품질 특성 국제 표준
