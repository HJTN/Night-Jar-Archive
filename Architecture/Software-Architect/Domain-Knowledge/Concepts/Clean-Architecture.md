# 클린 아키텍처 (Clean Architecture)

## Definition

Robert C. Martin(Uncle Bob)이 제안한 아키텍처 패턴. 비즈니스 규칙을 기술 세부사항(DB, 프레임워크, UI)으로부터 분리해 독립적으로 테스트·교체 가능하게 만드는 설계 원칙.

**핵심 규칙: 의존성은 항상 안쪽(도메인)을 향한다.**

## 4개 레이어

```
외부 (변경 잦음)
┌─────────────────────────────────────────────┐
│  Frameworks & Drivers                        │  DB, Web Framework, UI
│  ┌───────────────────────────────────────┐  │
│  │  Interface Adapters                   │  │  Controller, Presenter, Gateway
│  │  ┌───────────────────────────────┐   │  │
│  │  │  Application Business Rules  │   │  │  Use Cases
│  │  │  ┌───────────────────────┐  │   │  │
│  │  │  │  Enterprise Business  │  │   │  │  Entities (Domain)
│  │  │  │       Rules           │  │   │  │
│  │  │  └───────────────────────┘  │   │  │
│  │  └───────────────────────────────┘   │  │
│  └───────────────────────────────────────┘  │
└─────────────────────────────────────────────┘
내부 (변경 적음)
```

## 레이어별 역할

| 레이어 | 내용 | 예시 |
|---|---|---|
| **Entities** | 핵심 비즈니스 규칙 (도메인 객체) | Order, User, Payment |
| **Use Cases** | 애플리케이션 비즈니스 규칙 | CreateOrder, ProcessPayment |
| **Interface Adapters** | 외부와 내부 간 변환 | Controller, Presenter, Gateway |
| **Frameworks & Drivers** | DB, 웹 프레임워크, UI | Spring, MySQL, React |

## 의존성 규칙 (Dependency Rule)

- 외부 레이어는 내부 레이어에 의존 가능
- **내부 레이어는 외부 레이어를 알면 안 됨**
- Entity는 Use Case를 모름. Use Case는 Controller를 모름
- 방향이 역전되어야 할 때 → DIP([[SOLID]])로 해결

## Hexagonal Architecture와의 관계

Clean Architecture와 Hexagonal Architecture(Port & Adapter)는 같은 원칙을 다른 이름으로:

| 개념 | Clean Architecture | Hexagonal Architecture |
|---|---|---|
| 내부 | Entities + Use Cases | Domain (Core) |
| 외부 연결부 | Interface Adapters | Adapter |
| 추상화 경계 | Gateway Interface | Port |

## 장단점

| 장점 | 단점 |
|---|---|
| 프레임워크 독립 (교체 가능) | 레이어 수가 많아 초기 복잡도 높음 |
| DB 없이 Use Case 단위 테스트 가능 | 단순 CRUD에는 과도한 구조 |
| 비즈니스 규칙의 긴 생존성 | 팀 합의 없으면 레이어 경계 흐트러짐 |

## 언제 사용하는가

✅ 복잡한 비즈니스 도메인이 있는 시스템
✅ 장기 유지보수가 중요한 핵심 서비스
✅ [[Domain-Driven-Design]]과 함께 적용
❌ 단순 CRUD API, 스크립트 수준의 서비스

## Related Concepts

- [[SOLID]] — Clean Architecture의 기반 원칙
- [[Domain-Driven-Design]] — 함께 자주 적용
- [[Coupling]] — 낮은 결합도를 구조적으로 강제
- [[Architecture-Patterns]] — 아키텍처 패턴

## References

- Robert C. Martin, "Clean Architecture" (2017)
