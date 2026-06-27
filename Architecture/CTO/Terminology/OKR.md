# OKR (Objectives and Key Results)

## Definition

목표(Objective)와 측정 가능한 핵심 결과(Key Results)로 성과를 관리하는 목표 설정 프레임워크. Intel의 Andy Grove가 창안하고 Google이 전사 도입하면서 실리콘밸리 표준으로 자리잡았다.

- **Objective** — 정성적 방향. "무엇을 달성할 것인가" (예: 엔지니어링 생산성을 획기적으로 높인다)
- **Key Result** — 정량적 지표. "달성했음을 어떻게 알 수 있는가" (예: 배포 리드타임을 5일 → 1일로 단축)

## Context / When to Use

- **분기(Q) 단위** — 팀·개인 OKR 설정 및 중간 점검
- **연간** — 회사 전략과 정렬된 기술 조직 OKR 수립
- CTO는 회사 OKR → 엔지니어링 OKR → 팀 OKR로 계단식 정렬(Cascade)을 책임진다
- [[Technical-Debt]] 해소, 인프라 안정성, 개발자 경험 개선 등 기술 과제를 OKR화하면 비즈니스 우선순위와 협상하기 쉬워진다

## Key Principles

| 원칙 | 설명 |
|---|---|
| Ambitious | KR 달성률 70%가 성공. 100%면 목표가 너무 쉬움 |
| Measurable | 숫자로 측정 불가한 KR은 OKR이 아님 |
| Time-bound | 반드시 기간이 명확해야 함 |
| Transparent | 전사 공개가 원칙. 정렬·협업 촉진 |

## Example (CTO 관점)

```
Objective: 개발자 경험을 업계 최고 수준으로 끌어올린다
  KR1: 배포 빈도 주 1회 → 일 3회
  KR2: CI 빌드 시간 20분 → 5분 이하
  KR3: 개발자 만족도(eNPS) 30점 → 50점
```

## Related Terms

- [[Tech-Radar]] — OKR에서 기술 도입 목표를 설정할 때 Tech Radar를 기준으로 삼음
- [[Technical-Debt]] — 기술 부채 해소를 OKR Key Result로 정량화
- [[Engineering-Culture]] — 문화 개선 목표를 OKR로 추적
- [[Quarterly-Review-Checklist]] — 분기 OKR 점검 체크리스트

## References

- [Measure What Matters — John Doerr](https://www.whatmatters.com/)
- [Google re:Work — OKR Guide](https://rework.withgoogle.com/guides/set-goals-with-okrs/)
