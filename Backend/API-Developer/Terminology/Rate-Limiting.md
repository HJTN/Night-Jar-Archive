# Rate Limiting

## Definition

단위 시간당 클라이언트가 보낼 수 있는 API 요청 수를 제한하는 정책. API 남용·DDoS 방어, 서버 과부하 방지, 공평한 자원 배분을 목적으로 한다.

## Context / When to Use

- 공개 API 또는 외부 파트너에게 제공하는 API
- 비용이 발생하는 AI·SMS·결제 API 호출 보호
- 특정 사용자의 폭발적 요청이 다른 사용자에게 영향을 줄 때

## 알고리즘 비교

| 알고리즘 | 원리 | 장점 | 단점 |
|---|---|---|---|
| **Fixed Window** | 고정 시간 창(1분)에 N개 허용 | 구현 단순 | 창 경계에서 2배 버스트 가능 |
| **Sliding Window** | 현재 시점 기준 N초 이전~현재 집계 | 경계 버스트 없음 | 메모리 사용 많음 |
| **Token Bucket** | 버킷에 토큰 충전, 요청마다 소비 | 버스트 허용, 유연함 | 구현 복잡 |
| **Leaky Bucket** | 요청을 큐에 넣고 일정 속도로 처리 | 출력 속도 일정 | 큐 초과 시 요청 드롭 |

### Fixed Window 문제점 시각화
```
[0:00~0:59] 100개 허용
[0:58] 100개 요청 → 허용
[1:00] 새 창 시작
[1:01] 100개 요청 → 허용
→ 3초 동안 200개 요청 통과!
```

### Token Bucket 동작
```
버킷 용량: 100개 토큰
충전 속도: 10개/초
요청 처리: 요청 1건 = 토큰 1개 소비

→ 평소에 토큰 축적 → 버스트 시 한 번에 100개까지 처리 가능
```

## 응답 헤더

Rate Limit 초과 전·후 클라이언트에게 정보를 제공하는 표준 헤더:

| 헤더 | 의미 |
|---|---|
| `X-RateLimit-Limit` | 창당 허용 요청 수 |
| `X-RateLimit-Remaining` | 현재 창에서 남은 요청 수 |
| `X-RateLimit-Reset` | 제한이 초기화되는 Unix 타임스탬프 |
| `Retry-After` | 429 응답 시, N초 후 재시도 권고 |

```
HTTP/1.1 429 Too Many Requests
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 0
X-RateLimit-Reset: 1735689600
Retry-After: 30
Content-Type: application/json

{
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "요청 한도를 초과했습니다. 30초 후 재시도하세요."
  }
}
```

## 구현 전략

- **IP 기반**: 미인증 API에 적용, Redis에 `rate:ip:192.168.1.1` 키로 카운터 저장
- **User 기반**: 인증된 사용자 단위 제한, 플랜별 차등 제한 가능
- **API Key 기반**: 파트너 통합 API에서 키별 할당량 관리

```
# Redis를 이용한 Fixed Window 구현
INCR rate:user:123:1735689600
EXPIRE rate:user:123:1735689600 60
→ 값이 100 초과 시 429 반환
```

## Related Terms

- [[HTTP-Status-Code]] — 429 Too Many Requests 응답 코드
- [[REST]] — RESTful API 운영에서 Rate Limiting은 필수 보안 레이어
- [[Idempotency]] — Rate Limit으로 차단된 요청의 재시도 전략

## References

- [IETF RFC 6585 — 429 Too Many Requests](https://tools.ietf.org/html/rfc6585)
- [Stripe Rate Limiting](https://stripe.com/docs/rate-limits)
