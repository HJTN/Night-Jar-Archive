# Engineering Organization Models

> 엔지니어링 팀을 어떻게 구조화할 것인가에 대한 주요 모델

## 주요 모델

### 1. Functional (기능 조직)
- 백엔드·프론트엔드·인프라 등 기술 기능별로 팀 구성
- 전문성 집중·기술 표준화 용이
- 단점: 제품 기능 개발 시 팀 간 의존성 높음

### 2. Product (제품 조직) — Spotify 모델
- 제품 기능 단위로 풀스택 팀 구성 (Squad)
- 자율성·속도 향상
- 단점: 기술 표준화·중복 구현 발생 가능

### 3. Matrix
- 기능 조직 + 제품 조직의 혼합
- 대기업에서 사용. 복잡성 높음

### 4. Platform + Stream-Aligned (Team Topologies)
- **Stream-Aligned Team** — 비즈니스 흐름에 집중하는 팀
- **Platform Team** — 공통 인프라·도구를 내부 서비스로 제공 → [[Platform-Strategy]]
- **Enabling Team** — 다른 팀의 역량 향상을 돕는 전문가 팀
- **Complicated Subsystem Team** — 전문 도메인(ML·DSP 등) 담당

## CTO 관점 선택 기준

- 조직 규모가 작을 때(~30명): Functional 또는 초기 Product
- 스케일업(30~200명): Product + Platform 혼합
- 대규모(200명+): Team Topologies 모델 적극 검토

## Related Terms

- [[Platform-Strategy]] — Platform Team 구성과 직결
- [[Engineering-Culture]] — 조직 모델이 문화에 영향
- [[OKR]] — 팀 구조에 맞게 OKR 계단식 설계

## References

- [Team Topologies — Matthew Skelton & Manuel Pais](https://teamtopologies.com/)
- [Spotify Engineering Culture](https://engineering.atspotify.com/)
