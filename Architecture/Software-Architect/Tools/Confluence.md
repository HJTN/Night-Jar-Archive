# Confluence (Software Architect 관점)

> Atlassian의 팀 위키·문서 협업 플랫폼

## Overview

아키텍처 문서·[[ADR]]·리뷰 결과를 팀 전체가 접근 가능한 형태로 관리하는 **지식 저장소** 역할. Software Architect에게는 설계 산출물을 체계적으로 관리하고 공유하는 핵심 도구다.

## Architecture 작업에서의 주요 활용

| 활용 | 내용 |
|---|---|
| **ADR 저장** | Architecture Decision Record 체계적 관리 |
| **아키텍처 문서** | ADD(Architecture Design Document) 게시 |
| **리뷰 결과** | [[Architecture-Review-Process]] 결과 및 액션 아이템 기록 |
| **온보딩 자료** | 신규 팀원을 위한 시스템 구조 설명 문서 |
| **다이어그램 임베드** | [[Draw-io]] / [[Lucidchart]] 다이어그램 직접 삽입 |

## Key Features

| 기능 | 설명 |
|---|---|
| **Space** | 팀·프로젝트별 독립된 위키 공간 |
| **Page Templates** | ADR 템플릿, 아키텍처 문서 템플릿 적용 |
| **Macro** | 목차 자동 생성, Jira 이슈 인라인 삽입 |
| **Page Tree** | 계층적 문서 구조로 관련 ADR 묶기 |
| **@mention** | 리뷰어에게 직접 알림 전송 |

## Jira 연동

- Confluence 페이지에서 Jira 이슈 직접 생성
- 아키텍처 리뷰 액션 아이템을 Jira 이슈로 등록
- Jira Epic ↔ Confluence 아키텍처 문서 양방향 링크

## Tips & Shortcuts

- `Ctrl + K` — 페이지 링크 삽입
- `/draw.io` — 다이어그램 블록 삽입
- `/table` — 표 삽입
- 페이지 감시(Watch) 설정 → 변경 시 이메일 알림
- 페이지 레이블(Label)로 ADR Space 분류

## References

- [Atlassian Confluence](https://www.atlassian.com/software/confluence)
