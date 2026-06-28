# API Development Flow

> API 구현·테스트·문서화·배포 전체 흐름

## Overview

API 설계 스펙이 확정된 이후, 실제 코드를 작성하고 테스트하여 배포하는 전체 개발 흐름이다. 각 단계는 다음 단계로 넘어가기 전에 완료 기준을 충족해야 한다.

## Steps

1. **API 설계 확정**
   - [[API-Design-Process]] 완료 후 OpenAPI 스펙 최종 확인
   - 브랜치 생성: `git checkout -b feature/add-{resource}-api`

2. **로컬 환경 구성**
   - [[Docker]] Compose로 DB·Redis·의존 서비스 실행
   - `docker compose up -d`
   - `application-local.yml`에 로컬 환경 변수 설정

3. **구현**
   - Controller → Service → Repository 레이어 순서로 구현
   - [[IntelliJ-IDEA]] HTTP Client 또는 [[Postman]]으로 즉시 동작 확인
   - 커밋은 기능 단위로 자주: `feat(users): 사용자 생성 API 추가`

4. **단위 테스트 (Unit Test)**
   - Service 레이어 비즈니스 로직 테스트 (JUnit 5 + Mockito)
   - 정상 케이스 + 예외 케이스 모두 커버
   ```java
   @Test
   void 존재하지_않는_사용자_조회시_예외() {
       given(userRepository.findById(999L)).willReturn(Optional.empty());
       assertThrows(UserNotFoundException.class,
           () -> userService.getUser(999L));
   }
   ```

5. **통합 테스트 (Integration Test)**
   - DB 포함 전체 레이어 테스트 (`@SpringBootTest`)
   - TestContainers로 실제 DB 컨테이너 사용 권장
   - 엔드포인트 정상 동작 확인

6. **Postman / HTTP Client 테스트**
   - [[Postman]] Collection에 새 요청 추가
   - Test Script로 응답 구조·상태 코드 자동 검증
   - 인증이 필요한 API는 Pre-request Script로 토큰 자동 주입

7. **코드 리뷰 (PR)**
   - [[Git]]으로 PR 생성, [[API-Review-Checklist]] 기준으로 셀프 체크 후 요청
   - PR 설명에 변경된 엔드포인트, 테스트 방법 명시
   - 리뷰어 피드백 반영

8. **배포**
   - [[API-Release-Checklist]] 최종 점검
   - CI/CD 파이프라인 통과 확인 (빌드·테스트 녹색)
   - 스테이징 배포 → 검증 → 프로덕션 배포

9. **문서화 업데이트**
   - [[Swagger]] UI 자동 반영 확인 (springdoc-openapi 사용 시)
   - Changelog에 변경 사항 기록
   - 필요 시 팀 채널에 API 변경 공지

## Inputs

- 확정된 OpenAPI 3.0 스펙 문서
- 기능 요구사항 문서
- 기존 코드베이스 및 아키텍처

## Outputs

- 구현된 API 엔드포인트
- 단위·통합 테스트 코드
- 업데이트된 Swagger 문서
- PR 및 배포 이력

## Notes

- 구현 중 스펙 변경이 생기면 반드시 [[API-Design-Process]]로 돌아가 스펙 먼저 수정
- 로컬 테스트에서 통과한 케이스는 반드시 자동화 테스트로 코드화 (회귀 방지)
- 배포 후 최소 30분은 모니터링 (에러율, 응답 시간 대시보드)
