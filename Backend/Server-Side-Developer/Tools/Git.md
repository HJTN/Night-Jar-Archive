# Git

> 분산 버전 관리 시스템

## Overview

Git은 코드 변경 이력을 관리하고 팀과 협업하기 위한 표준 버전 관리 도구다. 서버 개발자는 Git을 통해 기능 개발, 버그 수정, 코드 리뷰 프로세스를 진행한다.

## 브랜치 전략

### Git Flow
규모가 있는 팀, 명확한 릴리즈 사이클이 있는 프로젝트에 적합.

```
main (또는 master)     ─────────────────────────────────── 운영 배포
                             ↑                   ↑
release/1.0          ──────────────              릴리즈 브랜치 (최종 검증)
                        ↑
develop              ────────────────────────────── 통합 개발 브랜치
                       ↑              ↑
feature/login     ──────        feature/order ──── 기능 브랜치
```

- `main`: 운영 배포 코드
- `develop`: 다음 릴리즈를 위한 통합 브랜치
- `feature/*`: 기능 개발 브랜치 (develop에서 분기, develop으로 머지)
- `release/*`: 릴리즈 준비 브랜치 (버그 수정만)
- `hotfix/*`: 운영 긴급 수정 (main에서 분기, main + develop으로 머지)

### Trunk-Based Development
CI/CD를 빠르게 돌리는 팀, 소규모 팀에 적합.

```
main             ────────────────────────────── 항상 배포 가능 상태 유지
                   ↑      ↑      ↑
feature branches  ─    ─     ─           짧은 수명 (1~2일 이내 머지)
```

- 브랜치 수명을 짧게 유지 (하루 이내)
- Feature Flag로 미완성 기능을 숨기고 main에 머지
- CI가 항상 green이어야 함

## Conventional Commits (커밋 메시지 컨벤션)

```
<타입>(<범위>): <제목>

<본문 - 선택사항>

<푸터 - 선택사항>
```

| 타입 | 사용 상황 |
|------|----------|
| `feat` | 새로운 기능 추가 |
| `fix` | 버그 수정 |
| `refactor` | 기능 변경 없이 코드 구조 개선 |
| `perf` | 성능 개선 |
| `test` | 테스트 코드 추가/수정 |
| `docs` | 문서 변경 |
| `chore` | 빌드 설정, 의존성 업데이트 등 |
| `style` | 코드 포매팅 (기능 변경 없음) |

```bash
# 예시
feat(order): 주문 취소 API 구현
fix(auth): JWT 만료 토큰 검증 누락 수정
refactor(user): 사용자 서비스 레이어 책임 분리
perf(product): 상품 목록 조회 쿼리 N+1 문제 수정
```

## 주요 명령어

```bash
# 브랜치 관리
git checkout -b feature/order-cancel   # 새 브랜치 생성 및 이동
git branch -d feature/order-cancel     # 브랜치 삭제

# 스테이징 및 커밋
git add src/                           # 특정 디렉토리 스테이징
git commit -m "feat(order): 주문 취소 API 구현"
git commit --amend                     # 직전 커밋 수정 (푸시 전만)

# 원격 저장소
git fetch --prune                      # 원격 브랜치 동기화 (삭제된 브랜치 반영)
git pull --rebase origin develop       # 리베이스로 최신화 (머지 커밋 방지)
git push -u origin feature/order-cancel

# 히스토리 정리
git rebase -i HEAD~3                   # 최근 3개 커밋 인터랙티브 리베이스 (squash 등)
git log --oneline --graph              # 브랜치 그래프 확인

# 임시 저장
git stash                              # 작업 중인 변경사항 임시 저장
git stash pop                          # 임시 저장된 내용 복구
git stash list                         # 스태시 목록 확인

# 특정 커밋만 가져오기
git cherry-pick <commit-hash>          # hotfix 등에서 특정 커밋만 적용

# 변경사항 취소
git restore <file>                     # 워킹 디렉토리 변경사항 취소
git restore --staged <file>            # 스테이징 취소
git revert <commit-hash>               # 커밋 취소 (새 커밋으로 되돌림, 이력 유지)
```

## 코드 리뷰 팁

- PR은 작게 유지 (300줄 이하 권장)
- PR 제목도 Conventional Commit 형식 사용
- Self-review 먼저: 본인 PR을 먼저 리뷰하고 올리기
- Draft PR로 WIP 상태 표시

## References

- [Conventional Commits](https://www.conventionalcommits.org/)
- [Git Flow by Vincent Driessen](https://nvie.com/posts/a-successful-git-branching-model/)
- [Trunk Based Development](https://trunkbaseddevelopment.com/)
