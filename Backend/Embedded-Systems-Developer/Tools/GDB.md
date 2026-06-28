# GDB

> GNU 디버거 — 임베디드 온-칩 디버깅

## Overview

GNU Debugger. 임베디드 환경에서는 `arm-none-eabi-gdb`를 사용하고, [[OpenOCD]]가 GDB 서버 역할을 해 JTAG/SWD를 통해 MCU에 접속한다. STM32CubeIDE와 VS Code에서 GUI로도 사용 가능하다.

## 연결 구조

```
PC                     디버거 하드웨어          MCU
arm-none-eabi-gdb ──→ OpenOCD ──→ ST-Link/J-Link ──→ MCU (SWD/JTAG)
  (포트 3333 TCP)
```

## 주요 명령어

| 명령어 | 단축키 | 설명 |
|--------|--------|------|
| `target extended-remote :3333` | — | OpenOCD에 연결 |
| `monitor reset halt` | — | MCU 리셋 후 정지 |
| `load` | — | ELF 파일을 MCU Flash에 프로그래밍 |
| `break main` | `b main` | main 함수에 중단점 설정 |
| `break file.c:42` | `b file.c:42` | 특정 파일 줄에 중단점 |
| `run` / `continue` | `r` / `c` | 실행 시작 / 계속 |
| `step` | `s` | 한 줄 실행 (함수 진입) |
| `next` | `n` | 한 줄 실행 (함수 건너뜀) |
| `finish` | — | 현재 함수 끝까지 실행 |
| `print expr` | `p expr` | 변수·표현식 값 출력 |
| `info registers` | `i r` | 모든 레지스터 값 출력 |
| `x/4xw 0x20000000` | — | 메모리 주소의 4워드 hex 출력 |
| `backtrace` | `bt` | 콜 스택 출력 |
| `list` | `l` | 소스 코드 표시 |
| `quit` | `q` | 종료 |

## 임베디드 디버깅 팁

- **Watch Point**: 특정 변수 값이 변경될 때 자동 중단  
  `watch myVariable`
- **Peripheral 레지스터 읽기**:  
  `x/xw 0x40020000` (GPIOA MODER 레지스터 확인)
- **플래시 프로그래밍 후 즉시 실행**:
  ```
  monitor reset halt
  load
  monitor reset run
  ```

## HardFault 분석

HardFault 발생 시 LR 레지스터에서 스택 프레임 위치를 찾아 원인 파악:

```
(gdb) info registers
(gdb) p/x $sp          # 스택 포인터 확인
(gdb) x/16xw $sp       # 스택 프레임 내용 확인
# 스택 프레임: R0, R1, R2, R3, R12, LR, PC, xPSR 순서
# PC 값이 문제 발생 주소
```

STM32CubeIDE의 Fault Analyzer 뷰를 사용하면 더 직관적으로 분석 가능.

## Related Terms

- [[OpenOCD]] — GDB 서버, JTAG/SWD 인터페이스
- [[GCC]] — `-g` 플래그로 빌드해야 디버그 심볼 포함
- [[STM32CubeIDE]] — GDB 프론트엔드 통합

## References

- GDB 공식 문서: sourceware.org/gdb/documentation
- OpenOCD + GDB 연동 가이드
