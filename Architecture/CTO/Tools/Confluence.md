# Confluence

> Atlassian의 팀 위키·기술 문서 협업 플랫폼

## Overview

Confluence는 Atlassian이 만든 팀 위키 및 문서 관리 플랫폼이다. [[Jira]]와 네이티브 통합이 강력하며, 대규모 엔지니어링 조직에서 기술 문서·설계 문서·의사결정 기록을 중앙 관리하는 데 표준으로 사용된다.

## Key Features

- **Space** — 팀·프로젝트·도메인별 문서 공간 분리
- **Page Templates** — 회의록·기술 스펙·ADR·포스트모템 등 표준 템플릿 제공
- **Jira 연동** — 이슈·스프린트·에픽을 Confluence 페이지에 임베드
- **Macro** — 동적 콘텐츠 삽입 (Table of Contents, Status, Roadmap 등)
- **Page History** — 모든 편집 이력 추적 및 버전 비교
- **권한 관리** — Space·Page 단위 세밀한 접근 제어

## CTO 활용 시나리오

| 용도 | 방법 |
|---|---|
| 기술 전략 문서 | Space: Engineering Strategy → Page 계층 구조 |
| ADR (Architecture Decision Record) | 표준 ADR 템플릿으로 의사결정 기록 |
| [[Tech-Radar]] 발행 | Radar 결과물을 Confluence에 게시 + [[Jira]] 링크 |
| 포스트모템 | 장애 분석 문서 표준화·팀 공유 |
| 온보딩 위키 | 신규 입사자용 Getting Started 가이드 |

## Tips & Shortcuts

- `e` — 현재 페이지 편집 모드 진입
- `/` — 매크로·요소 삽입 메뉴
- **라벨(Label)** — 페이지에 태그 붙여 크로스-스페이스 검색 용이
- **Page Tree 정렬** — 중요 문서를 상단 고정해 탐색 편의성 향상
- [[Notion]]과 비교: Confluence는 [[Jira]] 연동·권한 관리가 강점, Notion은 유연성이 강점

## Related Tools

- [[Jira]] — 이슈·스프린트와 문서를 연결하는 Atlassian 생태계
- [[Notion]] — 소규모 팀이나 유연한 구조가 필요한 경우 대안
- [[Slack]] — 문서 업데이트를 Slack 채널에 자동 알림 연동

## References

- [Confluence 공식 문서](https://confluence.atlassian.com/)
