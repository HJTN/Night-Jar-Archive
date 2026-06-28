# OpenOCD

> Open On-Chip Debugger — JTAG/SWD 기반 MCU 프로그래밍·디버깅 도구

## Overview

오픈소스 온-칩 디버거. JTAG/SWD 어댑터(ST-Link, J-Link, CMSIS-DAP)를 통해 MCU에 접근하며, GDB 서버(포트 3333)와 Telnet 서버(포트 4444)를 제공한다. [[GDB]]와 조합해 임베디드 디버깅 파이프라인의 핵심을 담당한다.

## 연결 구조

```
GDB(arm-none-eabi-gdb) ─── TCP:3333 ──→ OpenOCD ──→ ST-Link/J-Link ──→ MCU
Telnet                  ─── TCP:4444 ──→ OpenOCD
```

## 설치

```bash
# Ubuntu/Debian
sudo apt install openocd

# macOS (Homebrew)
brew install open-ocd

# Windows: 공식 사이트에서 설치 파일 다운로드
# https://openocd.org/pages/getting-openocd.html
```

## 주요 명령어

### 서버 시작

```bash
# STM32F4 + ST-Link 예시
openocd -f interface/stlink.cfg -f target/stm32f4x.cfg

# J-Link 사용 시
openocd -f interface/jlink.cfg -f target/stm32f4x.cfg
```

### Telnet 접속 후 직접 명령

```bash
telnet localhost 4444

# MCU 리셋
reset halt

# Flash 프로그래밍
program firmware.bin 0x08000000 verify reset exit

# Flash 지우기
flash erase_address 0x08000000 0x80000

# 메모리 읽기
mdw 0x08000000 16  # 0x08000000부터 16워드 읽기
```

### GDB와 연동

```bash
# 별도 터미널에서 GDB 실행
arm-none-eabi-gdb firmware.elf

# GDB 내부
(gdb) target extended-remote :3333
(gdb) monitor reset halt
(gdb) load
(gdb) continue
```

## ST-Link / J-Link 연동

| 어댑터 | 특징 | 설정 파일 |
|--------|------|-----------|
| ST-Link V2 | STM32 보드 내장, 저렴 | `interface/stlink.cfg` |
| J-Link | 고속, 다양한 MCU 지원, 유료 | `interface/jlink.cfg` |
| CMSIS-DAP | 오픈소스 표준, 다양한 보드 | `interface/cmsis-dap.cfg` |

## Related Terms

- [[GDB]] — OpenOCD가 GDB 서버 역할
- [[GCC]] — 빌드 결과물(.elf/.bin)을 OpenOCD로 플래시
- [[STM32CubeIDE]] — 내부적으로 OpenOCD 사용

## References

- OpenOCD 공식 문서: openocd.org
- STM32 ST-Link 드라이버 (STSW-LINK009)
