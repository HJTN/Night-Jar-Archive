# Bootloader

## Definition

MCU 전원 인가 시 가장 먼저 실행되는 소형 프로그램. Flash 또는 ROM에 저장되어 있으며, 애플리케이션 펌웨어를 메모리에 로드하고 실행권을 넘긴다.

## 부트로더의 역할

- 하드웨어 최소 초기화 (클럭, 스택 포인터)
- Flash에서 애플리케이션 코드 무결성 검증 (CRC, 서명)
- 정상 펌웨어로 점프(jump to application)
- OTA 또는 DFU 모드 진입 조건 판단

## 1단계 / 2단계 부트로더

| 단계 | 위치 | 역할 |
|------|------|------|
| 1단계 (ROM Bootloader) | MCU 내장 ROM (변경 불가) | 최소 초기화, UART/USB DFU 지원 |
| 2단계 (Custom Bootloader) | Flash 앞부분 (0x08000000~) | 펌웨어 검증, OTA 수신·적용 |

STM32의 경우 BOOT0 핀 상태에 따라 ROM 부트로더 또는 Flash 부트로더로 진입한다.

## STM32 Flash 레이아웃 예시

```
0x08000000  ┌─────────────────┐
            │  Bootloader     │  (예: 32KB)
0x08008000  ├─────────────────┤
            │  App Firmware   │  (나머지 Flash)
            └─────────────────┘
```

## OTA(Over-The-Air) 업데이트와의 관계

- 부트로더가 새 펌웨어를 다운로드 영역에 수신
- CRC/서명 검증 후 애플리케이션 영역으로 복사
- 복구(rollback) 로직을 부트로더에 구현해 벽돌 방지

## Related Terms

- [[Firmware]] — 부트로더가 로드하는 대상
- [[UART]] — ROM 부트로더의 기본 다운로드 인터페이스
- [[GPIO]] — BOOT0 핀 읽기에 사용

## References

- STM32 AN2606 Application Note (ROM Bootloader)
- MCUboot 오픈소스 보안 부트로더 프레임워크
