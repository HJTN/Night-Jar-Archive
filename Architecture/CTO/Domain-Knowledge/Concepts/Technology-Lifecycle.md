# Technology Lifecycle

> 기술이 등장해서 성숙하고 쇠퇴하는 과정을 이해하는 프레임워크

## Gartner Hype Cycle

기술의 기대치 변화를 5단계로 모델화:

```
기대치
  ↑
  │    ② Peak of Inflated Expectations
  │   /\
  │  /  \  ③ Trough of Disillusionment
  │ /    \/____________________
  │/  ① Innovation    ④ Slope of    ⑤ Plateau of
  │   Trigger        Enlightenment  Productivity
  └──────────────────────────────────────────► 시간
```

| 단계 | 설명 | CTO 행동 |
|---|---|---|
| ① Innovation Trigger | 기술 등장. 관심 시작 | Assess 배치 → [[Tech-Radar]] |
| ② Peak | 과대 기대. 미디어 과열 | 냉정한 평가. 파일럿 신중하게 |
| ③ Trough | 실망. 실패 사례 부각 | 진짜 가능성 재평가 기회 |
| ④ Slope | 실용 사례 축적. 방법론 성숙 | Trial → Adopt 검토 |
| ⑤ Plateau | 주류 채택. 안정화 | Adopt 배치. 표준화 |

## 실무 적용

- AI/LLM: 현재 ②~③ 구간. 과열된 기대와 현실 사이에서 신중한 도입 필요
- Kubernetes: ⑤ 구간. 대부분 조직에서 Adopt
- Quantum Computing: ① 구간. CTO는 Assess에 배치하되 투자 최소화

## Related Terms

- [[Tech-Radar]] — Hype Cycle 위치를 참고해 Ring 배치 결정
- [[Build-vs-Buy]] — 성숙 단계에 따라 외부 솔루션 성숙도 판단
- [[Technical-Debt]] — 쇠퇴기 기술을 계속 사용하면 부채 증가

## References

- [Gartner Hype Cycle](https://www.gartner.com/en/research/methodologies/gartner-hype-cycle)
