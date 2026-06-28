# DORA Metrics

## Definition

DevOps Research and Assessment(DORA) 팀이 수만 개 조직을 연구해 도출한 **소프트웨어 개발 팀 성과의 4가지 핵심 지표**. 엔지니어링 생산성과 안정성을 객관적으로 측정하는 업계 표준이다.

## 4가지 지표

| 지표 | 정의 | 측정 방법 |
|---|---|---|
| **Deployment Frequency** (배포 빈도) | 프로덕션에 코드를 배포하는 빈도 | CI/CD 파이프라인 배포 이벤트 횟수 |
| **Lead Time for Changes** (변경 리드타임) | 코드 커밋 → 프로덕션 배포까지 걸리는 시간 | PR 생성 시각 ~ 배포 완료 시각 |
| **Change Failure Rate** (변경 실패율) | 배포 후 장애·롤백·핫픽스가 발생한 비율 | (장애 유발 배포 수) / (전체 배포 수) |
| **Time to Restore Service** (복구 시간) | 장애 발생 → 서비스 복구까지 걸리는 시간 | 인시던트 시작 ~ 종료 시각 |

## 성과 등급

| 등급 | 배포 빈도 | 리드타임 | 변경 실패율 | 복구 시간 |
|:---:|---|---|:---:|---|
| **Elite** | 일 여러 번 | 1시간 미만 | 0~15% | 1시간 미만 |
| **High** | 일 1회 ~ 주 1회 | 1일 ~ 1주 | 0~15% | 1일 미만 |
| **Medium** | 주 1회 ~ 월 1회 | 1주 ~ 1개월 | 0~15% | 1일 ~ 1주 |
| **Low** | 월 1회 미만 | 1개월 초과 | 16~30% | 1주 초과 |

## CTO 활용 방법

- [[OKR]] Key Result로 DORA 지표 목표값 설정 (예: "리드타임 5일 → 1일")
- [[Quarterly-Review-Checklist]]에 분기별 DORA 지표 점검 항목 포함
- [[Datadog]] / [[Grafana]] 대시보드로 실시간 추적
- [[GitHub]] / [[GitLab]] 배포·이슈 데이터에서 자동 산출 가능

## 해석 시 주의사항

- 지표는 목표가 아니라 **신호**. 지표를 높이기 위해 측정 방식을 바꾸면 의미 없음
- 배포 빈도가 높다고 무조건 좋은 것이 아님 — 변경 실패율과 함께 봐야 함
- 팀 간 비교보다 **동일 팀의 시계열 변화**를 보는 것이 더 유용

## Related Terms

- [[OKR]] — DORA 지표를 KR로 정량화
- [[Engineering-Culture]] — DORA 지표가 높은 팀은 심리적 안전감도 높다는 연구 결과
- [[Tech-Radar]] — CI/CD 도구 채택이 배포 빈도와 직결
- [[Technical-Debt]] — 기술 부채가 쌓이면 리드타임·실패율이 악화

## References

- [DORA State of DevOps Report](https://dora.dev/research/)
- [Google Cloud — Four Keys to Measure DevOps Performance](https://cloud.google.com/blog/products/devops-sre/using-the-four-keys-to-measure-your-devops-performance)
