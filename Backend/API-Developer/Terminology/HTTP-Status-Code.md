# HTTP Status Code

## Definition

서버가 클라이언트 요청의 처리 결과를 3자리 숫자 코드로 알려주는 표준 응답 코드. RFC 7231로 정의되며 첫 자리가 결과 분류를 나타낸다.

## Context / When to Use

- API 응답을 설계할 때 상황에 맞는 코드를 명시적으로 반환해야 함
- 클라이언트가 응답 코드만 보고 재시도·에러 처리를 결정할 수 있어야 함
- 잘못된 코드 사용(예: 에러에 200 반환)은 디버깅을 어렵게 만듦

## 1xx~5xx 분류

| 분류 | 의미 | 설명 |
|---|---|---|
| **1xx** | Informational | 요청을 수신, 처리 중 |
| **2xx** | Success | 요청 정상 처리 |
| **3xx** | Redirection | 추가 조치 필요 (리다이렉트) |
| **4xx** | Client Error | 클라이언트 요청 오류 |
| **5xx** | Server Error | 서버 측 처리 오류 |

## API에서 자주 쓰는 코드 상세

### 2xx — 성공

| 코드 | 이름 | 사용 상황 |
|---|---|---|
| **200** | OK | GET/PUT/PATCH 성공, 응답 본문 있음 |
| **201** | Created | POST로 리소스 생성 성공, `Location` 헤더에 URI 포함 |
| **204** | No Content | DELETE 성공 또는 본문 없는 PUT 성공 |

### 4xx — 클라이언트 오류

| 코드 | 이름 | 사용 상황 |
|---|---|---|
| **400** | Bad Request | 요청 파라미터·바디 형식 오류 |
| **401** | Unauthorized | 인증 토큰 없음·만료 (로그인 필요) |
| **403** | Forbidden | 인증은 됐지만 권한 없음 |
| **404** | Not Found | 요청한 리소스가 존재하지 않음 |
| **409** | Conflict | 리소스 충돌 (중복 이메일 가입 등) |
| **422** | Unprocessable Entity | 형식은 맞지만 비즈니스 유효성 실패 |
| **429** | Too Many Requests | Rate Limit 초과 |

### 5xx — 서버 오류

| 코드 | 이름 | 사용 상황 |
|---|---|---|
| **500** | Internal Server Error | 예상치 못한 서버 오류 (버그) |
| **503** | Service Unavailable | 서버 과부하·점검 중 |

## 자주 혼동되는 코드

```
401 vs 403
  401 → "당신이 누구인지 모름" (로그인 안 됨)
  403 → "당신이 누구인지는 알지만 권한 없음"

400 vs 422
  400 → JSON 파싱 자체 실패, 필수 필드 누락
  422 → 형식은 맞지만 비즈니스 규칙 위반 (이미 사용된 이메일)

404 vs 410
  404 → 리소스 존재 여부 불확실 또는 의도적으로 숨김
  410 → 리소스가 영구적으로 삭제됨 (Gone)
```

## 에러 응답 형식 권고

```json
{
  "error": {
    "code": "USER_NOT_FOUND",
    "message": "요청한 사용자를 찾을 수 없습니다.",
    "details": {
      "userId": "999"
    }
  }
}
```

## Related Terms

- [[REST]] — HTTP 메서드와 상태 코드로 API를 표현하는 아키텍처
- [[Rate-Limiting]] — 429 Too Many Requests와 직접 연관
- [[Idempotency]] — 멱등 메서드와 적절한 상태 코드 매핑

## References

- [RFC 7231 — HTTP/1.1 Semantics and Content](https://tools.ietf.org/html/rfc7231)
- [httpstatuses.com](https://httpstatuses.com/)
