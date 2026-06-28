# SOLID 원칙

## Definition

객체 지향 설계의 5가지 핵심 원칙. 유지보수·확장·테스트가 쉬운 코드를 만들기 위한 가이드라인.

Robert C. Martin(Uncle Bob)이 정리했으며, 소프트웨어 아키텍처 수준에서도 동일하게 적용된다.

## Context / When to Use

모듈·클래스·서비스 설계 시 항상 점검해야 할 원칙. 코드 리뷰 및 아키텍처 리뷰 기준으로 활용.

## 5가지 원칙

| 약자 | 원칙 | 핵심 |
|---|---|---|
| **S** | Single Responsibility Principle (단일 책임) | 한 클래스는 하나의 책임만 가진다 |
| **O** | Open/Closed Principle (개방-폐쇄) | 확장에는 열려있고, 수정에는 닫혀있다 |
| **L** | Liskov Substitution Principle (리스코프 치환) | 서브타입은 상위 타입을 대체할 수 있어야 한다 |
| **I** | Interface Segregation Principle (인터페이스 분리) | 클라이언트는 불필요한 인터페이스에 의존하지 않는다 |
| **D** | Dependency Inversion Principle (의존성 역전) | 추상화에 의존하고, 구체화에 의존하지 않는다 |

## 각 원칙 상세

### S — 단일 책임 원칙 (SRP)
- 한 모듈이 변경되는 이유는 하나여야 한다
- 높은 [[Cohesion|응집도]]와 동일한 개념
- 예: User 클래스가 인증·프로필·알림을 모두 처리하면 SRP 위반

### O — 개방-폐쇄 원칙 (OCP)
- 새로운 기능은 기존 코드 수정 없이 추가되어야 한다
- 상속·인터페이스·전략 패턴으로 구현
- 예: 새 결제 수단 추가 시 기존 결제 코드를 수정하지 않음

### L — 리스코프 치환 원칙 (LSP)
- 부모 클래스를 자식 클래스로 교체해도 프로그램이 올바르게 동작해야 한다
- 잘못된 상속 계층 구조를 막는 원칙
- 반례: `Square extends Rectangle` (너비와 높이가 독립적이지 않아 LSP 위반)

### I — 인터페이스 분리 원칙 (ISP)
- 큰 인터페이스는 목적별로 작은 인터페이스로 분리
- 구현체가 사용하지 않는 메서드를 강제로 구현하지 않도록
- 예: Printer 인터페이스를 `print()` / `scan()` / `fax()`로 분리

### D — 의존성 역전 원칙 (DIP)
- 고수준 모듈이 저수준 모듈에 직접 의존하면 안 됨
- 추상화(인터페이스)를 통해 의존 → 낮은 [[Coupling|결합도]]
- 의존성 주입(DI)으로 구현

## 아키텍처에서의 SOLID

SOLID는 클래스 설계에서 시작했지만, 컴포넌트·서비스 수준에서도 동일하게 적용된다:

| 원칙 | 아키텍처 적용 |
|---|---|
| SRP | 마이크로서비스의 단일 책임 서비스 |
| OCP | Plugin 아키텍처, 확장 가능한 API 설계 |
| LSP | 인터페이스 계약을 지키는 API 설계 |
| ISP | 세분화된 API 엔드포인트, BFF 패턴 |
| DIP | Hexagonal Architecture의 Port & Adapter |

## Related Terms

- [[Cohesion]] — SRP와 직결
- [[Coupling]] — DIP로 낮추기
- [[Clean-Architecture]] — SOLID를 아키텍처 수준으로 확장

## References

- Robert C. Martin, "Clean Architecture" (2017)
- Robert C. Martin, "Agile Software Development" (2002)
