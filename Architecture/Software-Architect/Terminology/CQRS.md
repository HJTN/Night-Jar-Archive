# CQRS (Command Query Responsibility Segregation)

## Definition

명령(Command, 데이터 변경)과 조회(Query, 데이터 읽기)의 책임을 분리하는 패턴.

단일 모델로 읽기·쓰기를 모두 처리하면 복잡해지는 시스템에서 각각 최적화된 모델을 사용한다.

## Context / When to Use

읽기와 쓰기 부하 비율이 크게 다르거나, 조회 성능 최적화가 중요한 시스템.

## 구조

```
[Client]
   ├── Command → Command Handler → Write Model → DB(Write)
   └── Query  → Query Handler  → Read Model  → DB(Read, 비정규화 가능)
```

## 핵심 개념

| 개념 | 설명 |
|---|---|
| **Command** | 시스템 상태를 변경하는 요청. 반환값 없음 또는 성공 여부만 반환 |
| **Query** | 데이터를 조회하는 요청. 상태를 변경하지 않음 |
| **Write Model** | 도메인 규칙을 강제하는 정규화된 모델 |
| **Read Model** | UI/API 최적화를 위해 비정규화된 뷰 모델 |

## CQRS + Event Sourcing 조합

CQRS는 [[Event-Driven|Event Sourcing]]과 함께 사용하면 시너지가 높다:
- Write Model → 이벤트를 저장 (Event Store)
- Read Model → 이벤트를 구독해 프로젝션 생성 (Event Projection)

## 적용 기준

✅ 읽기와 쓰기 부하가 크게 다를 때 (읽기 10배, 쓰기 1배)
✅ 조회 성능 최적화가 중요할 때 (복잡한 JOIN 쿼리 제거)
✅ 복잡한 도메인 로직이 있는 시스템
✅ 마이크로서비스 아키텍처에서 서비스별 데이터 격리

❌ 단순 CRUD 애플리케이션 — 과도한 복잡성
❌ 팀이 이벤트 소싱 경험이 없는 경우

## 트레이드오프

| 장점 | 단점 |
|---|---|
| 읽기 성능 최적화 용이 | 시스템 복잡도 증가 |
| 독립적인 확장 가능 | 최종 일관성(Eventual Consistency) 허용 필요 |
| 도메인 모델 단순화 | 개발·운영 비용 증가 |

## Related Terms

- [[Event-Driven]] — 이벤트 기반 아키텍처
- [[Domain-Driven-Design]] — DDD와 함께 자주 사용
- [[Architecture-Patterns]] — CQRS는 아키텍처 패턴 중 하나

## References

- Greg Young, "CQRS Documents" (2010) — CQRS 원저자
- Martin Fowler, "CQRS" (martinfowler.com)
