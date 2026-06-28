# Embedded Systems Developer

> C/C++ 기반 임베디드 및 시스템 프로그래밍

## Overview

임베디드 시스템 개발자는 마이크로컨트롤러(MCU)·FPGA 등 하드웨어를 직접 제어하는 펌웨어와 소프트웨어를 개발하는 전문가다. C/C++ 기반으로 저수준 하드웨어 인터페이스([[GPIO]]/[[UART]]/[[SPI]]/[[I2C]])를 다루고, 실시간 제약 조건에서 동작하는 시스템을 만든다. 운영체제 없이 bare-metal로 동작하거나 [[RTOS]]를 사용해 멀티태스킹을 구현한다.

## Key Responsibilities

- **펌웨어 개발**: MCU 레지스터 직접 제어, HAL/LL 드라이버 작성, 주변장치 초기화
- **하드웨어 브링업**: 새 보드 최초 동작 검증, 회로도 분석, 전원 시퀀스 확인
- **디바이스 드라이버 작성**: 센서·액추에이터·통신 모듈 드라이버 구현
- **RTOS 태스크 설계**: 태스크 우선순위 설계, 세마포어·큐를 이용한 태스크 간 통신
- **디버깅**: JTAG/SWD([[OpenOCD]]/[[GDB]]) 온-칩 디버깅, 로직 애널라이저, 오실로스코프 활용
- **성능·메모리 최적화**: Flash/RAM 사용량 최소화, 인터럽트 레이턴시 최적화, 코드 크기 최적화

## Core Skills

| 분류 | 기술 / 도구 |
|------|------------|
| 언어 | C, C++, 어셈블리(기초) |
| MCU 플랫폼 | STM32, AVR, ESP32, NXP i.MX |
| 통신 프로토콜 | [[UART]], [[SPI]], [[I2C]], CAN, USB |
| RTOS | [[RTOS|FreeRTOS]], Zephyr, ThreadX |
| 디버깅 도구 | [[GDB]], [[OpenOCD]], J-Link, ST-Link |
| IDE / 빌드 | [[STM32CubeIDE]], [[Keil-MDK]], [[GCC]], CMake |
| 버전 관리 | [[Git]] |

## Related Notes

### 용어
- [[Bootloader]] — 전원 인가 시 첫 실행 코드
- [[Firmware]] — 하드웨어에 내장된 소프트웨어
- [[GPIO]] — 범용 입출력 핀
- [[UART]] — 비동기 직렬 통신
- [[SPI]] — 동기식 고속 직렬 통신
- [[I2C]] — 2선 멀티 디바이스 통신
- [[Interrupt]] — 하드웨어 이벤트 기반 CPU 반응 메커니즘
- [[RTOS]] — 실시간 운영체제

### 워크플로우
- [[Firmware-Development-Flow]] — 요구사항 분석부터 플래싱까지
- [[Hardware-Bring-Up-Process]] — 새 보드 최초 검증 절차

### 체크리스트
- [[Firmware-Release-Checklist]] — 릴리즈 전 확인 항목
- [[Hardware-Bring-Up-Checklist]] — 하드웨어 브링업 확인 항목

### 가이드
- [[Embedded-Systems-Developer-Guide]] — 종합 가이드 및 지식 맵
