# JWT (JSON Web Token)

## Definition

서버-클라이언트 간 인증 정보를 JSON으로 서명·전달하는 토큰 방식. 서버가 상태를 저장하지 않아도(Stateless) 토큰 자체로 인증을 검증할 수 있다.

## 구조: Header.Payload.Signature

JWT는 Base64URL 인코딩된 3개 파트가 `.`으로 구분된 문자열이다.

```
eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1c2VyMTIzIn0.abc123signature
     [Header]               [Payload]           [Signature]
```

### Header
```json
{
  "alg": "HS256",   // 서명 알고리즘 (HS256, RS256, ES256)
  "typ": "JWT"
}
```

### Payload (Claims)
```json
{
  "sub": "user123",          // Subject (사용자 식별자)
  "iss": "auth-service",     // Issuer (발급자)
  "aud": "api-service",      // Audience (수신자)
  "exp": 1719500000,         // Expiration (만료 시각, Unix timestamp)
  "iat": 1719496400,         // Issued At (발급 시각)
  "jti": "uuid-...",         // JWT ID (고유 식별자)
  "roles": ["USER", "ADMIN"] // Custom Claim (비즈니스 데이터)
}
```

**Claims 종류**:
- **Registered Claims**: `sub`, `iss`, `aud`, `exp`, `iat`, `jti` 등 표준 정의
- **Public Claims**: IANA에 등록된 공개 클레임
- **Private Claims**: 발급자/수신자가 합의해서 사용하는 커스텀 클레임

### Signature
```
HMACSHA256(
  base64UrlEncode(header) + "." + base64UrlEncode(payload),
  secretKey
)
```
서명으로 토큰 위변조 여부를 검증. 서버는 시크릿 키로 서명을 재계산해 검증한다.

## Access Token + Refresh Token 패턴

JWT를 단독으로 사용하면 토큰 탈취 시 만료 전까지 막을 방법이 없다. 이를 보완하기 위해 두 토큰을 조합한다.

```
[로그인]
클라이언트 → 서버: ID/PW
서버 → 클라이언트: Access Token (만료: 15분~1시간)
                   Refresh Token (만료: 7일~30일, DB/Redis에 저장)

[API 요청]
클라이언트 → 서버: Authorization: Bearer {AccessToken}

[Access Token 만료 후]
클라이언트 → 서버: Refresh Token으로 재발급 요청
서버: Refresh Token 유효성 검증 (DB/Redis에 저장된 값과 비교)
서버 → 클라이언트: 새 Access Token (+ 새 Refresh Token)

[로그아웃]
서버: DB/Redis에서 Refresh Token 삭제
```

| 토큰 | 만료 시간 | 저장 위치 (클라이언트) | 목적 |
|------|----------|---------------------|------|
| Access Token | 15분~1시간 | 메모리 (또는 LocalStorage) | API 인증 |
| Refresh Token | 7일~30일 | HttpOnly Cookie | Access Token 재발급 |

## 보안 주의사항

### 1. 알고리즘 none 공격
일부 라이브러리에서 `alg: "none"`을 허용하면, 공격자가 서명 없는 토큰을 만들어 인증 우회 가능.

```java
// 반드시 허용 알고리즘을 명시적으로 지정
Jwts.parserBuilder()
    .requireAlgorithm("HS256") // none 허용 방지
    .setSigningKey(secretKey)
    .build()
    .parseClaimsJws(token);
```

### 2. 민감 정보 포함 금지
Payload는 Base64URL **인코딩**만 되어 있고 **암호화되지 않음**. 누구나 디코딩해 내용을 볼 수 있다.

- 포함하면 안 되는 것: 비밀번호, 신용카드 번호, 주민등록번호
- 포함해도 되는 것: 사용자 ID, 역할(role), 권한(permission)

### 3. 토큰 탈취 대비
- Access Token은 수명을 짧게 유지
- Refresh Token은 HttpOnly, Secure, SameSite 쿠키에 저장 (XSS 방지)
- HTTPS만 사용

## 토큰 무효화 방법

JWT는 발급 후 서버가 강제로 무효화할 수 없다는 한계가 있다.

| 방법 | 설명 | 트레이드오프 |
|------|------|------------|
| 짧은 Access Token 수명 | 탈취돼도 짧은 시간만 유효 | 재발급 요청 빈도 증가 |
| Refresh Token 블랙리스트 | Redis에 무효화된 jti 저장 | Stateless 이점 일부 포기 |
| Refresh Token DB 저장 | 로그아웃 시 DB에서 삭제 | DB 조회 필요 (Stateful화) |
| 버전 관리 (tokenVersion) | 사용자 엔티티에 버전 필드, JWT에 버전 포함 | 모든 요청에 DB 조회 필요 |

## Related Terms

- [[Middleware]] - JWT 검증은 보통 인증 미들웨어/필터에서 처리
- [[Caching]] - Refresh Token 저장소로 Redis 활용

## References

- [JWT 공식 사이트](https://jwt.io/)
- [OWASP JWT Security](https://cheatsheetseries.owasp.org/cheatsheets/JSON_Web_Token_for_Java_Cheat_Sheet.html)
