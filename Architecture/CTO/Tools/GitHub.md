# GitHub

> Git 기반 코드 호스팅·협업·CI/CD 통합 플랫폼

## Overview

GitHub는 전 세계 1억 명 이상의 개발자가 사용하는 코드 협업 플랫폼이다. CTO는 코드를 직접 작성하기보다, 조직 전체의 개발 속도·품질·보안 현황을 집계 뷰로 파악하고 엔지니어링 문화를 가꾸는 데 GitHub를 활용한다.

## Key Features

- **Pull Request** — 코드 리뷰·승인·병합 워크플로우 표준화
- **GitHub Actions** — CI/CD 파이프라인 자동화 (YAML 기반)
- **Insights** — 기여자 활동, PR 사이클 타임, 코드 주파수 통계
- **Security** — Dependabot(의존성 취약점), Code Scanning(SAST), Secret Scanning
- **GitHub Copilot** — AI 코드 자동 완성 (개발자 생산성 도구)
- **Org Settings** — 조직 단위 권한·정책·브랜치 보호 규칙 관리

## CTO 활용 시나리오

| 용도 | 방법 |
|---|---|
| 개발 속도 파악 | Insights → PR 머지 시간, 배포 주기 → [[DORA-Metrics]] |
| 보안 현황 확인 | Security 탭 → CVE·시크릿 노출 현황 파악 |
| 기술 부채 추적 | 오래된 PR·이슈 목록 → [[Technical-Debt]] 파악 |
| AI 생산성 투자 | GitHub Copilot 도입 효과 측정 |
| 접근 권한 거버넌스 | 팀·리포지토리별 권한 정책 설정 |

## DORA 메트릭 추출

GitHub Actions + Insights 데이터로 [[DORA-Metrics]] 4가지 지표 측정:

| DORA 지표 | GitHub 데이터 소스 |
|---|---|
| 배포 빈도 | Actions 배포 워크플로우 실행 횟수 |
| 변경 리드타임 | PR 생성 → 프로덕션 배포 완료까지 시간 |
| 변경 실패율 | 배포 후 롤백·핫픽스 PR 비율 |
| 평균 복구 시간 | 장애 이슈 생성 → 해결까지 시간 |

## Related Tools

- [[GitLab]] — CI/CD 통합이 더 강하고 자체 호스팅 선호 시 대안
- [[Jira]] — 이슈와 PR 연결 (브랜치 이름에 이슈 번호 포함)
- [[Datadog]] / [[Grafana]] — 배포 이벤트를 모니터링 대시보드에 연동
- [[Slack]] — PR 리뷰 요청·머지 알림 연동

## References

- [GitHub 공식 문서](https://docs.github.com/)
- [GitHub Actions 가이드](https://docs.github.com/en/actions)
