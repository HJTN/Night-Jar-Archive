# UART

## Definition

Universal Asynchronous Receiver/Transmitter. 클럭 선 없이 TX/RX 2선만으로 동작하는 비동기 직렬 통신 프로토콜. 통신 양단이 동일한 Baud Rate를 설정해야 정상 통신이 가능하다.

## 프레임 구조

```
[IDLE] [START] [D0][D1][D2][D3][D4][D5][D6][D7] [PARITY] [STOP] [IDLE]
  HIGH    LOW                  8 데이터 비트         (선택)  HIGH
```

- **Start bit**: 항상 LOW (1비트)
- **Data bits**: 5~9비트, 일반적으로 8비트
- **Parity bit**: None / Even / Odd (선택)
- **Stop bit**: 1 또는 2비트 HIGH

## 주요 설정 파라미터

| 파라미터 | 일반 설정 | 설명 |
|----------|----------|------|
| Baud Rate | 9600, 115200 | 초당 비트 수 |
| Data Bits | 8 | 데이터 비트 수 |
| Parity | None | 패리티 검사 |
| Stop Bits | 1 | 스톱 비트 수 |
| Flow Control | None / RTS-CTS | 흐름 제어 |

표기법 예: `115200 8N1` (115200bps, 8bit, No parity, 1 stop bit)

## RS-232 vs RS-485

| 항목 | RS-232 | RS-485 |
|------|--------|--------|
| 통신 방식 | 1:1 (포인트-투-포인트) | 1:N (멀티드롭, 최대 32노드) |
| 전압 레벨 | ±3V~±15V | 차동 신호 (-7V~+12V) |
| 거리 | ~15m | ~1200m |
| 사용 예 | PC 시리얼 포트, 모뎀 | 산업용 버스, Modbus |

## 디버그 출력 (printf redirect)

```c
// STM32에서 printf를 UART로 리디렉션
int __io_putchar(int ch) {
    HAL_UART_Transmit(&huart2, (uint8_t *)&ch, 1, HAL_MAX_DELAY);
    return ch;
}
// 이후 printf() 사용 가능, 개발 중 디버그 로그 출력에 활용
```

## STM32 HAL 코드 예시

```c
// 송신
char msg[] = "Hello\r\n";
HAL_UART_Transmit(&huart2, (uint8_t *)msg, strlen(msg), HAL_MAX_DELAY);

// 수신 (인터럽트 방식 권장)
uint8_t rxBuf[64];
HAL_UART_Receive_IT(&huart2, rxBuf, 1);  // 1바이트 수신 후 콜백 호출
```

## Related Terms

- [[Interrupt]] — UART 수신 인터럽트로 논블로킹 수신
- [[GPIO]] — TX/RX 핀은 GPIO Alternate Function으로 설정
- [[Bootloader]] — ROM 부트로더의 기본 다운로드 인터페이스

## References

- STM32 HAL UART 드라이버 문서
- [[Hardware-Bring-Up-Checklist]] — UART 디버그 출력 확인 항목
