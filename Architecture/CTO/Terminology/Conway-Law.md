# Conway's Law

## Definition

> "조직이 설계하는 시스템은 그 조직의 커뮤니케이션 구조를 그대로 반영한다."
> — Melvin Conway, 1967

시스템 아키텍처는 그것을 만드는 팀의 조직 구조와 닮게 된다는 법칙. SW 엔지니어링에서 가장 자주 인용되는 관찰 중 하나다.

## 예시

| 조직 구조 | 결과 시스템 |
|---|---|
| iOS팀 / Android팀 / 백엔드팀 분리 | iOS API / Android API / 공통 API가 별도로 존재 |
| 결제팀 / 주문팀 / 배송팀 분리 | 결제 서비스 / 주문 서비스 / 배송 서비스로 분리된 마이크로서비스 |
| 단일 전체 팀 | 단일 모놀리식 애플리케이션 |

## Inverse Conway Maneuver (역 콘웨이 전략)

Conway's Law를 **의도적으로 활용**하는 전략. 원하는 시스템 아키텍처가 있다면, 먼저 그 아키텍처에 맞게 팀 구조를 바꾼다.

- 마이크로서비스 아키텍처를 원한다면 → 서비스 단위로 팀을 분리
- 도메인 경계를 명확히 하고 싶다면 → 도메인 단위로 팀 구성
- [[Engineering-Organization-Models]]의 Team Topologies 접근법의 핵심 아이디어

## CTO 관점

1. **조직 구조를 바꾸면 아키텍처가 따라온다** — 기술적 리팩토링 전에 팀 구조 재편을 먼저 고려
2. **아키텍처 목표에서 팀 설계 역산** — "우리가 원하는 아키텍처가 무엇인가?"에서 팀 구조 도출
3. **경계가 모호한 팀 → 경계가 모호한 서비스** — 팀 간 소통 문제가 시스템 통합 문제로 나타남
4. **[[Platform-Strategy]]와 연결** — Platform Team을 만들면 공통 인프라 플랫폼이 자연스럽게 생긴다

## 실무 적용 예시

```
목표: 주문·결제·배송을 독립 배포 가능한 서비스로 분리
→ 각 도메인에 독립 팀 구성 (Stream-Aligned Team)
→ 공통 인프라는 Platform Team이 제공
→ Conway's Law에 따라 시스템이 자연스럽게 서비스 경계를 가짐
```

## Related Terms

- [[Engineering-Organization-Models]] — Team Topologies에서 Conway's Law를 적극 활용
- [[Platform-Strategy]] — Platform Team 구성이 플랫폼 아키텍처를 만든다
- [[Technical-Debt]] — 잘못 설계된 팀 경계가 아키텍처 부채로 이어짐

## References

- [Conway's Law 원문](http://www.melconway.com/Home/Conways_Law.html)
- [Team Topologies — Matthew Skelton & Manuel Pais](https://teamtopologies.com/)
- [Thoughtworks — Inverse Conway Maneuver](https://www.thoughtworks.com/radar/techniques/inverse-conway-maneuver)
