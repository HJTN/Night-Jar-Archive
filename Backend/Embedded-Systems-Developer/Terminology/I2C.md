# I2C

## Definition

Inter-Integrated Circuit. 2선(SDA: 데이터, SCL: 클럭) 기반의 동기식 직렬 통신 프로토콜. 하나의 버스에 여러 장치를 주소로 구분해 연결할 수 있어 센서·EEPROM·디스플레이 연동에 널리 쓰인다.

## 구조 및 특징

- **마스터-슬레이브**: 마스터가 클럭(SCL)을 생성하고 통신을 주도
- **멀티 슬레이브**: 한 버스에 최대 128개(7비트 주소) 또는 1024개(10비트 주소) 장치 연결 가능
- **오픈-드레인 + 풀업 저항 필수**: 버스 충돌 방지, 일반적으로 4.7kΩ 풀업

## 속도 모드

| 모드 | 속도 |
|------|------|
| Standard Mode | 100 kHz |
| Fast Mode | 400 kHz |
| Fast Mode Plus | 1 MHz |
| High Speed Mode | 3.4 MHz |

## 7비트 주소 프레임 구조

```
START │ 7비트 주소 │ R/W │ ACK │ 데이터(8비트) │ ACK │ ... │ STOP
```

- **START**: SDA HIGH→LOW (SCL HIGH 상태)
- **R/W 비트**: 0 = Write, 1 = Read
- **ACK**: 수신 장치가 SDA를 LOW로 당겨 응답

## SPI vs I2C 비교

| 항목 | I2C | SPI |
|------|-----|-----|
| 선 수 | 2선 (SDA, SCL) | 4선 (MOSI, MISO, SCLK, CS) |
| 속도 | 최대 ~1 MHz | 수십 MHz |
| 멀티 슬레이브 | 주소 방식 (선 추가 없음) | CS 핀 추가 필요 |
| 전이중 통신 | 반이중 | 전이중 |
| 사용 예 | 센서, EEPROM | Flash, 디스플레이, ADC |

## STM32 HAL 코드 예시

```c
// 슬레이브 주소 0x68 장치에 레지스터 0x1B 읽기
uint8_t reg = 0x1B;
uint8_t data;
HAL_I2C_Master_Transmit(&hi2c1, 0x68 << 1, &reg, 1, HAL_MAX_DELAY);
HAL_I2C_Master_Receive(&hi2c1, (0x68 << 1) | 0x01, &data, 1, HAL_MAX_DELAY);
```

주의: STM32 HAL은 주소를 1비트 좌측 시프트(<<1)해서 사용한다.

## Related Terms

- [[SPI]] — 고속 대안, 비교 대상
- [[GPIO]] — SDA/SCL은 GPIO를 Alternate Function으로 설정
- [[Interrupt]] — DMA/인터럽트 기반 I2C로 블로킹 방지

## References

- I2C 스펙: NXP UM10204
- STM32 HAL I2C 드라이버 문서
