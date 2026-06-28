# Miro (Software Architect 관점)

> 온라인 화이트보드·워크숍 협업 도구

## Overview

클라우드 기반 온라인 화이트보드 플랫폼. 소프트웨어 아키텍트에게는 **Event Storming**, 아키텍처 스케치, 팀 브레인스토밍에 특히 유용하다.

## Architecture 작업에서의 주요 활용

| 활용 | 설명 |
|---|---|
| **Event Storming** | [[Domain-Driven-Design]] 도메인 이벤트 발굴 워크숍 |
| **아키텍처 스케치** | 초기 아이디어 빠른 시각화 (정식 다이어그램 전 단계) |
| **시스템 컨텍스트 탐색** | C4 Context 레벨 초안 작성 |
| **의존성 매핑** | 서비스 간 의존 관계 시각화 |
| **아키텍처 리뷰 워크숍** | 원격 팀과 함께 리뷰 진행 |

## Event Storming 스티커 색상 규칙

| 색상 | 의미 |
|---|---|
| 주황 | Domain Event (과거형으로 기술, 예: "주문이 생성됨") |
| 파랑 | Command (이벤트를 발생시키는 명령) |
| 노랑 | Aggregate (명령과 이벤트를 처리하는 도메인 객체) |
| 보라 | Policy (이벤트가 발생하면 실행되는 비즈니스 규칙) |
| 분홍 | External System (외부 시스템) |
| 초록 | Read Model (UI가 읽는 뷰) |

## vs 다른 도구 비교

| 상황 | 추천 도구 |
|---|---|
| 빠른 아이디어 스케치, Event Storming | **Miro** |
| 정식 C4 다이어그램, Git 저장 | [[Draw-io]] |
| 팀 협업 아키텍처 다이어그램 | [[Lucidchart]] |
| 엔터프라이즈 아키텍처 모델링 | [[ArchiMate]] |

## Tips & Shortcuts

- `Ctrl + /` — 단축키 목록 보기
- `S` — 스티커 노트 추가
- `T` — 텍스트 추가
- `F` — 프레임 추가 (영역 구분)
- 더블클릭 → 새 스티커 바로 생성
- `Ctrl + Shift + H` — 선택 요소 가운데 정렬

## References

- [Miro](https://miro.com)
- [Event Storming Guide](https://www.eventstorming.com) — Alberto Brandolini
