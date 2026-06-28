# Visual Studio Code

> 마이크로소프트의 경량 코드 에디터

## Overview

VS Code는 가볍고 빠른 코드 에디터로, 풍부한 확장 생태계를 통해 다양한 언어와 프레임워크를 지원한다. Java/Spring 개발에는 IntelliJ IDEA가 강력하지만, Node.js·Python·Go 서버 개발이나 설정 파일 편집, API 테스트에는 VS Code가 생산적이다.

## 서버 개발 관련 핵심 단축키

| 단축키 (Mac / Win) | 동작 |
|-------------------|------|
| `Cmd+P` / `Ctrl+P` | 파일 빠른 열기 |
| `Cmd+Shift+P` / `Ctrl+Shift+P` | 명령 팔레트 |
| `Cmd+Shift+F` / `Ctrl+Shift+F` | 전체 검색 |
| `Cmd+B` / `Ctrl+B` | 사이드바 토글 |
| `` Ctrl+` `` | 내장 터미널 열기 |
| `Cmd+D` / `Ctrl+D` | 다음 동일 단어 선택 (멀티 커서) |
| `Alt+↑/↓` | 현재 줄 위/아래로 이동 |
| `Cmd+/` / `Ctrl+/` | 라인 주석 토글 |
| `F12` | 정의로 이동 |
| `Shift+F12` | 모든 참조 찾기 |

## 서버 개발 유용한 확장

### REST API 테스트
**REST Client** (`humao.rest-client`)
`.http` 파일에 HTTP 요청을 작성하고 직접 실행. 버전 관리가 가능해 팀과 공유하기 좋다.

```http
### 로그인
@baseUrl = http://localhost:8080

POST {{baseUrl}}/api/auth/login
Content-Type: application/json

{
  "email": "test@example.com",
  "password": "password123"
}

### 주문 생성
@token = eyJhbGciOiJIUzI1NiJ9...

POST {{baseUrl}}/api/orders
Content-Type: application/json
Authorization: Bearer {{token}}

{
  "productId": 1,
  "quantity": 2
}

### 주문 조회
GET {{baseUrl}}/api/orders/1
Authorization: Bearer {{token}}
```

### Docker 관리
**Docker** (`ms-azuretools.vscode-docker`)
- 컨테이너/이미지 목록 시각화
- docker-compose 파일 자동 완성
- 컨테이너 로그 확인 및 셸 접속 (GUI)

### 코드 품질
| 확장 | 언어 | 기능 |
|------|------|------|
| **ESLint** | JavaScript/TypeScript | 코드 스타일 실시간 검사 |
| **Pylint / Ruff** | Python | 린팅 및 포매팅 |
| **Go** (`golang.go`) | Go | 자동 완성, 린팅, 테스트 |
| **SonarLint** | 다중 언어 | 보안 취약점 실시간 분석 |
| **Error Lens** | 다중 언어 | 에러 메시지를 코드 라인에 인라인 표시 |

### YAML/JSON/환경 설정
- **YAML** (`redhat.vscode-yaml`): Kubernetes, docker-compose YAML 자동 완성 및 유효성 검사
- **DotENV** (`mikestead.dotenv`): `.env` 파일 신택스 하이라이팅
- **Thunder Client**: Postman 대안 (VS Code 내장 GUI API 테스트)

## settings.json 유용한 설정

```json
{
  // 저장 시 자동 포매팅
  "editor.formatOnSave": true,
  
  // 저장 시 import 정리 (TypeScript)
  "editor.codeActionsOnSave": {
    "source.organizeImports": "explicit"
  },
  
  // 터미널 기본 셸 (Windows에서 Git Bash 사용)
  "terminal.integrated.defaultProfile.windows": "Git Bash",
  
  // 파일 자동 저장 (포커스 잃을 때)
  "files.autoSave": "onFocusChange",
  
  // 탭 사이즈
  "editor.tabSize": 2,
  
  // 미니맵 숨기기 (화면 공간 확보)
  "editor.minimap.enabled": false,
  
  // 브래킷 쌍 색상 강조
  "editor.bracketPairColorization.enabled": true,
  
  // 언어별 포매터 지정
  "[python]": {
    "editor.defaultFormatter": "charliermarsh.ruff"
  },
  "[go]": {
    "editor.defaultFormatter": "golang.go"
  }
}
```

## 내장 터미널 활용

VS Code에서 `` Ctrl+` ``로 터미널을 열면 현재 프로젝트 디렉토리에서 바로 시작된다. 분할 터미널로 서버 실행 + 로그 확인을 동시에 할 수 있다.

```bash
# 터미널 1: 서버 실행
npm run dev

# 터미널 2: API 테스트
curl -X POST http://localhost:3000/api/orders -H "Content-Type: application/json" -d '{}'
```

## References

- [VS Code 공식 문서](https://code.visualstudio.com/docs)
- [REST Client 확장](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)
