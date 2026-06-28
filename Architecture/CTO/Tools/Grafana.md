# Grafana

> 오픈소스 모니터링·시각화 플랫폼

## Overview

Grafana는 Prometheus·Elasticsearch·InfluxDB 등 다양한 데이터 소스에서 메트릭을 가져와 시각화하는 오픈소스 도구다. 자체 호스팅이 가능해 데이터를 외부 SaaS에 보내지 않으려는 팀이나 비용 절감을 원하는 조직에 적합하다. CTO는 [[DORA-Metrics]]와 인프라 건강도를 집계 뷰로 확인하는 데 활용한다.

## Key Features

- **Dashboard** — 다양한 차트·게이지·테이블로 메트릭 시각화
- **Multi Data Source** — Prometheus, Loki(로그), Tempo(트레이스), CloudWatch, BigQuery 등 통합
- **Alerting** — 임계값 기반 알림 → [[Slack]]·PagerDuty 연동
- **Grafana Cloud** — SaaS 버전 (자체 호스팅 없이 사용 가능, 무료 티어 제공)
- **Explore** — 로그·메트릭·트레이스를 한 화면에서 상관 분석

## CTO 활용 시나리오

| 용도 | 방법 |
|---|---|
| SLO 대시보드 | Prometheus 기반 가용성·레이턴시 집계 |
| 인프라 비용 추적 | 클라우드 메트릭으로 [[FinOps]] 지표 시각화 |
| DORA 메트릭 | 배포 이벤트·장애 데이터로 [[DORA-Metrics]] 계산 |
| 인시던트 대응 | 장애 발생 시 관련 메트릭 Explore로 원인 추적 |

## Datadog vs Grafana 비교

| 기준 | Datadog | Grafana |
|---|---|---|
| 비용 | 유료 SaaS (에이전트당 과금) | 오픈소스 무료 (Cloud는 유료) |
| 설치·운영 | SaaS, 즉시 사용 | 자체 호스팅 운영 필요 |
| 통합 | 600+ 기본 통합 | 데이터 소스 플러그인 방식 |
| 데이터 주권 | 외부 SaaS 전송 | 자체 보관 가능 |
| 적합 규모 | 스케일업~대기업 | 스타트업~중대형 |

> 스타트업: Grafana Cloud 무료 티어로 시작 → 스케일업 후 Datadog 전환 또는 자체 호스팅 유지

## Related Tools

- [[Datadog]] — SaaS 기반 상용 대안
- [[Slack]] — 알림 연동

## References

- [Grafana 공식 문서](https://grafana.com/docs/)
- [Prometheus + Grafana 스택](https://prometheus.io/)
