# REST

## Definition

Roy Fielding이 2000년 박사 논문에서 정의한 HTTP 기반 웹 아키텍처 스타일. Resource(자원)를 URI로 식별하고, HTTP 메서드로 행위를 표현하며, 무상태(Stateless) 통신을 핵심 원칙으로 한다.

## Context / When to Use

- 클라이언트-서버 간 범용 API 설계 시
- HTTP를 전송 프로토콜로 사용하는 모든 웹 API
- GraphQL, gRPC보다 낮은 러닝 커브가 필요한 프로젝트

## 6가지 REST 제약조건

| 제약조건 | 설명 |
|---|---|
| **Client-Server** | UI(클라이언트)와 데이터 저장(서버) 분리 → 독립 진화 |
| **Stateless** | 요청에 필요한 모든 정보 포함, 서버는 세션 저장 안 함 |
| **Cacheable** | 응답에 캐시 가능 여부 명시 (`Cache-Control`) |
| **Uniform Interface** | 일관된 인터페이스: URI 자원 식별, 표현을 통한 조작 |
| **Layered System** | 클라이언트는 중간 서버(프록시, 로드밸런서)를 인식하지 않음 |
| **Code on Demand** | (선택) 서버가 실행 가능한 코드를 클라이언트에 전송 |

## Richardson Maturity Model (성숙도 모델)

| 단계 | 이름 | 특징 | 예시 |
|---|---|---|---|
| **0단계** | The Swamp of POX | HTTP를 터널로만 사용 | `POST /api { "action": "getUser" }` |
| **1단계** | Resources | URI로 자원 식별 | `GET /users/1` |
| **2단계** | HTTP Verbs | HTTP 메서드 의미론 적용 | `DELETE /users/1` → 204 No Content |
| **3단계** | Hypermedia (HATEOAS) | 응답에 다음 가능 행동 링크 포함 | `"links": [{"rel":"self","href":"/users/1"}]` |

대부분의 실무 API는 **2단계**를 목표로 설계한다.

## RESTful 설계 원칙

### URI 명사 사용 (행위는 HTTP 메서드로)
```
✅ GET    /users          → 목록 조회
✅ GET    /users/{id}     → 단건 조회
✅ POST   /users          → 생성
✅ PUT    /users/{id}     → 전체 수정
✅ PATCH  /users/{id}     → 부분 수정
✅ DELETE /users/{id}     → 삭제

❌ GET  /getUsers
❌ POST /users/delete/{id}
❌ POST /createUser
```

### 계층 관계 표현
```
GET /users/{userId}/posts          → 특정 유저의 게시물 목록
GET /users/{userId}/posts/{postId} → 특정 유저의 특정 게시물
POST /users/{userId}/posts         → 특정 유저의 게시물 생성
```

### HTTP 메서드 의미론

| 메서드 | 의미 | 멱등성 | 요청 본문 |
|---|---|---|---|
| GET | 조회 | O | 없음 |
| POST | 생성 | X | 있음 |
| PUT | 전체 교체 | O | 있음 |
| PATCH | 부분 수정 | △ | 있음 |
| DELETE | 삭제 | O | 없음 |

## REST vs GraphQL vs gRPC

| 기준 | REST | GraphQL | gRPC |
|---|---|---|---|
| 프로토콜 | HTTP | HTTP | HTTP/2 |
| 데이터 패칭 | 여러 엔드포인트 | 단일 엔드포인트 | 스트리밍 가능 |
| 오버패칭 | 있음 | 없음 | 없음 |
| 캐싱 | HTTP 캐시 기본 지원 | 복잡 | 어려움 |
| 사용 상황 | 범용 공개 API | 유연한 클라이언트 | MSA 내부 통신 |

## Related Terms

- [[GraphQL]] — REST의 대안 API 쿼리 언어
- [[HTTP-Status-Code]] — REST 응답의 핵심 요소
- [[Idempotency]] — HTTP 메서드별 멱등성 속성
- [[Versioning]] — REST API의 버전 관리 전략

## References

- [Roy Fielding REST 논문](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)
- [RESTful API Design — Google Cloud](https://cloud.google.com/apis/design)
