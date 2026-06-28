# DBeaver

> 다중 DB 지원 범용 SQL 클라이언트 도구

## Overview

DBeaver는 MySQL, PostgreSQL, Oracle, SQLite, MongoDB 등 100개 이상의 데이터베이스를 지원하는 오픈소스 DB 관리 도구다. API 개발자는 API 구현 중 DB 데이터 확인·쿼리 튜닝·ERD 파악에 주로 활용한다.

## Key Features

- **다중 DB 연결**: JDBC 기반으로 MySQL, PostgreSQL, Redis, MongoDB 등 동시 연결
- **SQL 편집기**: 자동 완성, 구문 강조, 쿼리 실행 계획(EXPLAIN) 지원
- **ERD 다이어그램**: 테이블 간 관계 시각화 (API 설계 시 리소스 모델링에 유용)
- **데이터 편집기**: 테이블 데이터를 스프레드시트처럼 직접 편집
- **데이터 내보내기**: CSV, JSON, SQL INSERT 형식으로 내보내기
- **SSH 터널**: 운영 DB에 SSH 터널로 안전하게 접속

## Installation & Setup

```
1. https://dbeaver.io/download/ 에서 Community Edition 설치
2. 새 연결 → DB 유형 선택
3. Host / Port / Database / Username / Password 입력
4. Test Connection → 성공 시 Finish
```

## Common Usage (API 개발자 관점)

### 1. API 응답 데이터 검증
```sql
-- API가 반환한 userId로 실제 DB 데이터 확인
SELECT * FROM users WHERE id = 123;

-- API 집계 결과 수동 검증
SELECT status, COUNT(*) FROM orders GROUP BY status;
```

### 2. API 성능 튜닝
```sql
-- 실행 계획으로 인덱스 사용 여부 확인
EXPLAIN SELECT * FROM posts WHERE author_id = 1 ORDER BY created_at DESC;
```

### 3. 테스트 데이터 관리
```sql
-- 개발 환경 테스트 데이터 삽입
INSERT INTO users (name, email) VALUES ('테스트유저', 'test@example.com');

-- API 테스트 후 데이터 정리
DELETE FROM orders WHERE user_id = 999;
```

### 4. ERD로 리소스 모델 파악
- `Navigator` → DB 선택 → `ER Diagram` 탭으로 테이블 관계 시각화
- API 엔드포인트 설계 전 데이터 모델 파악에 필수

## Tips & Shortcuts

| 단축키 | 기능 |
|---|---|
| `Ctrl + Enter` | 현재 쿼리 실행 |
| `Ctrl + /` | 주석 토글 |
| `Ctrl + Shift + F` | SQL 포맷팅 |
| `F3` | 쿼리 실행 계획 (Explain) |
| `Ctrl + F` | 결과 내 검색 |
| `Alt + X` | 선택 쿼리 실행 |

## References

- [DBeaver 공식 문서](https://dbeaver.com/docs/dbeaver/)
- [DBeaver GitHub](https://github.com/dbeaver/dbeaver)
