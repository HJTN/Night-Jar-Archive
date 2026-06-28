# IntelliJ IDEA

> JetBrains의 Java/Kotlin IDE

## Overview

Java·Kotlin·Spring Boot 개발에 가장 널리 쓰이는 IDE. 강력한 코드 분석, 리팩토링, 디버거, Spring 프레임워크 지원으로 서버 개발자의 생산성을 크게 높인다.

## 서버 개발 핵심 단축키

### 탐색 (Navigation)
| 단축키 (Mac / Win) | 동작 |
|-------------------|------|
| `Cmd+Shift+O` / `Ctrl+Shift+N` | 파일명으로 빠른 파일 열기 |
| `Cmd+O` / `Ctrl+N` | 클래스명으로 빠른 탐색 |
| `Cmd+Shift+A` / `Ctrl+Shift+A` | 액션 검색 (모르는 단축키 찾기) |
| `Cmd+B` / `Ctrl+B` | 선언부로 이동 (Go to Definition) |
| `Cmd+Alt+B` / `Ctrl+Alt+B` | 구현체로 이동 (인터페이스 → 구현 클래스) |
| `Cmd+E` / `Ctrl+E` | 최근 파일 목록 |
| `Cmd+Shift+E` / `Ctrl+Shift+E` | 최근 위치 목록 |
| `F2` | 다음 에러/경고로 이동 |

### 편집 (Editing)
| 단축키 | 동작 |
|--------|------|
| `Cmd+D` / `Ctrl+D` | 현재 줄 복사 |
| `Cmd+Delete` / `Ctrl+Y` | 현재 줄 삭제 |
| `Cmd+/` / `Ctrl+/` | 라인 주석 토글 |
| `Alt+Enter` | 빠른 수정 (Quick Fix) |
| `Ctrl+Shift+Space` | 스마트 자동 완성 |
| `Cmd+Alt+L` / `Ctrl+Alt+L` | 코드 포매팅 |
| `Cmd+Alt+O` / `Ctrl+Alt+O` | import 정리 |
| `Shift+F6` | 이름 변경 (Rename Refactoring) |
| `Cmd+Alt+M` / `Ctrl+Alt+M` | 메서드 추출 |

### 실행 및 디버그
| 단축키 | 동작 |
|--------|------|
| `Ctrl+R` (Mac) / `Shift+F10` (Win) | 현재 설정으로 실행 |
| `Ctrl+D` (Mac) / `Shift+F9` (Win) | 디버그 모드 실행 |
| `F8` | Step Over (다음 줄로) |
| `F7` | Step Into (메서드 내부로) |
| `Shift+F8` | Step Out (현재 메서드 밖으로) |
| `F9` | Resume (다음 브레이크포인트까지 실행) |
| `Cmd+F8` / `Ctrl+F8` | 브레이크포인트 토글 |

## 디버거 활용

### 조건부 브레이크포인트
브레이크포인트에 우클릭 → Condition 설정. 특정 조건일 때만 중단.
```java
// 예: userId == 100 일 때만 중단
orderId > 1000 && user.isAdmin()
```

### Evaluate Expression
디버그 중 `Alt+F8`로 표현식 즉시 평가. 변수 상태 확인이나 메서드 호출 테스트에 유용.

### Watch
변수 또는 표현식의 값을 지속적으로 모니터링. 복잡한 객체의 특정 필드 추적에 유용.

## Spring Boot Run/Debug 설정

1. `Run → Edit Configurations → Add → Spring Boot`
2. **Main class**: 애플리케이션 메인 클래스 지정
3. **Active profiles**: `local`, `dev` 등 프로파일 지정
4. **Environment variables**: `DB_PASSWORD=...` 등 환경변수 설정 (소스 코드에 하드코딩 방지)
5. **VM Options**: `-Xmx512m -Xms256m` 등 JVM 옵션

```
Run Configuration 예시:
  Main class: com.example.MyApplication
  Active profiles: local
  Environment variables: DB_HOST=localhost;REDIS_HOST=localhost
```

## 유용한 플러그인

| 플러그인 | 용도 |
|---------|------|
| **Lombok** | `@Getter/@Setter/@Builder` 어노테이션 IDE 지원 |
| **Spring Boot Assistant** | `application.yml` 자동 완성 |
| **SonarLint** | 코드 품질 및 보안 취약점 실시간 분석 |
| **GitToolBox** | 인라인 Git blame 표시 |
| **Database Navigator** | 내장 DB 클라이언트 (쿼리 실행, 스키마 탐색) |
| **HTTP Client** | IntelliJ 내장 REST API 테스트 (`.http` 파일) |
| **Grep Console** | 로그 콘솔 필터링 및 컬러링 |

## Tips

- **Live Templates**: 자주 쓰는 코드 스니펫 등록 (`Settings → Live Templates`). `psvm`, `sout` 같은 기본 템플릿 외에 팀 공통 패턴을 등록
- **File and Code Templates**: 새 파일 생성 시 기본 템플릿 (저작권 헤더 등)
- **Local History**: Git 커밋 없이도 로컬에서 파일 변경 이력 확인 가능 (`Right-click → Local History`)
- **.http 파일**: HTTP Client 플러그인으로 Postman 없이 IDE 내에서 API 테스트

## References

- [IntelliJ IDEA 단축키 (공식)](https://www.jetbrains.com/help/idea/reference-keymap-mac-default.html)
- [IntelliJ IDEA Tips & Tricks](https://www.jetbrains.com/idea/guide/)
