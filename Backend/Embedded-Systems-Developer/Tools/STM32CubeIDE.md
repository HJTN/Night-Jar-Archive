# STM32CubeIDE

> STM32 MCU 전용 Eclipse 기반 무료 통합 개발환경

## Overview

STMicroelectronics가 제공하는 무료 IDE. Eclipse + GCC 툴체인 + STM32CubeMX 코드 생성기가 통합되어 있다. 핀 설정, 클럭 구성, 미들웨어 설정을 GUI로 하고, 자동 초기화 코드를 생성해준다. [[OpenOCD]] 기반 디버거가 내장되어 ST-Link만 있으면 즉시 디버깅 가능하다.

## 주요 기능

### 1. CubeMX 통합 (핀/클럭/미들웨어 설정 GUI)

- `.ioc` 파일로 MCU 핀 설정 관리
- 핀맵에서 기능(UART, SPI, I2C, TIM 등) 드래그·드롭 할당
- 클럭 트리 시각화, 자동 PLL 계산
- FreeRTOS, LWIP, USB 등 미들웨어 선택·설정

### 2. 코드 자동 생성

- `main.c`의 `/* USER CODE BEGIN */` ~ `/* USER CODE END */` 구간은 재생성 시 보존
- HAL 초기화 코드 자동 작성, 커스텀 코드는 USER CODE 블록 안에 작성해야 덮어쓰기 방지

### 3. 디버거

- ST-Link를 통한 SWD 디버깅
- 중단점, 단계 실행, 변수·레지스터 뷰
- **Live Expressions**: 실행 중 변수 값 실시간 확인
- **Memory Browser**: 메모리 주소 직접 확인·편집
- **SWV (Serial Wire Viewer)**: printf 없이 ITM으로 데이터 스트리밍

## 단축키

| 단축키 | 기능 |
|--------|------|
| `Ctrl+B` | 프로젝트 빌드 |
| `F5` | 디버그 시작 |
| `F8` | 실행 계속 (Resume) |
| `F6` | 다음 줄 (Step Over) |
| `F5` (디버그 중) | 함수 진입 (Step Into) |
| `Ctrl+Shift+O` | 임포트 정리 |
| `Ctrl+Shift+F` | 코드 자동 정렬 |
| `Ctrl+/` | 줄 주석 토글 |

## 프로젝트 생성 순서

1. File → New → STM32 Project
2. MCU 또는 보드 선택 (예: STM32F411RE)
3. `.ioc` 파일에서 핀·클럭·미들웨어 설정
4. `Project > Generate Code` (또는 Ctrl+Shift+S) → HAL 초기화 코드 생성
5. `USER CODE` 블록 안에 애플리케이션 코드 작성
6. 빌드 (Ctrl+B) → 디버그 (F11)

## Related Terms

- [[GCC]] — 내장 arm-none-eabi-gcc 툴체인
- [[GDB]] — 내장 디버거 백엔드
- [[OpenOCD]] — 내장 GDB 서버
- [[RTOS]] — FreeRTOS 미들웨어 통합 지원

## References

- STM32CubeIDE 공식: st.com/en/development-tools/stm32cubeide.html
- ST AN5952: STM32CubeIDE 시작 가이드
