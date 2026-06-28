# Postman

> API 테스트·문서화·자동화 도구

## Overview

Postman은 HTTP API를 시각적으로 테스트하고 문서화할 수 있는 도구다. 서버 개발자가 구현한 API를 개발 중에 빠르게 검증하고, 자동화된 테스트 스크립트를 작성해 회귀 테스트에 활용한다.

## 서버 개발자 관점의 핵심 활용

### 1. 개발 중 API 검증
구현한 API가 의도한 대로 동작하는지 빠르게 확인. curl보다 편리한 UI와 응답 포매팅.

```
Collection: Order API
├── POST /api/auth/login    (인증 토큰 획득)
├── POST /api/orders        (주문 생성)
├── GET  /api/orders/:id    (주문 조회)
├── PUT  /api/orders/:id    (주문 수정)
└── DELETE /api/orders/:id  (주문 취소)
```

### 2. Environment 변수 활용
환경(로컬/개발/운영)별로 다른 설정을 변수로 관리.

```json
// local 환경
{
  "baseUrl": "http://localhost:8080",
  "accessToken": "",          // 로그인 후 자동으로 채워짐
  "testUserId": "100"
}

// dev 환경
{
  "baseUrl": "https://api-dev.example.com",
  "accessToken": "",
  "testUserId": "200"
}
```

요청에서 변수 사용: `{{baseUrl}}/api/orders`

### 3. Pre-request Script로 자동 인증 처리
매 요청마다 수동으로 토큰을 복사하지 않아도 된다. Collection 레벨에서 자동 로그인 스크립트 설정.

```javascript
// Collection > Pre-request Script
const tokenExpiry = pm.environment.get("tokenExpiry");
const now = Date.now();

if (!tokenExpiry || now > parseInt(tokenExpiry)) {
    // 토큰이 없거나 만료되면 자동 로그인
    pm.sendRequest({
        url: pm.environment.get("baseUrl") + "/api/auth/login",
        method: "POST",
        header: { "Content-Type": "application/json" },
        body: {
            mode: "raw",
            raw: JSON.stringify({
                email: pm.environment.get("testEmail"),
                password: pm.environment.get("testPassword")
            })
        }
    }, (err, response) => {
        const token = response.json().accessToken;
        pm.environment.set("accessToken", token);
        pm.environment.set("tokenExpiry", now + 3600000); // 1시간
    });
}
```

요청 헤더: `Authorization: Bearer {{accessToken}}`

### 4. Test Script로 자동 검증

```javascript
// POST /api/orders 의 Tests 탭
// 응답 상태 코드 확인
pm.test("주문 생성 성공: 201", () => {
    pm.response.to.have.status(201);
});

// 응답 구조 확인
pm.test("응답에 orderId 포함", () => {
    const body = pm.response.json();
    pm.expect(body).to.have.property("orderId");
    pm.expect(body.orderId).to.be.a("number");
});

// 다음 요청에서 사용할 값 저장
const orderId = pm.response.json().orderId;
pm.environment.set("lastOrderId", orderId);

// 응답 시간 확인
pm.test("응답 시간 500ms 이하", () => {
    pm.expect(pm.response.responseTime).to.be.below(500);
});
```

### 5. Collection Runner (자동화 테스트)
여러 요청을 순서대로 실행하는 E2E 시나리오 테스트.

```
시나리오: 주문 생성 ~ 완료 플로우
1. POST /auth/login         → 토큰 획득
2. POST /orders             → 주문 생성 (orderId 저장)
3. GET  /orders/{{orderId}} → 주문 조회 확인
4. PUT  /orders/{{orderId}}/confirm → 주문 확인
5. GET  /orders/{{orderId}} → 상태 변경 확인 (CONFIRMED)
```

CLI로도 실행 가능 (CI 파이프라인 통합):
```bash
newman run MyCollection.json -e local.env.json --reporters cli,junit
```

## 팁

- **응답 저장**: 특정 응답을 예시 응답으로 저장해두면 API 문서 자동 생성에 활용
- **Mock Server**: 서버 구현 전 프론트엔드 개발팀에 목 서버 제공 가능
- **공유**: Collection을 팀에 공유하면 신규 팀원의 API 학습 비용 절감
- **.http 파일 대안**: IntelliJ IDEA의 HTTP Client로도 유사한 기능 사용 가능 (버전 관리 유리)

## References

- [Postman 공식 문서](https://learning.postman.com/)
- [Newman - Postman CLI](https://github.com/postmanlabs/newman)
