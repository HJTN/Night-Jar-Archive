# 확장성 (Scalability)

## Definition

시스템의 부하(트래픽, 데이터량, 사용자 수)가 증가할 때 성능 저하 없이 용량을 늘릴 수 있는 능력.

좋은 확장성 설계 = 부하 증가가 아키텍처 변경이 아닌 **리소스 추가**만으로 해결된다.

## Context / When to Use

시스템이 성장할 것으로 예상될 때. 초기 트래픽이 낮더라도 확장 전략을 미리 설계해야 한다.

## 확장 유형

| 유형 | 방법 | 특징 |
|---|---|---|
| **수직 확장 (Scale-Up)** | 서버의 CPU·메모리 업그레이드 | 빠르고 단순, 한계 존재, 다운타임 발생 가능 |
| **수평 확장 (Scale-Out)** | 서버 대수를 늘림 | 이론적으로 무한 확장, 분산 처리 필요 |

## 수평 확장을 위한 설계 원칙

| 원칙 | 설명 |
|---|---|
| **Stateless** | 세션·상태를 서버에 저장하지 않음 → 어느 서버로도 라우팅 가능 |
| **데이터 분리** | DB, 세션, 파일을 외부 스토리지로 분리 (Redis, S3, RDS) |
| **비동기 처리** | 메시지 큐로 부하 분산 (Kafka, SQS) |
| **캐싱** | Redis, CDN으로 반복 조회 부하 감소 |
| **Read Replica** | 읽기 부하를 복제본으로 분산 |
| **파티셔닝/샤딩** | 데이터를 분산 저장 |

## 확장성 설계 체크포인트

```
DAU(일일 활성 사용자) 추정
→ TPS 추정 (예: DAU × 평균 액션 수 / 86,400)
→ 병목 지점 식별 (DB? API? 외부 서비스?)
→ 각 병목에 맞는 확장 전략 선택
→ [[High-Availability]] 전략과 통합
```

## Auto Scaling (자동 확장)

- 클라우드 환경에서 트래픽에 따라 인스턴스를 자동으로 추가/제거
- AWS: Auto Scaling Group, ECS Auto Scaling
- 기준 지표: CPU 사용률, 요청 수, 큐 깊이

## Related Terms

- [[High-Availability]] — 확장성과 함께 설계
- [[NFR]] — 확장성은 핵심 NFR 중 하나
- [[Trade-off]] — Scale-Up vs Scale-Out 트레이드오프

## References

- AWS Well-Architected Framework, Performance Efficiency Pillar
- Martin Abbott, Michael Fisher, "The Art of Scalability" (2015)
