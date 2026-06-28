# IntelliJ IDEA

> JetBrains의 Java/Kotlin/Spring 전용 IDE

## Overview

IntelliJ IDEA는 Java·Kotlin·Spring Boot API 개발에 최적화된 IDE다. 강력한 코드 인텔리전스, 내장 HTTP Client, Spring 통합, 데이터베이스 도구를 제공한다. API 개발자는 코드 작성부터 API 테스트까지 IDE 하나로 처리할 수 있다.

## Key Features

- **Smart Code Completion**: Spring Bean, JPA Repository 메서드 자동 완성
- **내장 HTTP Client**: `.http` 파일로 API 요청 직접 실행 (Postman 대체 가능)
- **Database 도구**: IDE 내에서 DB 연결 및 쿼리 실행
- **Spring Boot 지원**: 컨텍스트 인식 자동 완성, Bean 의존성 다이어그램
- **리팩토링 도구**: 안전한 이름 변경, 메서드 추출, 인라인
- **Git 통합**: IDE 내 커밋·PR·브랜치 관리

## Installation & Setup

```
1. https://www.jetbrains.com/idea/ 에서 Ultimate 버전 설치
   (Community는 Spring 지원 제한)
2. Spring Boot 프로젝트: File → New → Project → Spring Initializr
3. SDK 설정: File → Project Structure → SDK → JDK 21 선택
```

## Common Usage (API 개발자 관점)

### 내장 HTTP Client로 API 테스트

`src/test/http/` 디렉토리에 `.http` 파일 생성:

```http
### 사용자 목록 조회
GET http://localhost:8080/v1/users?page=0&size=10
Authorization: Bearer {{auth_token}}
Accept: application/json

### 사용자 생성
POST http://localhost:8080/v1/users
Content-Type: application/json

{
  "name": "홍길동",
  "email": "hong@example.com"
}

### 환경변수 설정 (http-client.env.json)
# {
#   "dev": { "auth_token": "eyJ...", "baseUrl": "http://localhost:8080" }
# }
```

### Spring Boot API 개발 플로우
```
1. Controller 생성: Alt+Insert → Create Class
2. @RestController, @RequestMapping 자동 완성
3. Service, Repository 레이어 생성
4. Run (Shift+F10) → 내장 HTTP Client로 테스트
5. 디버그 (Shift+F9) → 브레이크포인트로 요청 흐름 추적
```

## Tips & Shortcuts

| 단축키 | 기능 |
|---|---|
| `Shift + Shift` | 전체 검색 (클래스·파일·심볼·액션) |
| `Ctrl + B` | 선언부로 이동 (메서드·클래스) |
| `Ctrl + Alt + L` | 코드 자동 포맷팅 |
| `Shift + F10` | 실행 |
| `Shift + F9` | 디버그 실행 |
| `Ctrl + Shift + F9` | 현재 파일 재컴파일 (Hot Reload) |
| `Alt + Enter` | Quick Fix (import 추가, 오류 수정) |
| `Ctrl + E` | 최근 파일 목록 |
| `Ctrl + Alt + B` | 구현체로 이동 (인터페이스 → 구현 클래스) |
| `Ctrl + P` | 메서드 파라미터 힌트 |

## 유용한 플러그인

| 플러그인 | 용도 |
|---|---|
| **Spring Boot Assistant** | 기본 내장, `application.yml` 자동완성 |
| **Lombok** | `@Getter/@Setter/@Builder` 코드 생성 인식 |
| **SonarLint** | 코드 품질 정적 분석 |
| **Rainbow Brackets** | 중첩 괄호 색상 구분 |
| **Key Promoter X** | 마우스 동작 → 단축키 알림 |

## References

- [IntelliJ IDEA 공식 문서](https://www.jetbrains.com/help/idea/)
- [IntelliJ HTTP Client 가이드](https://www.jetbrains.com/help/idea/http-client-in-product-code-editor.html)
