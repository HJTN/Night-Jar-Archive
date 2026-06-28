# API 설계 문서 템플릿

> OpenAPI 스펙 작성 전, 팀과 합의할 API 설계 문서 템플릿. 아래 내용을 채워 이해관계자 리뷰 후 OpenAPI YAML로 변환한다.

---

## 1. API 개요

| 항목 | 내용 |
|---|---|
| **API 명** | (예: 사용자 관리 API) |
| **버전** | v1 |
| **Base URL** | `https://api.example.com/v1` |
| **담당자** | |
| **작성일** | YYYY-MM-DD |
| **상태** | Draft / In Review / Confirmed |

### 목적

(이 API가 해결하는 문제나 제공하는 기능을 2~3문장으로 설명)

### 대상 클라이언트

- [ ] iOS 앱
- [ ] Android 앱
- [ ] 웹 프론트엔드
- [ ] 외부 파트너
- [ ] 내부 서비스

---

## 2. 인증 방식

| 방식 | 설명 |
|---|---|
| **인증 유형** | Bearer Token (JWT) / API Key / 없음 |
| **헤더** | `Authorization: Bearer {token}` |
| **토큰 만료** | Access: 15분 / Refresh: 7일 |
| **토큰 갱신** | `POST /v1/auth/refresh` |

---

## 3. 공통 응답 구조

### 성공 응답
```json
{
  "data": { ... },
  "meta": {
    "requestId": "uuid"
  }
}
```

### 에러 응답
```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "사람이 읽을 수 있는 오류 메시지",
    "details": { }
  }
}
```

### 에러 코드 목록
| 코드 | HTTP 상태 | 설명 |
|---|---|---|
| `RESOURCE_NOT_FOUND` | 404 | 요청한 리소스 없음 |
| `UNAUTHORIZED` | 401 | 인증 토큰 없음·만료 |
| `FORBIDDEN` | 403 | 권한 없음 |
| `VALIDATION_ERROR` | 422 | 입력값 유효성 실패 |
| `RATE_LIMIT_EXCEEDED` | 429 | Rate Limit 초과 |

---

## 4. 엔드포인트 목록

| # | 메서드 | URI | 설명 | 인증 |
|---|---|---|---|---|
| 1 | GET | `/resources` | 목록 조회 | 필요 |
| 2 | GET | `/resources/{id}` | 단건 조회 | 필요 |
| 3 | POST | `/resources` | 생성 | 필요 |
| 4 | PUT | `/resources/{id}` | 전체 수정 | 필요 |
| 5 | PATCH | `/resources/{id}` | 부분 수정 | 필요 |
| 6 | DELETE | `/resources/{id}` | 삭제 | 필요 |

---

## 5. 엔드포인트 상세

### 5.1 목록 조회

**`GET /v1/resources`**

**Query Parameters**

| 파라미터 | 타입 | 필수 | 기본값 | 설명 |
|---|---|---|---|---|
| `page` | integer | N | 0 | 페이지 번호 (0부터 시작) |
| `size` | integer | N | 20 | 페이지 크기 (최대 100) |
| `sort` | string | N | `createdAt,desc` | 정렬 기준 |
| `status` | string | N | - | 상태 필터 (`active` / `inactive`) |

**응답 예시 (200 OK)**
```json
{
  "data": [
    {
      "id": 1,
      "name": "예시 항목",
      "status": "active",
      "createdAt": "2026-06-28T10:00:00Z"
    }
  ],
  "pagination": {
    "page": 0,
    "size": 20,
    "totalCount": 152,
    "totalPages": 8
  }
}
```

---

### 5.2 단건 조회

**`GET /v1/resources/{id}`**

**Path Parameters**

| 파라미터 | 타입 | 설명 |
|---|---|---|
| `id` | integer | 리소스 ID |

**응답 예시 (200 OK)**
```json
{
  "data": {
    "id": 1,
    "name": "예시 항목",
    "description": "상세 설명",
    "status": "active",
    "createdAt": "2026-06-28T10:00:00Z",
    "updatedAt": "2026-06-28T12:00:00Z"
  }
}
```

**에러 응답 (404 Not Found)**
```json
{
  "error": {
    "code": "RESOURCE_NOT_FOUND",
    "message": "요청한 리소스를 찾을 수 없습니다.",
    "details": { "id": 999 }
  }
}
```

---

### 5.3 생성

**`POST /v1/resources`**

**Request Body** (`Content-Type: application/json`)

| 필드 | 타입 | 필수 | 제약 조건 | 설명 |
|---|---|---|---|---|
| `name` | string | Y | 1~100자 | 항목 이름 |
| `description` | string | N | 최대 500자 | 상세 설명 |
| `status` | string | N | `active`/`inactive` | 상태 (기본: `active`) |

**요청 예시**
```json
{
  "name": "새 항목",
  "description": "항목 설명",
  "status": "active"
}
```

**응답 예시 (201 Created)**
```
Location: /v1/resources/42
```
```json
{
  "data": {
    "id": 42,
    "name": "새 항목",
    "status": "active",
    "createdAt": "2026-06-28T10:00:00Z"
  }
}
```

---

### 5.4 부분 수정

**`PATCH /v1/resources/{id}`**

**Request Body** (변경할 필드만 포함)

```json
{
  "name": "수정된 이름"
}
```

**응답 예시 (200 OK)**: 수정된 전체 리소스 반환

---

### 5.5 삭제

**`DELETE /v1/resources/{id}`**

**응답**: `204 No Content` (본문 없음)

멱등 설계: 이미 삭제된 리소스에 재요청 시 `404` 또는 `204` 반환 (팀 정책에 따라 결정)

---

## 6. Rate Limiting

| 구분 | 제한 |
|---|---|
| 인증 사용자 | 분당 1,000건 |
| 미인증 요청 | 분당 100건 |
| 응답 헤더 | `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset` |

---

## 7. 변경 이력

| 버전 | 날짜 | 변경 내용 | 작성자 |
|---|---|---|---|
| 1.0.0 | YYYY-MM-DD | 최초 작성 | |

---

## 8. 리뷰 체크리스트

- [ ] 프론트엔드/앱 개발자 리뷰 완료
- [ ] 백엔드 팀 리뷰 완료
- [ ] 보안 검토 완료 ([[API-Review-Checklist]] 참조)
- [ ] OpenAPI YAML 변환 예정일: YYYY-MM-DD
