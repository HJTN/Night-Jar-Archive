# ADR (Architecture Decision Record)

## Definition

중요한 아키텍처 결정과 그 배경·대안·결과를 기록하는 경량 문서.

"왜 이 결정을 했는가"를 미래 팀원도 이해할 수 있도록 보존하며, 동일한 논쟁의 반복을 막는다.

## Context / When to Use

- 되돌리기 어려운(One-Way Door) 기술 결정을 내릴 때
- 팀이 반복적으로 같은 질문을 할 때
- 신규 팀원이 현재 구조를 이해하기 어려울 때
- 기술 스택·아키텍처 패턴·통신 방식을 선택할 때

## ADR 구조

| 섹션 | 내용 |
|---|---|
| **Title** | 결정 사항을 한 줄로 요약 |
| **Status** | Proposed / Accepted / Superseded / Deprecated |
| **Context** | 이 결정이 필요한 배경과 제약 |
| **Decision** | 선택한 방향을 한 문장으로 |
| **Rationale** | 선택 이유 및 채택하지 않은 대안과 그 이유 |
| **Consequences** | 긍정적 영향, 부정적 영향, 새로운 제약 |

## ADR 상태 라이프사이클

```
Proposed → Accepted → Superseded by ADR-XXXX
                    ↘ Deprecated
```

## 주의사항

- ADR은 작성 후 내용을 수정하지 않는다. 번복 시 새 ADR을 작성하고 이전 ADR을 Superseded로 표기
- 모든 결정이 ADR 대상은 아님 — 되돌리기 어렵거나 팀 전체에 영향을 주는 결정에 집중
- Git에 저장 시 코드와 결정 이력이 함께 관리되어 PR과 연결 가능

## Related Terms

- [[ADR-Writing-Process]] — ADR 작성 절차
- [[Architecture-Decision-Making]] — 결정 방법론
- [[Design-Decision-Checklist]] — 결정 전 점검 항목

## References

- Michael Nygard, "Documenting Architecture Decisions" (2011) — 원조 ADR 포맷
- [ADR GitHub Organization](https://adr.github.io)
