# 품질 속성 (Quality Attributes)

## Definition

시스템이 "무엇을 하는가"(기능 요구사항)와 달리, "얼마나 잘 하는가"를 측정하는 비기능 요구사항(NFR).

아키텍처 결정은 대부분 품질 속성 간의 **트레이드오프**를 선택하는 것이다.

## 주요 품질 속성

| 속성 | 정의 | 측정 예시 |
|---|---|---|
| **성능 (Performance)** | 요청에 응답하는 속도 | p95 응답시간 < 200ms |
| **가용성 (Availability)** | 시스템이 정상 동작하는 비율 | 99.9% SLO |
| **확장성 (Scalability)** | 부하 증가를 처리하는 능력 | 트래픽 10배 수용 시 응답시간 유지 |
| **보안 (Security)** | 무단 접근 방어 능력 | OWASP Top 10 충족 |
| **유지보수성 (Maintainability)** | 변경·수정의 용이성 | 기능 추가 시 영향 범위 최소화 |
| **신뢰성 (Reliability)** | 올바른 결과를 지속적으로 제공 | MTBF, 오류율 < 0.1% |
| **테스트 가능성 (Testability)** | 동작을 검증하기 쉬운 구조 | 단위 테스트 커버리지 > 80% |
| **관찰 가능성 (Observability)** | 내부 상태를 외부에서 추론하는 능력 | Logs, Metrics, Traces 3가지 기둥 |
| **비용 효율성 (Cost Efficiency)** | 기능 대비 운영 비용 | 월 인프라 비용 목표 내 |

## SLA / SLO / SLI 관계

| 용어 | 의미 |
|---|---|
| **SLI** (Service Level Indicator) | 측정값 (예: 실제 응답시간) |
| **SLO** (Service Level Objective) | 내부 목표 (예: p95 < 200ms) |
| **SLA** (Service Level Agreement) | 고객과의 계약 (예: 99.9% 가용성 보장) |

> SLA 위반 시 패널티. SLO는 SLA보다 엄격하게 설정해 완충지대 확보.

## 트레이드오프 예시

| 선택 | 희생 | 얻음 |
|---|---|---|
| 높은 가용성 (다중화) | 비용 증가, 복잡도 | 장애 내성 |
| 캐시 적용 | 일관성(Consistency) | 성능 향상 |
| MSA | 초기 복잡도 | 독립적 확장성 |
| Event Sourcing | 쿼리 복잡도 | 감사 로그, 이벤트 재생 |

**CAP 정리**: 분산 시스템에서 Consistency, Availability, Partition Tolerance 중 2개만 동시에 달성 가능.

## 아키텍처 리뷰와의 연계

- [[Architecture-Review-Checklist]] — 품질 속성별 체크 항목
- [[Design-Decision-Checklist]] — 트레이드오프 분석 섹션에서 직접 참조

## Related Concepts

- [[Architecture-Patterns]] — 패턴 선택이 품질 속성에 미치는 영향
- [[NFR]] — Solution Architect 관점의 비기능 요구사항
- [[Scalability]] — 확장성 상세

## References

- Len Bass et al., "Software Architecture in Practice" (4th ed.)
- Google SRE Book, "Service Level Objectives"
