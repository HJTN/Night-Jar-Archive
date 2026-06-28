# Message Queue (메시지 큐)

## Definition

서비스 간 비동기 통신을 위한 메시지 버퍼. Producer가 메시지를 큐에 넣으면 Consumer가 꺼내서 처리한다. 직접 호출 대신 메시지 브로커를 중간에 두어 두 서비스를 느슨하게 결합한다.

## 구조: Producer / Broker / Consumer

```
[Producer]  →  [Message Broker]  →  [Consumer]
주문 서비스      RabbitMQ / Kafka      알림 서비스
                                      재고 서비스
                                      결제 서비스
```

- **Producer**: 메시지를 생성해 브로커에 전송
- **Broker**: 메시지를 저장하고 Consumer에게 전달 (RabbitMQ, Kafka, AWS SQS 등)
- **Consumer**: 브로커에서 메시지를 가져와 처리
- **Queue/Topic**: Producer가 보내는 메시지의 목적지

## 비동기 처리의 이점

| 동기 호출 | 비동기 메시지 큐 |
|-----------|----------------|
| A 서비스가 B 서비스 응답을 기다림 | A는 메시지만 보내고 즉시 다음 작업 수행 |
| B 서비스 장애 시 A도 실패 | B 장애 시 메시지는 큐에 보존됨 |
| 급격한 트래픽 증가 시 B 과부하 | 큐가 버퍼 역할로 트래픽 평탄화 |
| 결합도 높음 (B의 API를 A가 알아야 함) | 결합도 낮음 (인터페이스는 메시지 포맷만) |

## Kafka vs RabbitMQ 비교

| 항목 | Apache Kafka | RabbitMQ |
|------|-------------|----------|
| 모델 | 분산 로그 (Log-based) | 전통적 메시지 큐 |
| 메시지 보존 | 설정한 기간 동안 보존 (기본 7일) | Consumer가 소비하면 삭제 |
| 처리량 | 매우 높음 (초당 수백만 건) | 중간 (초당 수만~수십만 건) |
| 순서 보장 | 파티션 내에서 순서 보장 | 큐 내에서 순서 보장 |
| 재처리 | 오프셋으로 과거 메시지 재소비 가능 | 기본적으로 재소비 불가 |
| 라우팅 | Topic/Partition 기반 단순 라우팅 | Exchange를 통한 유연한 라우팅 |
| 적합한 사용 | 이벤트 스트리밍, 로그 수집, 감사(Audit) | 작업 큐, RPC, 복잡한 라우팅 |

## 전달 보장 수준

| 수준 | 설명 | 특징 |
|------|------|------|
| **At-most-once** | 최대 한 번 전달 (유실 가능) | 가장 빠름. 로그·지표 등 손실 허용 데이터에 적합 |
| **At-least-once** | 최소 한 번 전달 (중복 가능) | 메시지는 반드시 처리되지만 중복 처리 가능. Consumer가 멱등성(Idempotent) 보장해야 함 |
| **Exactly-once** | 정확히 한 번 전달 | 구현 복잡, 성능 비용 큼. 금융·결제처럼 중복이 치명적인 경우 |

### 멱등성 (Idempotency)
같은 메시지를 여러 번 처리해도 결과가 동일해야 한다. At-least-once 보장을 사용할 때 필수.

```java
// 멱등성 보장 예시: 처리된 메시지 ID를 DB에 기록
public void processOrder(OrderMessage msg) {
    if (processedMessageRepository.exists(msg.getMessageId())) {
        return; // 이미 처리됨, 중복 무시
    }
    // 주문 처리 로직
    processedMessageRepository.save(msg.getMessageId());
}
```

## 사용 예시 패턴

### 이벤트 기반 알림
```
주문 완료 → [주문 이벤트 발행] → Kafka → [알림 Consumer] → 이메일/푸시 발송
                                        → [포인트 Consumer] → 적립금 지급
                                        → [재고 Consumer] → 재고 차감
```

### 작업 큐 (Task Queue)
```
API 요청 (동영상 인코딩) → [큐에 작업 추가] → 즉시 202 Accepted 응답
                                            ↓
                                     [Worker Pool] → 백그라운드 처리
```

## Related Terms

- [[Middleware]] - 메시지 큐와 미들웨어 모두 관심사 분리 도구
- [[Concurrency]] - Consumer 병렬 처리 시 동시성 고려
- [[Caching]] - 처리 결과를 캐시에 저장하는 패턴과 조합

## References

- [Apache Kafka 공식 문서](https://kafka.apache.org/documentation/)
- [RabbitMQ 공식 문서](https://www.rabbitmq.com/documentation.html)
- [AWS SQS - Message Delivery](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/welcome.html)
