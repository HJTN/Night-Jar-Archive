# RTOS

## Definition

Real-Time Operating System. 정해진 시간(데드라인) 내에 작업을 완료함을 보장하는 운영체제. 태스크 스케줄링, 동기화, 태스크 간 통신(IPC) 기능을 제공하며 임베디드 시스템에서 FreeRTOS가 가장 널리 사용된다.

## 핵심 개념

| 개념 | 설명 |
|------|------|
| 태스크(Task) | 독립적인 실행 단위. 각자 스택과 우선순위를 가짐 |
| 스케줄러 | 우선순위 기반 선점형(preemptive) 스케줄링 |
| 세마포어 | 카운팅/바이너리. 태스크 동기화, ISR→태스크 신호 전달 |
| 뮤텍스 | 상호 배제. 공유 자원 보호, 우선순위 상속 지원 |
| 큐(Queue) | 태스크 간 데이터 전달. FIFO 구조 |
| 소프트웨어 타이머 | 주기적/단발성 콜백 실행 |

## FreeRTOS 핵심 API

```c
// 태스크 생성
xTaskCreate(vMyTask,        // 함수 포인터
            "MyTask",       // 태스크 이름
            256,            // 스택 크기 (words)
            NULL,           // 매개변수
            3,              // 우선순위 (높을수록 우선)
            &xTaskHandle);  // 핸들 (NULL 가능)

// 세마포어 사용
SemaphoreHandle_t xSem = xSemaphoreCreateBinary();
xSemaphoreGive(xSem);               // 일반 컨텍스트
xSemaphoreGiveFromISR(xSem, &xHPT); // ISR 컨텍스트
xSemaphoreTake(xSem, portMAX_DELAY);// 대기

// 큐 사용
QueueHandle_t xQueue = xQueueCreate(10, sizeof(uint32_t));
xQueueSend(xQueue, &data, 0);
xQueueReceive(xQueue, &data, portMAX_DELAY);
```

## Bare-metal vs RTOS 선택 기준

| 상황 | 권장 |
|------|------|
| 단순한 단일 루프, 인터럽트 몇 개 | Bare-metal |
| 여러 독립 기능이 동시에 필요 | RTOS |
| 엄격한 타이밍 요구사항 | RTOS |
| Flash/RAM이 매우 제한적 (< 16KB RAM) | Bare-metal |
| 네트워크·USB·파일시스템 미들웨어 필요 | RTOS |

## 주의사항

- 태스크 스택 오버플로우: `configCHECK_FOR_STACK_OVERFLOW` 활성화 권장
- 우선순위 역전(Priority Inversion): 뮤텍스 사용 시 우선순위 상속으로 해결
- ISR에서는 반드시 `FromISR` suffix API 사용

## Related Terms

- [[Interrupt]] — ISR에서 RTOS API로 태스크에 신호 전달
- [[Firmware]] — RTOS는 펌웨어의 일부로 동작
- [[Bootloader]] — RTOS 펌웨어를 로드하는 주체

## References

- FreeRTOS 공식 문서: freertos.org
- [[Firmware-Development-Flow]] — RTOS 태스크 설계 단계 포함
