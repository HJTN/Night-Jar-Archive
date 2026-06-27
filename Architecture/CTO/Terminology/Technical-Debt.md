# Technical Debt

## Definition

단기 편의나 속도를 위해 선택한 불완전한 설계·구현이 미래에 추가 비용(수정·장애·느린 개발)으로 돌아오는 현상. Ward Cunningham이 1992년 금융 용어 "부채"에서 차용해 소프트웨어에 적용한 개념이다.

> "나중에 갚겠다는 전제로 빌린 기술적 타협. 이자(유지비용)가 계속 붙는다."

## 유형

| 유형 | 설명 | 예시 |
|---|---|---|
| **Deliberate** | 의도적 선택. 속도 우선 후 나중에 개선 | MVP를 위한 하드코딩 |
| **Accidental** | 지식 부족·실수로 발생 | 안티패턴 코드, 중복 로직 |
| **Bit Rot** | 시간 경과로 환경이 변해 낡아진 코드 | 지원 종료된 라이브러리 |
| **Architecture Debt** | 시스템 구조 자체의 문제 | 모놀리스의 과도한 결합도 |

## Context / When to Use

- CTO 관점: 기술 부채는 완전히 없앨 수 없음. 관리하고 상환 속도를 조절하는 것이 목표
- [[OKR]]의 Key Result로 부채 지표를 정량화해 비즈니스와 협상
- [[Tech-Radar]]의 Hold 항목들이 방치되면 Architecture Debt로 전환
- Sprint의 20% 룰: 매 스프린트 20%를 부채 상환에 배정하는 전략이 일반적

## 측정 지표

- **Code Coverage** — 테스트 커버리지 하락 = 부채 누적 신호
- **Cyclomatic Complexity** — 복잡도 증가 = 유지보수 비용 상승
- **Lead Time** — 기능 개발 시간이 늘어나면 부채가 쌓인 것
- **Bug Rate** — 회귀 버그 증가 = 구조적 부채 신호

## Related Terms

- [[OKR]] — 부채 해소 목표를 분기 OKR로 정량화
- [[Tech-Radar]] — Hold 기술이 방치되면 부채화
- [[Build-vs-Buy]] — 직접 개발 시 부채 리스크 vs. 외부 솔루션
- [[Engineering-Culture]] — 부채를 방치하는 문화 vs. 지속적 개선 문화

## References

- [Ward Cunningham on Technical Debt](https://wiki.c2.com/?TechnicalDebt)
- [Martin Fowler — Technical Debt Quadrant](https://martinfowler.com/bliki/TechnicalDebtQuadrant.html)
