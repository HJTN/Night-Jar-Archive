# Platform Strategy

## Definition

제품·서비스·인프라를 외부 참여자(개발자, 파트너, 고객)가 그 위에서 가치를 창출할 수 있는 **플랫폼**으로 발전시키는 기술·비즈니스 전략. 내부적으로는 개발팀이 공통 인프라를 활용해 생산성을 높이는 **Internal Platform**과, 외부를 향한 **Product Platform** 두 가지 맥락이 있다.

## 두 가지 맥락

### 1. Internal Developer Platform (IDP)
- 개발팀이 인프라를 직접 관리하지 않고 셀프서비스로 배포·운영할 수 있는 내부 플랫폼
- [[Build-vs-Buy]]: Backstage 같은 오픈소스 도입 vs. 자체 구축
- 목표: Golden Path 제공 → 개발자 생산성 향상, [[Engineering-Culture]] 개선

### 2. Product Platform (외부 플랫폼)
- API·SDK를 공개해 서드파티가 제품 위에서 서비스를 만들도록 허용
- 네트워크 효과를 통한 생태계 구성
- 예: Stripe API, Twilio, AWS

## 플랫폼 전략 수립 체크포인트

1. **핵심 기능은 무엇인가?** — 플랫폼의 고유 가치를 명확히 정의
2. **누가 플랫폼 위에서 무엇을 만드는가?** — 내부 팀 vs. 외부 파트너
3. **거버넌스는 어떻게 할 것인가?** — API 정책, 버전 관리, 지원 범위
4. **수익화 또는 내부 가치 측정은?** — 외부: 과금 모델 / 내부: 생산성 지표

## Context / When to Use

- 스케일업 단계에서 여러 팀이 공통 인프라를 공유하기 시작할 때
- 제품을 B2B SaaS → API 플랫폼으로 전환 검토 시
- [[Tech-Radar]]의 플랫폼 사분면 구성 시 전략적 방향 수립

## Related Terms

- [[Build-vs-Buy]] — 플랫폼을 직접 구축할지 외부 솔루션을 조합할지
- [[Tech-Radar]] — 플랫폼 후보 기술들의 채택 수준 관리
- [[Engineering-Culture]] — 내부 플랫폼은 Developer Experience 문화와 연결
- [[Technology-Strategy-Planning]] — 플랫폼 전략이 기술 로드맵의 핵심 축

## References

- [Platform Engineering — CNCF](https://tag-app-delivery.cncf.io/whitepapers/platforms/)
- [Team Topologies — Matthew Skelton & Manuel Pais](https://teamtopologies.com/)
