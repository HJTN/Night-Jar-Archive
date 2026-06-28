# GCC

> GNU C/C++ 컴파일러 — 임베디드 크로스 컴파일

## Overview

GNU Compiler Collection. 임베디드 ARM 개발에는 `arm-none-eabi-gcc` 크로스 컴파일러를 사용한다. 호스트(PC)에서 타겟(ARM MCU)용 바이너리를 생성한다. STM32CubeIDE와 Keil MDK 모두 내부적으로 GCC 기반 툴체인을 사용한다.

## 주요 컴파일 플래그

| 플래그 | 의미 | 용도 |
|--------|------|------|
| `-O0` | 최적화 없음 | 디버그 빌드 |
| `-O2` | 속도 최적화 | 릴리즈 빌드 일반 |
| `-Os` | 코드 크기 최적화 | Flash 제한 시 |
| `-Og` | 디버그 최적화 | 디버거 친화적 |
| `-g` | 디버그 심볼 포함 | GDB 사용 시 필수 |
| `-mcpu=cortex-m4` | 타겟 CPU 지정 | MCU에 맞게 변경 |
| `-mfpu=fpv4-sp-d16` | FPU 지정 | 하드웨어 부동소수점 |
| `-mfloat-abi=hard` | 하드웨어 FPU 사용 | 성능 향상 |
| `-Wall -Wextra` | 경고 최대화 | 코드 품질 |

## 링커 스크립트 (.ld)

메모리 레이아웃을 정의한다. STM32CubeMX가 자동 생성.

```ld
MEMORY
{
  FLASH (rx) : ORIGIN = 0x08000000, LENGTH = 512K
  RAM   (xrw): ORIGIN = 0x20000000, LENGTH = 128K
}

SECTIONS
{
  .text : { *(.text*) } > FLASH
  .data : { *(.data*) } > RAM AT > FLASH  /* 초기값은 Flash에 저장 */
  .bss  : { *(.bss*)  } > RAM             /* 0으로 초기화 */
}
```

## 메모리 섹션 요약

| 섹션 | 내용 | 저장 위치 |
|------|------|----------|
| `.text` | 코드, 상수 | Flash |
| `.data` | 초기값 있는 전역/정적 변수 | Flash(초기값) → RAM(런타임) |
| `.bss` | 초기값 없는 전역/정적 변수 | RAM (0으로 초기화) |
| `.stack` | 스택 | RAM |
| `.heap` | 동적 할당 영역 | RAM |

## Makefile 기반 빌드 예시

```makefile
CC = arm-none-eabi-gcc
CFLAGS = -mcpu=cortex-m4 -mthumb -Os -g -Wall
LDFLAGS = -T STM32F4.ld -Wl,--gc-sections

all: firmware.bin

firmware.elf: main.c startup.s
	$(CC) $(CFLAGS) $(LDFLAGS) -o $@ $^

firmware.bin: firmware.elf
	arm-none-eabi-objcopy -O binary $< $@

size: firmware.elf
	arm-none-eabi-size $<
```

`arm-none-eabi-size`로 Flash/RAM 사용량을 빠르게 확인할 수 있다.

## Related Terms

- [[GDB]] — GCC로 빌드된 바이너리를 디버깅
- [[OpenOCD]] — GDB 서버, GCC 결과물을 MCU에 플래시
- [[Firmware]] — GCC의 빌드 결과물

## References

- [[STM32CubeIDE]] — GCC 툴체인 내장
- [[Firmware-Release-Checklist]] — 빌드 플래그 확인 항목 포함
