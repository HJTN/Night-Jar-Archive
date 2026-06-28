# GraphQL

## Definition

Facebook이 2015년 오픈소스로 공개한 API 쿼리 언어이자 런타임. 클라이언트가 필요한 데이터의 구조를 직접 명시하면 서버가 그 구조 그대로 응답한다.

## Context / When to Use

- 클라이언트마다 필요한 데이터가 다른 경우 (모바일 vs 웹)
- Over-fetching(필요 이상 데이터), Under-fetching(데이터 부족)이 반복될 때
- 단일 요청으로 여러 리소스를 한 번에 가져와야 할 때
- 빠른 UI 변경이 잦은 프로덕트 (프론트엔드 주도 개발)

## 핵심 개념

### Schema 정의
```graphql
type User {
  id: ID!
  name: String!
  email: String!
  posts: [Post!]!
}

type Post {
  id: ID!
  title: String!
  author: User!
}

type Query {
  user(id: ID!): User
  posts: [Post!]!
}

type Mutation {
  createPost(title: String!, authorId: ID!): Post!
}

type Subscription {
  postCreated: Post!
}
```

### Query / Mutation / Subscription

| 타입 | 용도 | HTTP 비유 |
|---|---|---|
| **Query** | 데이터 조회 | GET |
| **Mutation** | 데이터 변경 (생성/수정/삭제) | POST/PUT/DELETE |
| **Subscription** | 실시간 데이터 수신 (WebSocket) | Server-Sent Events |

### 요청 예시
```graphql
# Query - 필요한 필드만 선택
query {
  user(id: "1") {
    name
    posts {
      title
    }
  }
}

# Mutation
mutation {
  createPost(title: "GraphQL 정리", authorId: "1") {
    id
    title
  }
}
```

## REST vs GraphQL 비교

| 기준 | REST | GraphQL |
|---|---|---|
| 엔드포인트 수 | 리소스별 다수 | 단일 (`/graphql`) |
| Over-fetching | 발생 가능 | 없음 (필드 선택) |
| Under-fetching | 발생 가능 (여러 요청 필요) | 없음 (중첩 쿼리) |
| HTTP 캐싱 | 기본 지원 | 복잡 (POST 요청) |
| 러닝 커브 | 낮음 | 높음 |
| 버전 관리 | URI 버전(`/v1/`) | 스키마 진화 (Deprecation) |
| 사용 상황 | 범용 API | 유연한 클라이언트 요구 |

## N+1 문제와 DataLoader

**문제**: 게시물 목록(1회 쿼리) → 각 게시물의 작성자 조회(N회 쿼리) = 총 N+1회

```
# N+1 발생 예시
posts → [post1, post2, post3]
         ↓       ↓       ↓
       user1   user2   user3   (각각 DB 쿼리)
```

**DataLoader 해결책**: 요청을 배치로 묶어 단 1회 쿼리
```javascript
const userLoader = new DataLoader(async (userIds) => {
  // userIds = [1, 2, 3] → SELECT * FROM users WHERE id IN (1,2,3)
  return await User.findByIds(userIds);
});
```

## Related Terms

- [[REST]] — GraphQL의 대안 아키텍처, 비교 기준
- [[HTTP-Status-Code]] — GraphQL은 보통 200으로 에러도 응답
- [[Versioning]] — GraphQL은 스키마 Deprecation으로 버전 관리

## References

- [GraphQL 공식 문서](https://graphql.org/learn/)
- [GraphQL vs REST](https://www.apollographql.com/blog/graphql-vs-rest)
