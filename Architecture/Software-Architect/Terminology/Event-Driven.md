# 이벤트 기반 아키텍처 (Event-Driven Architecture, EDA)

## Definition

시스템 구성 요소가 이벤트(상태 변화의 신호)를 생성·탐지·소비함으로써 상호작용하는 아키텍처 패턴.

직접 호출 대신 이벤트로 통신하므로 컴포넌트 간 [[Coupling|결합도]]가 낮아진다.

## Context / When to Use

서비스 간 낮은 결합도가 필요하거나, 비동기 처리로 성능을 높여야 하는 시스템.

## 핵심 컴포넌트

| 컴포넌트 | 역할 | 예시 |
|---|---|---|
| **Event Producer** | 이벤트 생성·발행 | 주문 서비스 |
| **Event Broker** | 이벤트 라우팅·저장 | Kafka, RabbitMQ, AWS SNS |
| **Event Consumer** | 이벤트 구독·처리 | 결제 서비스, 알림 서비스 |
| **Event Store** | 이벤트 영속 저장 (Event Sourcing) | Kafka, EventStoreDB |

## 이벤트 처리 방식

| 방식 | 설명 | 특징 |
|---|---|---|
| **Event Notification** | 변경 사실만 알림, 상세는 조회 | 경량, 낮은 결합도 |
| **Event-Carried State Transfer** | 이벤트에 상태 포함 | 수신자가 독립적 처리 가능 |
| **Event Sourcing** | 이벤트가 시스템 상태의 유일한 소스 | 감사 로그, 타임트래블 가능 |

## 장단점

| 장점 | 단점 |
|---|---|
| 낮은 결합도 — 서비스 독립 배포 가능 | 디버깅·추적 어려움 (분산 트레이싱 필요) |
| 높은 확장성 | 최종 일관성(Eventual Consistency) 수용 필요 |
| 서비스 간 독립적 진화 | 이벤트 스키마 버전 관리 필요 |
| 비동기 처리로 성능 향상 | 시스템 복잡도 증가 |

## 적용 시나리오

- MSA에서 서비스 간 통신 (Kafka, RabbitMQ)
- 실시간 데이터 파이프라인
- [[CQRS]] + Event Sourcing 조합
- 사용자 행동 이벤트 수집 (Analytics)

## Related Terms

- [[CQRS]] — EDA와 함께 자주 사용
- [[Domain-Driven-Design]] — Domain Event 개념
- [[Coupling]] — EDA로 결합도 낮추기
- [[Architecture-Patterns]] — 아키텍처 패턴

## References

- Martin Fowler, "What do you mean by 'Event-Driven'?" (martinfowler.com)
