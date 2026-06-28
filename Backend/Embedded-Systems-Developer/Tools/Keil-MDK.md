# Keil MDK

> ARM Keil Microcontroller Development Kit — ARM 기반 임베디드 개발 IDE

## Overview

ARM이 제공하는 임베디드 개발 통합 환경. IDE(µVision) + 컴파일러(ARMCC/AC6) + 디버거가 하나로 패키지화되어 있다. Windows 전용이며, 상업용 라이선스 비용이 높아 대규모 기업·방산·자동차 프로젝트에 주로 사용된다.

## 주요 구성 요소

| 구성 요소 | 설명 |
|-----------|------|
| µVision IDE | 코드 편집, 빌드, 디버그 통합 환경 |
| ARM Compiler 6 (AC6) | LLVM 기반, 최적화 성능 우수 |
| Pack Manager (CMSIS-Pack) | MCU 지원 패키지 다운로드·관리 |
| CMSIS | ARM Cortex-M 공통 드라이버 표준 |
| µVision 디버거 | JTAG/SWD 온-칩 디버깅, 실시간 메모리 뷰 |

## Pack Manager 사용법

1. `Project > Manage > Pack Installer` 열기
2. MCU 제조사(예: STMicroelectronics) 선택
3. 해당 MCU 시리즈(예: STM32F4xx) 패키지 설치
4. 프로젝트에서 Device 선택 시 드라이버 자동 포함

## STM32CubeIDE와 비교

| 항목 | Keil MDK | STM32CubeIDE |
|------|----------|--------------|
| 가격 | 유료 (무료 버전: 32KB 제한) | 무료 |
| 컴파일러 | ARM AC6 (LLVM 기반) | GCC |
| 최적화 | 일반적으로 더 좋음 | 충분히 우수 |
| 코드 생성 | 수동 | CubeMX 통합 자동 생성 |
| OS 지원 | Windows만 | Windows, macOS, Linux |
| RTOS 지원 | MDK-RTX5 내장 | FreeRTOS 통합 |

## 주요 기능

- **실시간 변수 뷰어(Watch Window)**: 디버그 중 변수 값 실시간 모니터링
- **논리 분석기(Logic Analyzer)**: 핀 파형 소프트웨어 시뮬레이션
- **코드 커버리지**: 실행된 코드 라인 시각화
- **메모리 맵 뷰**: Flash/RAM 사용량 그래픽 확인

## 라이선스 주의

- **MDK-Lite**: 무료, 32KB 코드 크기 제한 → 학습용
- **MDK-Essential/Plus/Professional**: 유료, 기능 차등
- 오픈소스 프로젝트나 소규모 팀이라면 [[STM32CubeIDE]](무료) 권장

## Related Terms

- [[GCC]] — STM32CubeIDE는 GCC 사용, Keil은 AC6 사용
- [[GDB]] — Keil은 전용 디버거 사용, GDB 호환 모드도 지원
- [[OpenOCD]] — Keil에서도 OpenOCD 연동 가능

## References

- ARM Keil 공식 사이트: keil.com/mdk5
- CMSIS-Pack 레포지토리
