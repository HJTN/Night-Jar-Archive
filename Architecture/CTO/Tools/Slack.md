# Slack

> 채널 기반 팀 커뮤니케이션 및 워크플로우 자동화 메신저

## Overview

Slack은 채널(Channel) 기반으로 팀 커뮤니케이션을 구조화하는 메신저 플랫폼이다. CTO는 엔지니어링 조직의 정보 흐름을 설계하고, 인시던트 대응 채널 운영, 기술 공지, 비동기 의사결정에 Slack을 활용한다.

## Key Features

- **Channels** — 주제·팀·프로젝트별 대화 공간 분리. 공개/비공개 설정
- **Threads** — 메시지 단위 스레드로 맥락 유지
- **Huddle** — 즉석 음성·화상 통화 (경량 회의 대체)
- **Workflow Builder** — 코딩 없이 자동화 워크플로우 생성 (예: 장애 알림 → 채널 생성)
- **앱 연동** — [[Jira]]·[[Confluence]]·GitHub·PagerDuty·Datadog 등 300+ 앱 통합
- **Slack Connect** — 외부 파트너·벤더와 채널 공유

## CTO 관점 채널 구조 설계

| 채널 유형 | 예시 | 목적 |
|---|---|---|
| 팀 채널 | `#team-backend`, `#team-infra` | 팀 일상 소통 |
| 프로젝트 채널 | `#proj-migration-2025` | 프로젝트 한시적 협업 |
| 인시던트 채널 | `#incident-20250610` | 장애 대응 실시간 조율 |
| 공지 채널 | `#engineering-announcements` | CTO 기술 공지 (쓰기 제한) |
| 학습 채널 | `#tech-share`, `#radar-discuss` | [[Tech-Radar]] 논의, 아티클 공유 |
| 알림 채널 | `#alerts-prod`, `#ci-cd-status` | 자동화 알림 수신 |

## Tips & Shortcuts

- `Cmd+K` (Mac) / `Ctrl+K` (Win) — 채널·멤버 빠른 이동
- `/remind` — 나 또는 채널에 리마인더 설정
- **Star** — 중요 채널·DM을 즐겨찾기로 고정
- **Status** — 집중 모드·회의 중·부재 상태 설정으로 방해 최소화
- 채널 이름 규칙을 전사 표준화하면 탐색성이 크게 향상됨 (`{type}-{team}-{topic}`)

## Related Tools

- [[Jira]] — Jira 이슈 업데이트를 Slack 채널에 자동 알림
- [[Confluence]] — Confluence 페이지 업데이트 알림 수신
- [[Notion]] — Notion 댓글·할당 알림 연동 가능

## References

- [Slack 공식 가이드](https://slack.com/help)
