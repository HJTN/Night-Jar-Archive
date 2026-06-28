# Pagination (페이지네이션)

## Definition

수백만 건의 데이터를 한 번에 반환하지 않고 페이지 단위로 나눠 반환하는 기법. 응답 속도·메모리·네트워크 대역폭을 절약한다.

## Context / When to Use

- 목록 조회 API에서 데이터가 수십 건 이상일 때
- 무한 스크롤, 더보기 버튼, 페이지 번호 UI를 지원할 때
- DB 풀 스캔을 방지하고 응답 시간을 일정하게 유지할 때

## 방식별 비교

| 방식 | 파라미터 예시 | 동작 방식 | 장점 | 단점 |
|---|---|---|---|---|
| **Offset** | `?page=2&size=20` | `LIMIT 20 OFFSET 40` | 구현 단순, 임의 페이지 이동 가능 | 데이터 삽입 시 중복·누락 발생, 깊은 페이지 느림 |
| **Cursor** | `?cursor=eyJ...&size=20` | `WHERE id > cursor LIMIT 20` | 실시간 데이터에서 안정적, 성능 일정 | 임의 페이지 이동 불가 |
| **Keyset** | `?after_id=100&size=20` | `WHERE id > 100 LIMIT 20` | Cursor와 유사, 인덱스 활용 효율적 | 정렬 기준 변경 어려움 |

## Offset 기반 (전통적 방식)

```
GET /posts?page=1&size=10
GET /posts?page=2&size=10

# 응답
{
  "data": [...],
  "pagination": {
    "page": 2,
    "size": 10,
    "totalCount": 1532,
    "totalPages": 154
  }
}
```

**문제점**: page=1000 이상에서 `OFFSET 10000`은 DB가 10000개를 읽고 버리므로 느림.

## Cursor 기반 (무한 스크롤 권장)

```
# 첫 요청
GET /posts?size=10

# 응답
{
  "data": [...],
  "pagination": {
    "nextCursor": "eyJpZCI6MTAwfQ==",  ← Base64({"id":100})
    "hasNext": true
  }
}

# 다음 페이지
GET /posts?cursor=eyJpZCI6MTAwfQ==&size=10
```

**장점**: 데이터가 실시간으로 추가·삭제되어도 중복·누락 없음.

## 대용량 데이터 권장 방식

```
데이터 < 10만 건, 관리자 페이지, 임의 이동 필요
  → Offset 페이지네이션

실시간 피드, 무한 스크롤, 수백만 건 이상
  → Cursor / Keyset 페이지네이션
```

## 응답 링크 헤더 (Link Header)

RFC 5988 표준을 따르는 방식:
```
Link: <https://api.example.com/posts?page=3>; rel="next",
      <https://api.example.com/posts?page=154>; rel="last",
      <https://api.example.com/posts?page=1>; rel="first",
      <https://api.example.com/posts?page=1>; rel="prev"
```

## Related Terms

- [[REST]] — RESTful API에서 컬렉션 리소스 반환 시 필수
- [[HTTP-Status-Code]] — 빈 페이지 요청 시 200 vs 204 선택
- [[Rate-Limiting]] — 페이지 요청도 Rate Limit 대상

## References

- [Cursor-based Pagination — Slack API](https://api.slack.com/docs/pagination)
- [GitHub REST API Pagination](https://docs.github.com/en/rest/using-the-rest-api/using-pagination-in-the-rest-api)
