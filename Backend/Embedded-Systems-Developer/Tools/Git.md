# Git

> 분산 버전 관리 시스템 — 펌웨어 개발 관점

## Overview

임베디드 펌웨어 개발에서도 Git은 필수다. 하드웨어 리비전별 코드 분기, 릴리즈 버전 태깅, 팀 협업을 관리한다. 바이너리 파일(.bin/.hex)은 용량이 크지 않으므로 커밋해도 되지만, `.gitignore`로 빌드 아티팩트를 선별 관리하는 것이 좋다.

## 펌웨어 개발 브랜치 전략

```
main          ──●──────────────────●── (릴리즈 태그: v1.0.0, v1.1.0)
                 \                /
develop         ──●──●──●──●──●──
                       \     /
feature/uart-dma  ──●──●
```

| 브랜치 | 용도 |
|--------|------|
| `main` | 릴리즈된 안정 버전, 태그 부착 |
| `develop` | 통합 개발 브랜치 |
| `feature/*` | 기능 단위 개발 |
| `hw/rev-b` | 하드웨어 리비전별 분기 |
| `hotfix/*` | 긴급 버그 수정 |

## 하드웨어 버전별 태그 전략

```bash
# 릴리즈 태그 (하드웨어 리비전 포함 권장)
git tag -a v2.1.0-hwB -m "Firmware v2.1.0 for HW Rev B"
git push origin v2.1.0-hwB

# 태그 목록 확인
git tag -l "v*"
```

## 바이너리 파일 관리

```gitignore
# .gitignore 예시 (임베디드 프로젝트)
build/
*.o
*.d
*.map
*.lst
Debug/
Release/

# 최종 바이너리는 선택적으로 포함 (릴리즈 시)
# *.bin
# *.hex
```

빌드 재현성을 위해 최종 `.bin`/`.hex`는 릴리즈 태그에 첨부하거나 별도 아티팩트 저장소 사용.

## 주요 명령어 (펌웨어 개발 관점)

```bash
# 하드웨어 리비전 브랜치 생성
git checkout -b hw/rev-c develop

# 특정 커밋으로 되돌리기 (안전하게)
git revert <commit-hash>

# 두 버전 간 변경 내용 비교
git diff v1.0.0..v1.1.0 -- src/

# 특정 파일의 변경 이력
git log --oneline -- src/uart.c

# 서브모듈 (외부 HAL/드라이버 라이브러리 관리)
git submodule add https://github.com/STMicroelectronics/stm32f4xx_hal_driver libs/hal
git submodule update --init --recursive
```

## Related Terms

- [[Firmware]] — 버전 관리 대상
- [[GCC]] — 빌드 결과물(.bin/.hex) 관리
- [[Firmware-Release-Checklist]] — 릴리즈 전 태그 전략 포함

## References

- [[Firmware-Development-Flow]] — 개발 흐름에서 Git 브랜치 관리 위치
