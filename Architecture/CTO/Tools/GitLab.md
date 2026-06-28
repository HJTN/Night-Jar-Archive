# GitLab

> DevSecOps 통합 플랫폼 — 코드 호스팅·CI/CD·보안·모니터링 올인원

## Overview

GitLab은 코드 관리부터 CI/CD·보안 스캔·모니터링까지 소프트웨어 개발 수명주기 전체를 단일 플랫폼으로 제공하는 DevSecOps 도구다. 자체 호스팅(Self-Managed)이 가능해 보안·데이터 주권이 중요한 조직(금융, 공공, 엔터프라이즈)에서 선호된다.

## Key Features

- **CI/CD** — 내장 파이프라인 (`.gitlab-ci.yml`). 복잡한 멀티스테이지 파이프라인에 강점
- **Self-Managed** — 온프레미스 또는 사설 클라우드에 직접 설치·운영 (CE 무료)
- **Security Scanning** — SAST·DAST·의존성 스캔·컨테이너 스캔 통합
- **Container Registry** — 내장 Docker 이미지 저장소
- **GitLab Duo (AI)** — AI 코드 어시스턴트 (GitHub Copilot 대응)
- **Value Stream Analytics** — 개발 사이클 전체의 리드타임·병목 분석 → [[DORA-Metrics]]

## GitHub vs GitLab 비교

| 기준 | GitHub | GitLab |
|---|---|---|
| 생태계 | 더 큰 오픈소스 커뮤니티 | 완결된 DevSecOps 툴체인 |
| CI/CD | Actions (외부 연동 강점) | 내장 CI (자체 완결) |
| 자체 호스팅 | GitHub Enterprise (유료) | Community Edition (무료) |
| 보안 스캔 | 별도 도구 필요 | 내장 (Ultimate 티어) |
| 데이터 주권 | GitHub.com SaaS | 완전 자체 호스팅 가능 |

> CTO 선택 기준: 오픈소스 생태계 연결이 중요하면 GitHub, 보안·컴플라이언스·자체 호스팅이 중요하면 GitLab

## CTO 활용 시나리오

| 용도 | 방법 |
|---|---|
| 보안 컴플라이언스 | 내장 Security Dashboard로 전사 취약점 현황 파악 |
| 개발 속도 추적 | Value Stream Analytics → [[DORA-Metrics]] |
| 인프라 코드 관리 | Terraform·Helm 차트 리포지토리 중앙화 |
| 규제 감사 대응 | 모든 변경 이력·승인 기록을 Self-Managed로 보관 |

## Related Tools

- [[GitHub]] — SaaS 중심·오픈소스 생태계 활용 시 대안
- [[Jira]] — 이슈 트래킹 연동
- [[Datadog]] — 배포 이벤트 모니터링 연동

## References

- [GitLab 공식 문서](https://docs.gitlab.com/)
- [GitLab vs GitHub 비교](https://about.gitlab.com/devops-tools/github-vs-gitlab/)
