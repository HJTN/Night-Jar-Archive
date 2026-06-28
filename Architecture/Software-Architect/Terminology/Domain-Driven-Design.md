# 도메인 주도 설계 (Domain-Driven Design, DDD)

## Definition

복잡한 비즈니스 도메인을 소프트웨어에 정확히 반영하기 위해 도메인 전문가와 개발자가 공통 언어(Ubiquitous Language)를 사용해 설계하는 방법론.

→ 상세 개념: [[Domain-Driven-Design|도메인 주도 설계 개념 문서 (Domain-Knowledge)]]

## Context / When to Use

복잡한 비즈니스 로직이 있는 핵심 시스템. 도메인 전문가와 긴밀한 협업이 필요한 경우.

## 핵심 개념 요약

| 개념 | 설명 |
|---|---|
| **Ubiquitous Language** | 도메인 전문가와 개발자가 공유하는 공통 용어 |
| **Bounded Context** | 단일 도메인 모델이 유효한 경계 |
| **Aggregate** | 트랜잭션 일관성의 경계 단위 |
| **Entity** | 고유 식별자를 가진 도메인 객체 |
| **Value Object** | 식별자 없이 값으로 정의되는 불변 객체 |
| **Domain Event** | 도메인에서 발생한 중요한 사건 |
| **Repository** | Aggregate 저장·조회 인터페이스 |

## 전략적 설계 (Strategic Design)

- **Bounded Context 식별**: 팀·데이터·언어 경계 정의
- **Context Map**: Bounded Context 간의 관계 매핑 (Upstream/Downstream)
- **Event Storming**: 도메인 이벤트 발굴 워크숍 ([[Miro]] 활용)

## 전술적 설계 (Tactical Design)

- Aggregate, Entity, Value Object, Domain Service, Repository 구현
- [[Clean-Architecture]]나 Hexagonal Architecture와 함께 적용

## Related Terms

- [[CQRS]] — DDD와 시너지 높은 패턴
- [[Event-Driven]] — Domain Event 발행·구독
- [[Clean-Architecture]] — 함께 자주 적용
- [[Architecture-Patterns]] — 아키텍처 패턴

## References

- Eric Evans, "Domain-Driven Design" (2003) — DDD 원저서
- Vaughn Vernon, "Implementing Domain-Driven Design" (2013)
