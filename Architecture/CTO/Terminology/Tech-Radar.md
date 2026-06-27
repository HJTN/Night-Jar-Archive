# Tech Radar

## Definition

조직이 사용하거나 평가 중인 기술을 시각화하고, 각 기술의 채택 권장 수준을 나타내는 전략 도구. ThoughtWorks가 내부 기술 평가 목적으로 개발해 공개한 이후 업계 표준 프레임워크로 자리잡았다.

## 구조: 4 Quadrants × 4 Rings

**Quadrants (기술 분류)**
| 사분면 | 설명 |
|---|---|
| Techniques | 개발 방법론·프로세스·패턴 (예: GitOps, Trunk-Based Development) |
| Tools | 소프트웨어 도구 (예: Playwright, Terraform) |
| Platforms | 인프라·플랫폼 (예: Kubernetes, AWS Lambda) |
| Languages & Frameworks | 언어·프레임워크 (예: Rust, Next.js) |

**Rings (채택 단계)**
| 링 | 의미 |
|---|---|
| **Adopt** | 프로덕션 사용 권장. 조직 표준 |
| **Trial** | 프로젝트에 시험 적용 권장 |
| **Assess** | 가능성 탐색. 파일럿 또는 리서치 단계 |
| **Hold** | 신규 도입 중단. 기존 사용은 유지 |

## Context / When to Use

- 연 2회 Tech Radar를 발행해 기술 방향성을 전사 공유
- [[Build-vs-Buy]] 의사결정 시 Radar를 기준으로 검토
- 신규 기술 제안이 들어올 때 어느 Ring에 배치할지 논의의 출발점으로 활용
- 개발팀이 기술 선택 시 Radar 범위 내에서 자율적으로 결정하도록 가이드

## Related Terms

- [[OKR]] — 기술 도입 목표를 OKR Key Result로 연결
- [[Build-vs-Buy]] — 도구·플랫폼 평가 시 Radar와 연계
- [[Technical-Debt]] — Hold 상태 기술이 방치되면 기술 부채화
- [[Platform-Strategy]] — 플랫폼 사분면이 Platform Strategy와 직접 연결
- [[Tech-Radar-Review-Process]] — Radar 갱신 절차 워크플로우

## References

- [ThoughtWorks Technology Radar](https://www.thoughtworks.com/radar)
- [Build Your Own Tech Radar](https://www.thoughtworks.com/insights/blog/technology-strategy/five-ways-a-technology-radar-can-help-your-enterprise-navigate-tech)
