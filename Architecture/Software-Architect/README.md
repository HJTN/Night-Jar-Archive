# Software Architect

> 시스템 구조 설계, 기술 결정, 아키텍처 문서화의 책임자

## Overview

Software Architect는 소프트웨어 시스템의 구조적 청사진을 설계하고 기술 결정을 내리는 역할이다. 개발팀이 올바른 방향으로 구현할 수 있도록 아키텍처 원칙·패턴·가이드라인을 제시하며, 비즈니스 요구사항을 기술 구조로 변환하는 브리지 역할을 한다.

**Software Architect vs CTO:**
- **Software Architect** — 특정 시스템·제품의 기술 구조 설계에 집중. 코드·설계 레벨에 더 가까움
- **CTO** — 조직 전체의 기술 전략·방향·투자 결정. 비즈니스 레벨에 더 가까움

## Key Responsibilities

- **아키텍처 설계** — 시스템 컴포넌트, 인터페이스, 데이터 흐름, 경계 정의
- **[[ADR]] 작성** — 주요 기술 결정과 그 배경·대안·결과 문서화
- **[[Architecture-Review-Process|아키텍처 리뷰]] 주도** — 설계가 요구사항과 품질 기준을 충족하는지 검토
- **NFR 정의** — 성능·가용성·보안·확장성 등 비기능 요구사항 정의 및 검증 → [[Quality-Attributes]]
- **개발팀 기술 가이드** — 코딩 표준, 패턴 적용 지침, 기술 부채 방향 제시
- **[[Domain-Driven-Design|도메인 모델 설계]]** — Bounded Context, Aggregate, Entity 정의
- **기술 트레이드오프 분석** — 대안 탐색 및 장단점 비교

## Core Skills

| 영역 | 핵심 역량 |
|---|---|
| **아키텍처 패턴** | MSA, Event-Driven, CQRS, Layered, Clean Architecture |
| **설계 원칙** | [[SOLID]], [[Cohesion]], [[Coupling]], DRY, YAGNI |
| **도메인 설계** | [[Domain-Driven-Design]], Bounded Context, Aggregate |
| **UML & 다이어그램** | C4 Model, 시퀀스·컴포넌트·클래스 다이어그램 |
| **품질 속성** | [[Quality-Attributes]], NFR 정의, SLO 설정 |
| **커뮤니케이션** | 기술 개념을 비기술 이해관계자에게 설명 |

## Core Skills & Tools

**주요 도구** → [[Draw-io]], [[Lucidchart]], [[PlantUML]], [[ArchiMate]], [[Miro]], [[Confluence]]

## Related Notes

### 도메인 지식
- [[Architecture-Patterns]] — 주요 아키텍처 패턴 (MSA, Event-Driven, CQRS 등)
- [[Domain-Driven-Design]] — 도메인 모델 중심 설계 방법론
- [[Architecture-Decision-Making]] — 아키텍처 의사결정 프레임워크
- [[Clean-Architecture]] — 비즈니스 로직을 외부로부터 격리하는 설계 패턴
- [[Quality-Attributes]] — 성능·가용성·보안 등 품질 속성 목록

### 용어
- [[ADR]] · [[SOLID]] · [[Cohesion]] · [[Coupling]]
- [[CQRS]] · [[Event-Driven]] · [[Domain-Driven-Design]]

### 워크플로우
- [[Architecture-Design-Process]] — 요구사항 분석부터 아키텍처 완성까지
- [[ADR-Writing-Process]] — 기술 결정 문서화 절차
- [[Architecture-Review-Process]] — 설계 검토 프로세스

### 체크리스트
- [[Architecture-Review-Checklist]] — 품질 속성별 리뷰 항목
- [[Design-Decision-Checklist]] — 설계 결정 전 점검 항목

### 템플릿
- [[ADR-Template]] — ADR 작성 템플릿
- [[Architecture-Design-Document-Template]] — 아키텍처 설계 문서 템플릿

### 종합 가이드
- [[Software-Architect-Guide]] — 도메인 지식·업무·도구 전체 요약
