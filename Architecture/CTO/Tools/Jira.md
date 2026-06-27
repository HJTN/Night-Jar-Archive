# Jira

> Atlassian의 이슈 트래킹 및 애자일 프로젝트 관리 도구

## Overview

Jira는 소프트웨어 개발팀의 이슈·버그·스토리·에픽을 관리하는 업계 표준 도구다. CTO는 직접 사용하기보다 엔지니어링 조직 전체의 진행 상황·병목·리스크를 집계 뷰로 파악하는 데 활용한다.

## Key Features

- **Issue Types** — Epic·Story·Task·Bug·Subtask 계층 구조
- **Scrum/Kanban Board** — 스프린트 기반 또는 흐름 기반 작업 관리
- **Roadmap (Advanced)** — 에픽·분기 단위 기술 로드맵 시각화
- **JQL (Jira Query Language)** — 복잡한 필터·리포트 작성 가능
- **Dashboards** — 팀·조직 단위 진행 현황 집계 시각화
- **Confluence 연동** — 스펙 문서·회의록과 이슈 직접 연결

## CTO 활용 시나리오

| 용도 | 방법 |
|---|---|
| 엔지니어링 현황 파악 | Dashboard로 팀별 완료율·블로커 한눈에 확인 |
| [[OKR]] 연계 | Epic → OKR Objective 매핑. KR 진행률을 스토리 포인트로 추적 |
| 채용 파이프라인 | 커스텀 프로젝트로 후보자 단계 관리 → [[Engineering-Hiring-Process]] |
| 기술 부채 관리 | [[Technical-Debt]] 태그 이슈 모음. 분기 상환 현황 추적 |
| 릴리즈 추적 | Fix Version 기능으로 릴리즈별 포함 이슈 관리 |

## Tips & Shortcuts

- `g` + `g` — 빠른 이슈 이동
- **JQL 예시**: `project = ENG AND labels = "tech-debt" AND status != Done` — 미해결 기술 부채 이슈 목록
- **Epic Link** — 스토리를 에픽에 연결해 로드맵 진행률 자동 집계
- **Automation** — 규칙 기반 자동화로 반복 작업 제거 (예: 스프린트 종료 시 미완료 이슈 자동 이월)

## Related Tools

- [[Confluence]] — 설계 문서·스펙·포스트모템과 이슈 연결
- [[Slack]] — Jira 알림을 채널에 자동 발송
- [[Notion]] — 소규모 팀이나 간단한 관리에는 Notion으로 대체 가능

## References

- [Jira 공식 문서](https://support.atlassian.com/jira-software-cloud/)
