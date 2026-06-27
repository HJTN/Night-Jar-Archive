# Cloud Native

> 클라우드 환경의 이점을 최대한 활용하도록 설계·구축된 애플리케이션 방식

## 핵심 원칙 (CNCF 정의)

| 원칙 | 설명 |
|---|---|
| **Microservices** | 기능을 독립 배포 가능한 작은 서비스로 분리 |
| **Containers** | Docker 컨테이너로 환경 일관성 보장 |
| **Dynamic Orchestration** | Kubernetes로 컨테이너 자동 스케줄링·복구 |
| **DevOps** | 개발·운영 통합. CI/CD 파이프라인 |
| **Declarative APIs** | 상태를 선언적으로 정의 (YAML, Terraform) |

## 12 Factor App (Cloud Native 설계 원칙)

1. Codebase — 단일 코드베이스, 다중 배포
2. Dependencies — 명시적 의존성 선언
3. Config — 환경 변수로 설정 관리
4. Backing Services — DB·캐시를 교체 가능한 리소스로
5. Build/Release/Run — 빌드·릴리즈·실행 단계 분리
6. Processes — 무상태(Stateless) 프로세스
7. Port Binding — 포트 바인딩으로 서비스 노출
8. Concurrency — 프로세스 모델로 수평 확장
9. Disposability — 빠른 시작·정상 종료
10. Dev/Prod Parity — 개발·스테이징·프로덕션 환경 일치
11. Logs — 로그를 이벤트 스트림으로 처리
12. Admin Processes — 관리 작업을 일회성 프로세스로

## CTO 관점

- Cloud Native는 기술 선택이 아니라 **조직 역량 투자**
- [[Platform-Strategy]]: 내부 Platform Team이 Cloud Native 인프라를 추상화
- [[Technical-Debt]]: 레거시 모놀리스에서 Cloud Native로 전환 시 아키텍처 부채 상환 필요
- [[Engineering-Culture]]: DevOps·SRE 문화 없이는 Cloud Native 효과 반감

## Related Terms

- [[Platform-Strategy]] — Cloud Native 인프라를 내부 플랫폼으로 제공
- [[Technical-Debt]] — 모놀리스에서 Cloud Native 전환 시 부채 관리
- [[Tech-Radar]] — Kubernetes·Terraform·Istio 등의 Adopt 여부 결정

## References

- [CNCF Cloud Native Definition](https://github.com/cncf/toc/blob/main/DEFINITION.md)
- [12 Factor App](https://12factor.net/)
