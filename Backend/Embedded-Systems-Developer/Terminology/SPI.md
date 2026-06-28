# SPI

## Definition

Serial Peripheral Interface. 4선(MOSI/MISO/SCLK/CS) 기반의 동기식 전이중 직렬 통신 프로토콜. 마스터가 클럭을 생성하며, 슬레이브 선택 핀(CS, Chip Select)으로 통신 대상을 지정한다.

## 핀 구성

| 핀 | 방향 | 설명 |
|----|------|------|
| SCLK (SCK) | 마스터 → 슬레이브 | 동기 클럭 |
| MOSI | 마스터 → 슬레이브 | Master Out Slave In |
| MISO | 슬레이브 → 마스터 | Master In Slave Out |
| CS (NSS) | 마스터 → 슬레이브 | Chip Select (Active-Low) |

멀티 슬레이브: 슬레이브마다 별도 CS 핀 필요 (MOSI/MISO/SCLK 공유)

## SPI 모드 (CPOL/CPHA)

| Mode | CPOL | CPHA | 클럭 유휴 상태 | 샘플링 에지 |
|------|------|------|--------------|------------|
| 0 | 0 | 0 | LOW | Rising |
| 1 | 0 | 1 | LOW | Falling |
| 2 | 1 | 0 | HIGH | Falling |
| 3 | 1 | 1 | HIGH | Rising |

장치 데이터시트에서 지원 모드를 확인하고 일치시켜야 한다.

## I2C vs SPI 비교

| 항목 | SPI | I2C |
|------|-----|-----|
| 선 수 | 4선 (+ 슬레이브당 CS 1개) | 2선 |
| 속도 | 수십 MHz | 최대 ~1 MHz |
| 전이중 | 가능 | 불가 (반이중) |
| 멀티 슬레이브 | CS 핀 추가 필요 | 주소 방식 |
| 사용 예 | Flash, SD카드, TFT 디스플레이, 고속 ADC | 센서, EEPROM, RTC |

## STM32 HAL 코드 예시

```c
// CS LOW (통신 시작)
HAL_GPIO_WritePin(CS_GPIO_Port, CS_Pin, GPIO_PIN_RESET);

// 송수신 동시 (전이중)
uint8_t txBuf[4] = {0x01, 0x02, 0x03, 0x04};
uint8_t rxBuf[4];
HAL_SPI_TransmitReceive(&hspi1, txBuf, rxBuf, 4, HAL_MAX_DELAY);

// CS HIGH (통신 종료)
HAL_GPIO_WritePin(CS_GPIO_Port, CS_Pin, GPIO_PIN_SET);
```

## Related Terms

- [[I2C]] — 저속 멀티 디바이스 통신, 비교 대상
- [[GPIO]] — CS 핀은 일반 GPIO로 수동 제어
- [[Interrupt]] — SPI DMA 완료 인터럽트 활용 시

## References

- STM32 HAL SPI 드라이버 문서
- W25Q128 SPI Flash 데이터시트 (SPI Mode 0/3 지원 예시)
