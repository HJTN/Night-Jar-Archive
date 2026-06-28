# Datadog

> 클라우드 인프라·애플리케이션 통합 모니터링 및 관찰 가능성(Observability) SaaS 플랫폼

## Overview

Datadog은 메트릭·로그·트레이스를 단일 플랫폼에서 통합 관리하는 상용 모니터링 도구다. CTO는 시스템 전반의 SLO/SLA 달성 현황을 집계 뷰로 파악하고, 장애 발생 시 신속한 원인 추적에 활용한다.

## Key Features

- **Infrastructure Monitoring** — 서버·컨테이너·클라우드 리소스 메트릭 수집
- **APM (Application Performance Monitoring)** — 분산 트레이싱, 서비스 간 레이턴시 병목 파악
- **Log Management** — 전사 로그 중앙 수집·검색·분석
- **Dashboards** — 커스텀 대시보드로 SLO/SLA·비용·[[DORA-Metrics]] 시각화
- **Monitors & Alerts** — 임계값 기반 알림 → [[Slack]]·PagerDuty 연동
- **SLO Tracking** — 에러 버짓 소진율 자동 추적

## CTO 활용 시나리오

| 용도 | 방법 |
|---|---|
| SLO/SLA 현황 파악 | 서비스별 가용성·레이턴시 대시보드 집계 뷰 |
| [[OKR]] KR 추적 | 배포 빈도·장애 복구 시간([[DORA-Metrics]]) 자동 집계 |
| 비용 관리 | 인프라 리소스 사용량 트렌드 → [[FinOps]] 연계 |
| 인시던트 대응 | 장애 감지 → [[Incident-Response-Process]] 트리거 |
| 이사회 보고 | 엔지니어링 신뢰성 지표를 비즈니스 언어로 변환 |

## CTO 관점 핵심 대시보드

1. **Engineering Health** — 전체 서비스 SLO 달성률, 장애 빈도
2. **DORA Metrics** — 배포 빈도, 리드타임, 변경 실패율, 복구 시간
3. **Cost & Usage** — 팀·서비스별 인프라 비용 트렌드

## Related Tools

- [[Grafana]] — 오픈소스 대안. 데이터 주권·비용이 중요한 경우
- [[Slack]] — 알림 채널 연동
- [[Jira]] — 인시던트를 Jira 이슈로 자동 생성 가능

## References

- [Datadog 공식 문서](https://docs.datadoghq.com/)
- [Datadog SLO 가이드](https://docs.datadoghq.com/monitors/service_level_objectives/)
