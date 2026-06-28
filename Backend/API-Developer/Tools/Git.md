# Git

> 분산 버전 관리 시스템

## Overview

Git은 소스코드 변경 이력을 추적하고 협업을 지원하는 분산 버전 관리 시스템이다. API 개발에서는 기능 브랜치로 개발하고, PR(Pull Request) 리뷰를 통해 API 설계 검증 후 메인 브랜치에 병합하는 방식으로 사용한다.

## Key Features

- **브랜치**: 기능·버그 수정 단위로 독립 작업 공간 생성
- **커밋**: 변경 이력을 스냅샷으로 저장
- **PR(Pull Request)**: 코드 리뷰 및 병합 요청, API 설계 피드백 받는 핵심 채널
- **태그**: 버전 릴리스 지점 표시 (`v1.2.0`)
- **Stash**: 미완성 변경사항을 임시 저장

## Installation & Setup

```bash
# Git 설치 확인
git --version

# 초기 설정
git config --global user.name "이름"
git config --global user.email "email@example.com"
git config --global core.editor "code --wait"   # VS Code 기본 에디터
```

## Common Usage (API 개발자 브랜치 전략)

### 브랜치 명명 규칙

```
feature/  → 새 기능, 새 API 엔드포인트
  feature/add-user-profile-api
  feature/graphql-schema-v2

fix/      → 버그 수정
  fix/pagination-offset-calculation

refactor/ → 리팩토링 (기능 변경 없음)
  refactor/extract-auth-middleware

release/  → 릴리스 준비 브랜치
  release/v2.1.0
```

### 일반적인 작업 흐름

```bash
# 1. 최신 main 기준으로 기능 브랜치 생성
git checkout main && git pull origin main
git checkout -b feature/add-payment-api

# 2. 개발 후 스테이징
git add src/main/java/com/example/payment/

# 3. Conventional Commits 형식으로 커밋
git commit -m "feat(payment): POST /payments 엔드포인트 추가"

# 4. 원격 푸시 후 PR 생성
git push origin feature/add-payment-api
```

### Conventional Commits

```
<type>(<scope>): <description>

type:
  feat     → 새 기능 (새 API 엔드포인트)
  fix      → 버그 수정
  docs     → 문서 변경 (OpenAPI 스펙 수정)
  refactor → 리팩토링
  test     → 테스트 추가/수정
  chore    → 빌드, 설정 변경

예시:
  feat(users): GET /users/{id} 조회 API 추가
  fix(auth): JWT 만료 시간 검증 로직 수정
  docs(openapi): /orders 엔드포인트 스펙 업데이트
```

### 주요 명령어

```bash
git status                    # 작업 트리 상태 확인
git diff                      # 스테이징 전 변경 확인
git log --oneline --graph     # 커밋 히스토리 그래프
git stash                     # 변경사항 임시 저장
git stash pop                 # 임시 저장 복원
git rebase main               # main 기준으로 커밋 재배치
git cherry-pick <hash>        # 특정 커밋만 가져오기
```

## Tips & Shortcuts

- PR 설명에 변경된 API 엔드포인트 목록, 테스트 방법 명시 → 리뷰 속도 향상
- `.gitignore`에 `application-local.yml`, `.env` 포함 → 비밀 정보 유출 방지
- `git rebase -i HEAD~3`으로 커밋 정리 후 PR (WIP 커밋 squash)

## References

- [Git 공식 문서](https://git-scm.com/doc)
- [Conventional Commits 명세](https://www.conventionalcommits.org/)
- [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow)
