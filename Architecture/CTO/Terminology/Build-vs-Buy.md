# Build vs Buy

## Definition

필요한 기능이나 시스템을 **직접 개발(Build)** 할지, **외부 솔루션을 구매·도입(Buy)** 할지 결정하는 전략적 판단. CTO가 가장 빈번하게 직면하는 의사결정 유형 중 하나다. "Buy"는 SaaS 구독, 오픈소스 도입, SI 외주 등을 모두 포함한다.

## 의사결정 프레임워크

| 기준 | Build 유리 | Buy 유리 |
|---|---|---|
| 핵심 경쟁력 | 차별화 핵심 기능 | 범용 기능 (이메일, 결제 등) |
| 개발 역량 | 내부 전문가 보유 | 역량 부족·채용 어려움 |
| 시간 | 장기 전략 투자 | 빠른 출시(Time-to-Market) 필요 |
| 비용 | 장기 TCO 절감 | 초기 비용 최소화 |
| 커스터마이징 | 높은 맞춤화 필요 | 표준 기능으로 충분 |
| 벤더 리스크 | 종속 회피 필요 | 벤더 생태계 활용 가능 |

## CTO 관점 체크포인트

1. **이것이 우리의 핵심 경쟁력인가?** → Yes면 Build 우선 검토
2. **시장에 충분히 성숙한 솔루션이 있는가?** → Yes면 Buy 우선 검토
3. **벤더 종속(Vendor Lock-in) 리스크는 감수 가능한가?**
4. **Buy 후 마이그레이션이 필요해질 경우 탈출 비용은?**
5. **내부 팀이 Build를 장기 유지보수할 여력이 있는가?**

## Context / When to Use

- 새로운 기능 또는 시스템 도입 시 항상 먼저 검토
- [[Tech-Radar]]의 Tools·Platforms 사분면 평가 시 Build vs Buy 관점 포함
- [[Technical-Debt]] 관점: Buy는 단기 빠르나 장기 커스터마이징 부채 발생 가능
- [[Tech-Evaluation-Checklist]] 참고해 체계적으로 평가

## Related Terms

- [[Tech-Radar]] — Buy 후보 기술을 Radar에 배치해 채택 수준 결정
- [[Technical-Debt]] — Build 선택 시 장기 유지 부채 리스크
- [[Platform-Strategy]] — 플랫폼을 Build할지 Buy할지가 핵심 전략 결정
- [[Tech-Evaluation-Checklist]] — 평가 기준 체크리스트

## References

- [Thoughtworks — Build vs Buy](https://www.thoughtworks.com/)
- [CTO Craft Community](https://ctocraft.com/)
