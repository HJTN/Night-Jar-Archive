# API Versioning

## Definition

기존 클라이언트를 깨뜨리지 않으면서(하위 호환성 유지) API를 발전시키기 위해 버전을 명시적으로 관리하는 전략.

## Context / When to Use

- 기존 클라이언트에 Breaking Change(필드 제거, 타입 변경, 응답 구조 변경)가 필요할 때
- 여러 버전의 클라이언트(앱 구버전, 신버전)가 동시에 운영될 때
- 공개 API를 외부 파트너에게 제공할 때

## 버전 관리 방식 비교

| 방식 | 예시 | 장점 | 단점 |
|---|---|---|---|
| **URI 경로** | `/v1/users` | 명시적, 쉬운 라우팅, URL로 바로 확인 | URI가 지저분해짐, REST 순수주의에 반함 |
| **쿼리 파라미터** | `/users?version=1` | URI 깔끔 | 캐싱 복잡, 의도치 않게 누락 가능 |
| **요청 헤더** | `Accept-Version: v1` | URI 깔끔, REST에 부합 | 가시성 낮음, 테스트 불편 |
| **Content Negotiation** | `Accept: application/vnd.api.v1+json` | 표준 HTTP 방식 | 구현 복잡, 클라이언트 설정 어려움 |

**실무 권장**: URI 경로 방식 (`/v1/`, `/v2/`) → 명시적이고 캐싱 친화적

## URI 버전 설계

```
# 좋은 예
GET  https://api.example.com/v1/users
GET  https://api.example.com/v2/users

# 마이너 버전은 URI에 넣지 않음 (하위 호환)
❌ /v1.1/users  → 비권장
✅ /v1/users    → 하위 호환 변경은 같은 버전 내에서
```

## Semantic Versioning (의미 버전)

```
MAJOR.MINOR.PATCH
  2  .  3  .  1

MAJOR: Breaking Change (하위 호환 불가)
       → URI 버전 증가 /v2/
MINOR: 새 기능 추가, 하위 호환 유지
       → 동일 URI, 새 필드 추가
PATCH: 버그 수정
       → 동일 URI, 동작 수정
```

### Breaking Change 판단 기준
```
Breaking Change (버전 증가 필요):
  ❌ 응답 필드 제거 또는 이름 변경
  ❌ 필수 요청 파라미터 추가
  ❌ 응답 타입 변경 (string → number)
  ❌ 에러 코드 변경

Non-Breaking Change (같은 버전 유지 가능):
  ✅ 새 선택적 요청 파라미터 추가
  ✅ 새 응답 필드 추가
  ✅ 새 엔드포인트 추가
  ✅ 버그 수정 (스펙 변경 없음)
```

## Deprecation 정책

```
1. Deprecated 공지: Sunset 헤더 또는 응답 필드에 명시
   Sunset: Sat, 31 Dec 2026 23:59:59 GMT
   Deprecation: true

2. 최소 유지 기간:
   - 내부 API: 1~3개월
   - 공개 API: 6~12개월

3. 마이그레이션 가이드 문서 제공

4. 지원 종료 시 410 Gone 반환
```

## 헤더 방식 예시

```
# Accept-Version 헤더
GET /users
Accept-Version: v2

# Content Negotiation
GET /users
Accept: application/vnd.example.v2+json
```

## Related Terms

- [[REST]] — REST API 설계에서 버전 관리는 필수 고려 사항
- [[HTTP-Status-Code]] — 지원 종료 버전: 410 Gone
- [[Swagger]] — OpenAPI로 버전별 스펙 문서화

## References

- [Stripe API Versioning](https://stripe.com/docs/upgrades)
- [Microsoft REST API Guidelines — Versioning](https://github.com/microsoft/api-guidelines/blob/vNext/azure/Guidelines.md#versioning)
