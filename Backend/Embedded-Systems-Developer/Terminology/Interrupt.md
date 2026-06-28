# Interrupt

## Definition

하드웨어 또는 소프트웨어 이벤트 발생 시 CPU가 현재 작업을 잠시 중단하고, 미리 등록된 ISR(Interrupt Service Routine)을 실행한 뒤 원래 작업으로 복귀하는 메커니즘이다.

## 인터럽트 처리 흐름

```
메인 코드 실행
    │
    ▼
[이벤트 발생: UART 수신, GPIO 에지, 타이머 만료 등]
    │
    ▼
CPU: 현재 레지스터 스택에 저장 (컨텍스트 저장)
    │
    ▼
ISR 실행
    │
    ▼
CPU: 레지스터 복원 (컨텍스트 복원)
    │
    ▼
메인 코드 재개
```

## ARM Cortex-M NVIC (Nested Vectored Interrupt Controller)

- 최대 240개 외부 인터럽트 지원
- 우선순위 0(최고) ~ 255(최저), STM32는 보통 0~15 사용
- **선점형 우선순위(Preemptive Priority)**: 높은 우선순위 ISR이 낮은 우선순위 ISR을 선점 가능
- **서브 우선순위(Sub Priority)**: 같은 선점 우선순위 내 실행 순서 결정

```c
// STM32 HAL NVIC 설정 예시
HAL_NVIC_SetPriority(USART1_IRQn, 2, 0);  // 선점:2, 서브:0
HAL_NVIC_EnableIRQ(USART1_IRQn);
```

## Polling vs Interrupt 비교

| 항목 | Polling | Interrupt |
|------|---------|-----------|
| CPU 사용 | 이벤트 없을 때도 계속 체크 | 이벤트 발생 시에만 실행 |
| 반응 속도 | 폴링 주기에 따라 지연 가능 | 즉각 반응 (레이턴시 낮음) |
| 구현 복잡도 | 단순 | ISR 작성 필요 |
| 사용 예 | 빠른 센서 읽기, 단순 루프 | UART 수신, 타이머, GPIO 에지 |

## ISR에서 하지 말아야 할 것

- `HAL_Delay()` 등 블로킹 함수 호출 금지 (SysTick 인터럽트 필요)
- 긴 연산, 복잡한 로직 수행 금지 (레이턴시 유발)
- `printf()` 직접 호출 금지 (재진입 불가, 느림) → 플래그 세우고 메인에서 처리
- RTOS 사용 시: ISR 전용 API 사용 (`xQueueSendFromISR`, `xSemaphoreGiveFromISR`)

## Related Terms

- [[GPIO]] — GPIO 인터럽트(EXTI) 소스
- [[UART]] — UART 수신 인터럽트
- [[RTOS]] — 인터럽트와 RTOS 태스크 간 통신

## References

- ARM Cortex-M Programming Guide (NVIC 챕터)
- STM32 HAL EXTI, USART 인터럽트 예제
