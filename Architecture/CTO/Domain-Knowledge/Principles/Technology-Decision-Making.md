# Technology Decision Making

> CTO가 기술 의사결정 시 적용하는 프레임워크와 원칙

## 의사결정 유형별 접근

### Type 1: 되돌리기 어려운 결정 (One-Way Door)
- 예: 핵심 플랫폼 전환, 주요 벤더 계약, 아키텍처 패러다임 전환
- **신중하게**: 충분한 데이터·전문가 의견·PoC 후 결정
- CTO가 직접 최종 결정권 행사

### Type 2: 되돌릴 수 있는 결정 (Two-Way Door)
- 예: 라이브러리 선택, 팀 내 프로세스, 도구 시험 도입
- **빠르게**: 팀에 위임해 실험하고 학습
- [[Tech-Radar]]의 Trial 단계가 이에 해당

## 의사결정 프레임워크

### RFC (Request for Comments)
- 중요한 기술 결정을 문서로 제안 → 팀 피드백 수렴 → 결정
- [[Confluence]]에 RFC 문서 게시. 일정 기간(1~2주) 코멘트 수렴
- 투명성 확보 + 집단 지성 활용

### ADR (Architecture Decision Record)
- 결정 사항·배경·대안·결과를 기록
- "왜 이 결정을 했는가"를 미래 팀원이 이해할 수 있게 보존
- [[Technical-Debt]] 발생 시 ADR이 맥락 제공

### DACI / RACI
- **Driver**: 결정을 진행시키는 사람
- **Approver**: 최종 결정권자 (보통 CTO)
- **Contributor**: 인풋을 제공하는 사람
- **Informed**: 결과를 통보받는 사람

## 기술 선택 원칙

1. **Boring Technology 우선** — 검증된 기술이 혁신적 기술보다 위험이 낮다 (Dan McKinley)
2. **기술 이종성 최소화** — 스택이 다양할수록 운영 복잡도 증가
3. **커뮤니티 크기** — 생태계가 큰 기술이 장기적으로 안전
4. **탈출 전략** — 도입 전에 "언젠가 이걸 버려야 할 때 어떻게 할 것인가?" 고려

## Related Terms

- [[Build-vs-Buy]] — 가장 빈번한 기술 의사결정 유형
- [[Tech-Radar]] — 기술 선택의 조직 표준 제공
- [[Technical-Debt]] — 잘못된 결정의 결과가 부채로 누적
- [[Tech-Evaluation-Checklist]] — 체계적 평가 도구

## References

- [Choose Boring Technology — Dan McKinley](https://mcfunley.com/choose-boring-technology)
- [ADR Tools — GitHub](https://github.com/npryce/adr-tools)
