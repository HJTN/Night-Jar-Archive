# Engineering Culture

## Definition

엔지니어링 조직 내에서 공유되는 가치관·행동 양식·협업 방식·학습 태도의 총체. 코드나 프로세스보다 오래 살아남으며, 채용·의사결정·제품 품질에 직접적인 영향을 미친다.

> "Culture eats strategy for breakfast." — Peter Drucker

## 핵심 구성 요소

| 요소 | 설명 |
|---|---|
| **Psychological Safety** | 실패와 반론을 두려워하지 않는 환경 (Google Project Aristotle) |
| **Continuous Learning** | 포스트모템·Tech Talk·스터디 등 학습 문화 |
| **Ownership** | 설계·구현·운영까지 팀이 책임지는 You Build It, You Run It |
| **Transparency** | 의사결정 근거와 회사 방향을 공개. [[OKR]] 전사 공유 |
| **Blameless Culture** | 개인 잘못이 아닌 시스템·프로세스 개선 지향 |
| **Developer Experience** | 빌드·배포·피드백 루프 최적화. 생산성 투자 |

## CTO의 역할

- 문화는 **CTO가 보여주는 행동**이 곧 모델이 된다 (Top-down)
- 채용 기준에 문화 적합성 포함 → [[Engineering-Hiring-Process]] 참고
- [[Technical-Debt]]을 방치하는 문화 vs. 지속적으로 개선하는 문화를 선택하는 것은 CTO 결정
- [[OKR]]을 통해 문화 지표(eNPS, 이직률, 배포 빈도)를 정량 추적

## 문화 측정 지표

- **eNPS (Employee Net Promoter Score)** — 엔지니어 만족도 지표
- **DORA Metrics** — 배포 빈도, 리드타임, 변경 실패율, 복구 시간
- **이직률 / 재직 기간** — 문화 건강도의 간접 지표
- **심리적 안전감 설문** — Google re:Work 설문 기반

## Context / When to Use

- 새 조직 합류 시 첫 90일 문화 진단
- 팀 성과 저하·이직 증가 시 문화 요인 점검
- M&A 통합 시 문화 충돌 리스크 평가

## Related Terms

- [[OKR]] — 문화 지표를 OKR Key Result로 추적
- [[Technical-Debt]] — 부채 허용 수준이 문화를 반영
- [[Engineering-Hiring-Process]] — 채용 과정에서 문화를 전달하고 평가
- [[Platform-Strategy]] — Developer Experience가 내부 문화와 연결

## References

- [Google Project Aristotle](https://rework.withgoogle.com/print/guides/5721312655835136/)
- [DORA State of DevOps Report](https://dora.dev/research/)
