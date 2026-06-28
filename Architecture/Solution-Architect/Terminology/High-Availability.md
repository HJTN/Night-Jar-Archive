# High Availability (고가용성, HA)

## Definition

시스템이 장애 없이 지속적으로 운영되는 능력. 보통 **99.9% 이상의 업타임**을 목표로 설계한다.

가용성은 단순히 서버를 여러 대 두는 것이 아니라, 장애 발생 시 자동으로 복구되는 구조를 설계하는 것이다.

## Context / When to Use

SLA에서 가용성 목표가 정의될 때. 서비스 다운타임이 비즈니스 손실에 직결되는 시스템 설계 시.

## 가용성 수준 (Nines)

| 가용성 | 연간 다운타임 | 해당 수준 |
|---|---|---|
| 99% | 87.6시간 | - |
| 99.9% ("Three Nines") | 8.76시간 | 일반 서비스 |
| 99.95% | 4.38시간 | 주요 서비스 |
| 99.99% ("Four Nines") | 52.6분 | 금융·이커머스 |
| 99.999% ("Five Nines") | 5.26분 | 통신·의료 |

## 핵심 HA 패턴

| 패턴 | 설명 |
|---|---|
| **Active-Active** | 모든 노드가 트래픽 처리, 한 노드 장애 시 나머지가 이어받음 |
| **Active-Passive** | Standby 노드가 대기, Primary 장애 시 Failover |
| **Multi-AZ 배포** | 여러 가용 영역(AZ)에 분산 배포 |
| **Load Balancer** | 트래픽을 여러 인스턴스에 분산 |
| **Circuit Breaker** | 장애 서비스 격리, 연쇄 장애 방지 |
| **Health Check & Auto Scaling** | 비정상 인스턴스 자동 교체·확장 |

## HA와 DR의 차이

| 항목 | HA (고가용성) | DR (재해 복구) |
|---|---|---|
| **목적** | 일반 장애로 인한 중단 최소화 | 재해(데이터센터 전체 장애) 복구 |
| **RTO** | 초~분 수준 | 분~시간 수준 |
| **복잡도** | 상대적으로 낮음 | 높음 (Multi-Region) |
| **비용** | 중간 | 높음 |

## 관련 지표

- **MTBF** (Mean Time Between Failures): 장애 간 평균 시간
- **MTTR** (Mean Time To Recovery): 장애 복구 평균 시간
- **RTO** (Recovery Time Objective): 복구 목표 시간
- **RPO** (Recovery Point Objective): 데이터 복구 목표 시점

## Related Terms

- [[NFR]] — 가용성은 핵심 NFR 중 하나
- [[Scalability]] — HA와 함께 설계
- [[Solution-Review-Checklist]] — HA 항목 체크

## References

- AWS Well-Architected Framework, Reliability Pillar
