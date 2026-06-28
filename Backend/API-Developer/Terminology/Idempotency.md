# Idempotency (멱등성)

## Definition

동일한 요청을 한 번 보내든 여러 번 보내든 서버 상태와 응답 결과가 항상 동일한 API 속성. 수학의 f(f(x)) = f(x)에서 유래.

## Context / When to Use

- 네트워크 타임아웃 후 클라이언트가 요청을 재시도할 때 중복 처리 방지
- 결제·주문 같은 민감한 API에서 이중 처리 사고 예방
- 분산 시스템에서 메시지 재전송 시 안전성 보장

## HTTP 메서드별 멱등성

| 메서드 | 멱등성 | 안전성(부작용 없음) | 설명 |
|---|---|---|---|
| **GET** | O | O | 조회만, 서버 상태 변경 없음 |
| **HEAD** | O | O | GET과 동일, 헤더만 반환 |
| **PUT** | O | X | 동일 데이터로 덮어쓰기, 결과 동일 |
| **DELETE** | O | X | 두 번 삭제해도 리소스는 없음 |
| **POST** | X | X | 호출마다 새 리소스 생성 |
| **PATCH** | △ | X | 구현에 따라 다름 (절대값 vs 상대값) |

```
# PATCH 멱등 예시 (절대값 — 멱등)
PATCH /users/1  { "name": "홍길동" }  →  name이 항상 "홍길동"

# PATCH 비멱등 예시 (상대값 — 비멱등)
PATCH /accounts/1  { "balance": "+1000" }  →  호출마다 잔액 증가
```

## 결제 API와 Idempotency-Key 패턴

POST는 기본적으로 비멱등이지만, `Idempotency-Key` 헤더로 멱등성을 부여할 수 있다.

```
# 첫 번째 요청
POST /payments
Idempotency-Key: a8f3d2e1-9b4c-4f7e-8a1d-3c6e5f2b9d0a
{ "amount": 10000, "currency": "KRW" }

→ 201 Created  { "paymentId": "pay_123", "status": "completed" }

# 네트워크 오류로 응답 못 받아 재시도
POST /payments
Idempotency-Key: a8f3d2e1-9b4c-4f7e-8a1d-3c6e5f2b9d0a  ← 동일한 키
{ "amount": 10000, "currency": "KRW" }

→ 200 OK  { "paymentId": "pay_123", "status": "completed" }  ← 캐시된 응답, 중복 결제 없음
```

### 서버 구현 전략
```
1. 요청 수신 시 Idempotency-Key를 Redis/DB에 저장
2. 이미 존재하는 키이면 → 저장된 응답 그대로 반환
3. 없으면 → 정상 처리 후 응답을 키와 함께 저장 (TTL: 24시간)
```

## 실무 주의사항

- Stripe, Toss Payments 등 주요 결제 API는 Idempotency-Key를 공식 지원
- 키는 UUID v4 등 충분한 무작위성 필요
- 동일 키에 다른 요청 바디를 보내면 `422` 또는 `409` 반환 권고

## Related Terms

- [[REST]] — HTTP 메서드 의미론의 핵심 개념
- [[HTTP-Status-Code]] — 멱등 요청의 재시도 응답 코드 처리
- [[Rate-Limiting]] — 재시도와 Rate Limit의 상호작용

## References

- [Stripe Idempotent Requests](https://stripe.com/docs/api/idempotent_requests)
- [RFC 7231 — Idempotent Methods](https://tools.ietf.org/html/rfc7231#section-4.2.2)
