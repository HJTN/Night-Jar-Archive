# Postman

> API 테스트·문서화·자동화 도구

## Overview

Postman은 API를 GUI로 요청하고 응답을 확인할 수 있는 API 플랫폼이다. API 개발자는 구현 중 빠른 테스트, 팀과의 Collection 공유, CI/CD 연동 자동화 테스트까지 활용한다.

## Key Features

- **Collection**: 관련 API 요청을 폴더 구조로 묶어 관리 및 팀 공유
- **Environment**: dev/staging/prod 환경변수 분리 (`{{baseUrl}}`, `{{token}}`)
- **Pre-request Script**: 요청 전 토큰 자동 갱신 등 JavaScript로 사전 처리
- **Test Script**: 응답 후 자동 검증 (상태 코드, 응답 필드 확인)
- **Mock Server**: 실제 서버 없이 Collection으로 Mock API 생성
- **Newman**: CLI로 Collection을 CI/CD 파이프라인에서 실행

## Installation & Setup

```
1. https://www.postman.com/downloads/ 에서 Postman 설치
2. 계정 생성 (무료) → 팀 워크스페이스 사용 가능
3. Collection 생성: New → Collection
4. Environment 생성: Environments → Add
```

## Common Usage (API 개발 워크플로우)

### Environment 변수 설정

```json
// dev 환경
{
  "baseUrl": "http://localhost:8080",
  "token": "",
  "userId": "1"
}

// staging 환경
{
  "baseUrl": "https://api-staging.example.com",
  "token": "",
  "userId": "100"
}
```

### Pre-request Script — 토큰 자동 갱신

```javascript
// 요청 전 실행: 토큰 만료 시 자동으로 재발급
const tokenExpiry = pm.environment.get("tokenExpiry");
const now = Date.now();

if (!tokenExpiry || now > parseInt(tokenExpiry)) {
    pm.sendRequest({
        url: pm.environment.get("baseUrl") + "/v1/auth/token",
        method: "POST",
        header: { "Content-Type": "application/json" },
        body: {
            mode: "raw",
            raw: JSON.stringify({
                username: pm.environment.get("username"),
                password: pm.environment.get("password")
            })
        }
    }, (err, res) => {
        const json = res.json();
        pm.environment.set("token", json.accessToken);
        pm.environment.set("tokenExpiry", now + 15 * 60 * 1000); // 15분
    });
}
```

### Test Script — 자동 검증

```javascript
// 응답 후 실행: 테스트 자동화
pm.test("상태 코드 200", () => {
    pm.response.to.have.status(200);
});

pm.test("응답에 userId 필드 존재", () => {
    const json = pm.response.json();
    pm.expect(json).to.have.property("userId");
});

pm.test("응답 시간 500ms 이하", () => {
    pm.expect(pm.response.responseTime).to.be.below(500);
});

// 다음 요청에서 사용할 변수 저장
const json = pm.response.json();
pm.environment.set("createdUserId", json.userId);
```

### Newman으로 CI/CD 연동

```bash
# Collection 내보내기 후 실행
npm install -g newman
newman run collection.json \
  --environment staging.json \
  --reporters cli,junit \
  --reporter-junit-export results.xml
```

## Tips & Shortcuts

| 단축키 | 기능 |
|---|---|
| `Ctrl + Enter` | 요청 전송 |
| `Ctrl + S` | 요청 저장 |
| `Ctrl + /` | Request URL 포커스 |
| `Ctrl + Alt + C` | 요청을 cURL로 변환 |

- **Collection Runner**: 폴더 전체 요청 순서대로 실행, 통합 테스트에 활용
- **Visualize**: 응답을 테이블·차트로 시각화
- `{{$randomEmail}}`, `{{$randomUUID}}` 등 내장 동적 변수 활용

## References

- [Postman 공식 문서](https://learning.postman.com/docs/)
- [Newman GitHub](https://github.com/postmanlabs/newman)
