# ArchiMate

> 엔터프라이즈 아키텍처 모델링 표준 언어·도구

## Overview

The Open Group이 관리하는 엔터프라이즈 아키텍처 모델링 표준 언어. Business, Application, Technology 3개 레이어로 기업 전체 IT 구조를 시각화한다.

주로 Solution Architect / CTO가 전사 아키텍처 시각화에 사용하며, Software Architect는 [[Draw-io]]나 [[Lucidchart]]를 더 자주 사용한다.

## 3개 레이어

| 레이어 | 대상 | 주요 요소 |
|---|---|---|
| **Business** | 비즈니스 프로세스·조직·기능 | Business Process, Business Role, Business Service |
| **Application** | 애플리케이션 기능·데이터 | Application Component, Application Service, Data Object |
| **Technology** | 인프라·서버·네트워크 | Node, Device, System Software, Communication Path |

## 관계 유형

| 관계 | 의미 |
|---|---|
| **Serving** | 하위 요소가 상위 요소를 지원 |
| **Realization** | 하위 요소가 상위 요소를 구현 |
| **Composition** | 포함 관계 |
| **Association** | 일반적인 연관 관계 |

## 주요 도구

| 도구 | 특징 |
|---|---|
| **Archi** | 오픈소스 ArchiMate 모델링 도구, 무료 |
| **Sparx EA** | 기업용 EA 도구, 유료, UML + ArchiMate 통합 |
| **BiZZdesign** | 클라우드 기반 EA 플랫폼 |

## Common Usage

- 전사 아키텍처(Enterprise Architecture) 문서화
- TOGAF 프레임워크와 함께 사용
- 비즈니스-IT 정렬(Business-IT Alignment) 시각화
- 여러 시스템 간의 관계를 한 장에 표현

## Tips & Shortcuts

- 레이어 간 선이 너무 복잡해지면 View를 분리해 표현
- Archi 도구에서 `Ctrl + Shift + E` → 모델 내보내기 (PNG/SVG)
- 관계를 먼저 모델링하고 뷰(다이어그램)는 나중에 생성

## References

- [The Open Group ArchiMate](https://www.opengroup.org/archimate-forum)
- [Archi Tool](https://www.archimatetool.com) — 무료 오픈소스 ArchiMate 도구
