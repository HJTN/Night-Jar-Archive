# Architecture Design Process

> 요구사항 분석 → 아키텍처 탐색 → 설계 확정 → 문서화까지의 전체 흐름

## Overview

소프트웨어 아키텍처를 처음 설계하거나 기존 시스템을 재설계할 때 따르는 프로세스. 결과물은 아키텍처 설계 문서(Architecture Design Document), C4 다이어그램 세트, [[ADR]] 세트다.

## Steps

1. **요구사항 수집** — 기능 요구사항 + NFR 정의
   - 이해관계자 인터뷰: "이 시스템이 해결해야 할 문제는?"
   - NFR 정의: 목표 성능(p95 응답시간), 가용성(SLO), 보안 요건 → [[Quality-Attributes]]
   - 시스템 규모 추정: DAU, TPS, 데이터 증가량

2. **현황 분석 (As-Is)**
   - 기존 시스템 구조 파악
   - 기술 부채, 병목, 제약 조건 파악
   - 팀 기술 역량 현황 파악

3. **아키텍처 드라이버 식별**
   - 설계에 가장 큰 영향을 미치는 핵심 요인 3~5개 선별
   - 예: "높은 쓰기 처리량", "멀티 테넌트", "엄격한 보안 격리"

4. **도메인 모델 설계** (복잡한 비즈니스 로직이 있는 경우)
   - Event Storming으로 도메인 이벤트 발굴 (Miro 활용)
   - [[Domain-Driven-Design]] Bounded Context 정의
   - Aggregate, Entity, Value Object 설계

5. **아키텍처 패턴 탐색**
   - 후보 패턴 탐색 → [[Architecture-Patterns]] 참고
   - 각 패턴의 트레이드오프 분석: Monolith vs MSA, Sync vs Async
   - NFR 충족 여부 시뮬레이션

6. **아키텍처 스케치**
   - [[Miro]]에서 화이트보드 스케치 (빠른 아이디어 탐색)
   - 컴포넌트, 인터페이스, 데이터 흐름 초안 작성

7. **주요 시나리오 워크스루**
   - 핵심 유스케이스를 설계 위에서 시뮬레이션
   - "이 요청은 어떤 컴포넌트를 거쳐 처리되는가?"
   - 병목·복잡성 사전 발견

8. **ADR 작성**
   - 주요 기술 결정(패턴 선택, 기술 스택, 통신 방식)을 [[ADR-Writing-Process]]로 문서화

9. **아키텍처 다이어그램 작성**
   - C4 Model: Context → Container → Component 순서로 작성
   - [[Draw-io]] 또는 [[Lucidchart]] 활용

10. **아키텍처 문서화**
    - Architecture Design Document 작성 → [[Architecture-Design-Document-Template]] 활용
    - [[Confluence]]에 게시

11. **아키텍처 리뷰** → [[Architecture-Review-Process]]
    - 팀원·이해관계자와 검토
    - 피드백 반영 후 확정

## Inputs

- 비즈니스 요구사항 문서 (BRD 또는 Product Spec)
- NFR 목록 (성능·가용성·보안 목표)
- 기존 시스템 현황 문서

## Outputs

- 아키텍처 설계 문서 (Architecture Design Document)
- C4 모델 다이어그램 (Context, Container, Component)
- ADR 세트 (주요 결정 기록)
- 리스크 및 미결 사항 목록

## Notes

- "완벽한" 아키텍처를 처음부터 만들려 하지 말 것 — 반복적으로 개선한다
- 설계 단계에서 구현 세부사항까지 결정하지 않음. 팀에 자율권을 남긴다
- Evolutionary Architecture: 요구사항이 바뀌면 아키텍처도 진화해야 한다
- 다이어그램이 너무 복잡하면 C4 레벨을 나눠서 표현 (Context는 경영진용, Component는 개발팀용)
