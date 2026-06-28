# Firmware

## Definition

하드웨어를 직접 제어하기 위해 비휘발성 메모리(Flash/ROM)에 저장된 소프트웨어. OS 없이 하드웨어와 직접 상호작용하며, 제품 출하 후에도 업데이트가 가능하다.

## RAM vs Flash 저장

| 항목 | Flash (프로그램 메모리) | RAM (데이터 메모리) |
|------|------------------------|-------------------|
| 코드(.text) | Flash에 저장, CPU가 직접 실행 | — |
| 초기값 있는 전역변수(.data) | Flash에 초기값 보관 | 부팅 시 RAM으로 복사 |
| 초기값 없는 전역변수(.bss) | — | 부팅 시 0으로 초기화 |
| 스택/힙 | — | 런타임에 사용 |

## 펌웨어 업데이트 방식

| 방식 | 설명 | 사용 상황 |
|------|------|-----------|
| JTAG/SWD | 디버거로 직접 Flash 프로그래밍 | 개발·양산 초기 |
| DFU (Device Firmware Upgrade) | USB/UART 통한 ROM 부트로더 활용 | 공장 라인, A/S |
| OTA (Over-The-Air) | Wi-Fi/BLE/LTE 통한 무선 업데이트 | 현장 배포 제품 |
| SD카드/외부 Flash | 파일 복사 후 부트로더가 적용 | 대용량 업데이트 |

## 버전 관리의 중요성

- 하드웨어 리비전(Rev A, Rev B)과 펌웨어 호환성 추적 필수
- 시맨틱 버전 사용 권장: `MAJOR.MINOR.PATCH` (예: `2.3.1`)
- 버전 정보를 Flash 특정 주소에 저장해 부트로더·진단 도구가 읽을 수 있게 함
- [[Git]] 태그로 릴리즈 버전 관리: `git tag v2.3.1`

## Related Terms

- [[Bootloader]] — 펌웨어를 로드·실행하는 초기 프로그램
- [[GCC]] — 펌웨어를 빌드하는 컴파일러
- [[Git]] — 펌웨어 소스 버전 관리

## References

- [[Firmware-Release-Checklist]] — 릴리즈 전 확인 항목
- [[Firmware-Development-Flow]] — 개발 전체 흐름
