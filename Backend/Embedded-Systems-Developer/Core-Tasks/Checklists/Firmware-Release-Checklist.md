# Firmware Release Checklist

> 펌웨어 릴리즈 전 반드시 확인해야 할 항목

## 버전 및 빌드 설정

- [ ] 버전 번호 업데이트 (`#define FW_VERSION "1.2.3"` 등)
- [ ] 빌드 플래그를 릴리즈 설정으로 변경 (`-Os`, `-O2`, 디버그 심볼 제거)
- [ ] `DEBUG` 매크로, 테스트용 코드 비활성화 또는 제거
- [ ] 로그 출력 레벨 조정 (디버그 로그 → 에러/경고만 출력)
- [ ] Assert/Breakpoint 코드 비활성화 확인

## 메모리 사용량 확인

- [ ] Flash 사용량 확인 (`arm-none-eabi-size firmware.elf`) — 여유 공간 확인
- [ ] RAM(SRAM) 사용량 확인 — 스택 오버플로우 여유 공간 포함
- [ ] 힙/스택 크기 설정이 런타임 요구사항에 충분한지 확인
- [ ] [[RTOS]] 사용 시 각 태스크 스택 사용량 확인 (`uxTaskGetStackHighWaterMark`)

## 기능 테스트

- [ ] 핵심 기능(Core Features) 전 항목 동작 확인
- [ ] 모든 통신 인터페이스([[UART]], [[SPI]], [[I2C]]) 정상 동작 확인
- [ ] [[Interrupt|인터럽트]] 기반 기능 동작 확인
- [ ] 에러 처리 경로 테스트 (통신 실패, 타임아웃 등)

## 안정성 테스트

- [ ] 경계값(Boundary Value) 테스트 완료
- [ ] 장기 연속 동작 테스트 (최소 24시간)
- [ ] 전원 사이클 후 정상 부팅 및 동작 확인 (최소 10회)
- [ ] Watchdog 타이머 정상 동작 확인 (강제 행 걸기 테스트)
- [ ] OTA 업데이트 가능한 제품: OTA 업데이트 정상 동작 및 롤백 확인

## 보안 (해당되는 경우)

- [ ] 하드코딩된 자격증명(비밀번호, API 키) 없음 확인
- [ ] 펌웨어 서명/CRC 검증 로직 포함 확인
- [ ] 디버그 인터페이스(JTAG/SWD) 잠금 설정 여부 결정

## 코드 품질

- [ ] 컴파일 경고(Warning) 0개 확인 (`-Wall -Wextra`)
- [ ] 정적 분석 도구(PC-lint, Coverity 등) 경고 검토
- [ ] 코드 리뷰 완료

## 문서화 및 버전 관리

- [ ] 변경 이력(Changelog/Release Notes) 작성
- [ ] [[Projects/Templates/Firmware-Version-Template|Firmware-Version-Template]] 작성 완료
- [ ] [[Git]] 태그 부착 (`git tag -a v1.2.3 -m "Release v1.2.3"`)
- [ ] `.bin`/`.hex` 릴리즈 아티팩트 저장 (날짜·버전 포함 파일명)
- [ ] 하드웨어 리비전 호환성 명시

## Notes

릴리즈 체크리스트는 팀원이 서명하고 보관한다. 발견된 이슈는 즉시 [[Git]] 이슈 또는 별도 문서에 기록한다.

## Related

- [[Firmware-Development-Flow]] — 개발 전체 흐름
- [[Firmware]] — 펌웨어 버전 관리 개념
- [[GCC]] — 빌드 플래그 설명
