# GPIO

## Definition

General Purpose Input/Output. MCU의 범용 입출력 핀. 디지털 신호(HIGH/LOW)를 읽거나 출력하는 데 사용하며, 특수 기능(UART/SPI/I2C 등)으로 재구성(Alternate Function)도 가능하다.

## 동작 모드

| 모드 | 설명 | 사용 예 |
|------|------|--------|
| Input (Floating) | 외부 신호 읽기, 내부 저항 없음 | 외부 풀업 회로 사용 시 |
| Input + Pull-up | 내부 저항으로 기본 HIGH | 버튼 (누르면 LOW) |
| Input + Pull-down | 내부 저항으로 기본 LOW | 버튼 (누르면 HIGH) |
| Output (Push-Pull) | HIGH/LOW 모두 구동 가능 | LED 켜기/끄기 |
| Output (Open-Drain) | LOW만 구동, HIGH는 외부 풀업 의존 | I2C 버스, 오픈콜렉터 |
| Alternate Function | UART/SPI/I2C 등 주변장치 핀으로 사용 | 통신 핀 설정 |
| Analog | ADC/DAC 입출력 | 센서 아날로그 값 읽기 |

## Pull-up / Pull-down 저항

```
VCC
 │
[R]  ← 풀업 저항 (예: 10kΩ)
 │
 ├──── MCU GPIO Input 핀
 │
[버튼]
 │
GND
```

버튼을 누르지 않으면 GPIO = HIGH, 누르면 GPIO = LOW (Active-Low 방식)

## 인터럽트 트리거 종류

| 트리거 | 설명 |
|--------|------|
| Rising Edge | LOW → HIGH 전환 시 |
| Falling Edge | HIGH → LOW 전환 시 |
| Both Edge | 양방향 전환 모두 |
| High Level | HIGH 유지 중 계속 |
| Low Level | LOW 유지 중 계속 |

## STM32 HAL 코드 예시

```c
// LED 출력 (Push-Pull)
HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_SET);   // HIGH
HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_RESET);  // LOW
HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);                  // 토글

// 버튼 입력 읽기
GPIO_PinState state = HAL_GPIO_ReadPin(GPIOC, GPIO_PIN_13);
if (state == GPIO_PIN_RESET) {
    // 버튼 눌림 (Active-Low)
}
```

## Related Terms

- [[Interrupt]] — GPIO 인터럽트(EXTI)와 연계
- [[UART]] — GPIO를 Alternate Function으로 설정하면 UART 핀이 됨
- [[SPI]] — 동일하게 Alternate Function 사용

## References

- STM32 HAL GPIO 드라이버 문서
- [[Hardware-Bring-Up-Checklist]] — GPIO 동작 확인 항목 포함
