# Reference Architecture (레퍼런스 아키텍처)

## Definition

특정 도메인·기술·시나리오에 대해 검증된 모범 사례를 기반으로 만든 **재사용 가능한 표준 아키텍처 템플릿**.

처음부터 설계하지 않고, 검증된 구조를 출발점으로 사용해 리스크를 낮추고 설계 시간을 단축한다.

## Context / When to Use

솔루션 설계 초기에 기준점(Starting Point)으로 활용. 특히 클라우드 마이그레이션, 신규 시스템 설계, RFP 응답 시 레퍼런스 아키텍처를 참조해 설계의 신뢰성을 높인다.

## 주요 레퍼런스 아키텍처 소스

| 소스 | 내용 |
|---|---|
| **AWS Well-Architected Framework** | 6대 기둥 (안정성·성능·보안·비용·운영·지속가능성) 기반 가이드 |
| **AWS Reference Architecture** | 웹 서비스·서버리스·데이터 파이프라인 등 시나리오별 아키텍처 |
| **Google Cloud Architecture Center** | GCP 기반 레퍼런스 아키텍처 |
| **Azure Architecture Center** | Azure 기반 레퍼런스 아키텍처 |
| **TOGAF** | 엔터프라이즈 아키텍처 프레임워크 |

## 레퍼런스 아키텍처 활용 방법

1. 현재 요구사항에 맞는 레퍼런스 아키텍처 선택
2. 레퍼런스 아키텍처와 현재 상황의 차이점 파악
3. 조직의 제약 (예산·팀 역량·기존 인프라)에 맞게 조정
4. 조정한 부분과 그 이유를 문서화 (ADR)

## 주의사항

- 레퍼런스 아키텍처는 출발점이지 정답이 아님
- "왜 이 레퍼런스를 선택했는가", "어디서 벗어났는가"를 항상 문서화
- 클라우드 벤더 레퍼런스 아키텍처는 해당 벤더의 서비스를 전제로 함 (벤더 종속 주의)

## Related Terms

- [[NFR]] — 레퍼런스 아키텍처 선택의 기준
- [[Trade-off]] — 레퍼런스에서 벗어날 때의 트레이드오프
- [[PoC]] — 레퍼런스 아키텍처 적합성 검증 수단

## References

- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)
- [AWS Reference Architectures](https://aws.amazon.com/architecture/)
- [Google Cloud Architecture Center](https://cloud.google.com/architecture)
