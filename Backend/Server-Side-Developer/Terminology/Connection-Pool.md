# Connection Pool (커넥션 풀)

## Definition

DB 연결을 미리 생성해 재사용함으로써 오버헤드를 줄이는 기법. 매 요청마다 새 커넥션을 생성하는 대신, 풀에서 빌려 쓰고 반납한다.

## 커넥션 풀 없이 쓸 때 문제점

DB 연결 생성은 비싼 작업이다.

1. TCP 3-way handshake
2. DB 인증 (username/password 검증)
3. 세션 초기화

초당 수백 요청이 들어오는 서버에서 매번 이 과정을 반복하면 응답 지연과 DB 과부하가 발생한다.

커넥션 풀은 이 연결들을 미리 만들어두고 재사용하여 이 문제를 해결한다.

```
요청 → 풀에서 커넥션 대여 → DB 작업 → 커넥션 반납 → 풀로 돌아감
```

## HikariCP (Spring Boot 기본 커넥션 풀)

Spring Boot 2.x부터 기본 커넥션 풀. 가장 빠른 Java 커넥션 풀 라이브러리.

### 핵심 파라미터

| 파라미터 | 기본값 | 설명 | 권장 |
|---------|--------|------|------|
| `maximumPoolSize` | 10 | 풀의 최대 커넥션 수 | CPU 코어 수 기준으로 계산 |
| `minimumIdle` | maximumPoolSize와 동일 | 유휴 상태로 유지할 최소 커넥션 수 | 고정 풀이면 maximumPoolSize와 같게 |
| `connectionTimeout` | 30,000ms | 풀에서 커넥션 대기 최대 시간 | 3,000~5,000ms로 낮추는 것 고려 |
| `idleTimeout` | 600,000ms | 유휴 커넥션이 풀에서 제거되는 시간 | 10분 |
| `maxLifetime` | 1,800,000ms | 커넥션 최대 수명 (DB의 wait_timeout보다 짧게) | DB 설정보다 수분 짧게 |
| `keepaliveTime` | 0 (비활성) | 유휴 커넥션의 생존 확인 주기 | 60,000ms 권장 |

```yaml
# application.yml
spring:
  datasource:
    hikari:
      maximum-pool-size: 20
      minimum-idle: 20        # 고정 풀 사이즈 권장
      connection-timeout: 5000
      max-lifetime: 1800000
      keepalive-time: 60000
      pool-name: MyHikariPool
```

## 적정 풀 사이즈 계산법

HikariCP 저자 Brett Wooldridge의 공식:

```
pool size = Tn × (Cm - 1) + 1

Tn = 최대 스레드 수
Cm = 한 트랜잭션에서 동시에 필요한 최대 커넥션 수
```

실용적인 접근법 (PostgreSQL 권장):

```
pool size = (core_count × 2) + effective_spindle_count

예: CPU 4코어, SSD(spindle=1)
→ (4 × 2) + 1 = 9 → 10으로 올림
```

**중요**: 풀 사이즈를 크게 한다고 반드시 성능이 좋아지지 않는다. 과도한 커넥션은 DB 서버 부하를 오히려 증가시킨다.

## 커넥션 풀 모니터링

```java
// HikariCP 메트릭 (Actuator + Micrometer)
// /actuator/metrics/hikaricp.connections.active
// /actuator/metrics/hikaricp.connections.pending (이 값이 지속적으로 높으면 풀 사이즈 부족)
```

- `hikaricp.connections.active`: 현재 사용 중인 커넥션 수
- `hikaricp.connections.pending`: 커넥션 대기 중인 스레드 수 → 0에 가까워야 정상
- `hikaricp.connections.timeout`: 타임아웃 발생 횟수 → 0이어야 정상

## 흔한 실수

1. **커넥션 미반납**: try-with-resources 또는 Spring @Transactional 사용으로 방지
2. **풀 사이즈 과대 설정**: DB 서버 max_connections 초과 주의
3. **maxLifetime > DB wait_timeout**: DB가 먼저 연결을 끊으면 "Broken pipe" 에러 발생

## Related Terms

- [[Concurrency]] - 풀 접근 시 스레드 안전성
- [[ORM]] - JPA/Hibernate는 커넥션 풀 위에서 동작
- [[Caching]] - 캐싱으로 DB 커넥션 사용량 자체를 줄일 수 있음

## References

- [HikariCP - About Pool Sizing](https://github.com/brettwooldridge/HikariCP/wiki/About-Pool-Sizing)
- [HikariCP Configuration](https://github.com/brettwooldridge/HikariCP#gear-configuration-knobs-baby)
