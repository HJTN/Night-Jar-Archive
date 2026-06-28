# Caching

## Definition

자주 조회되는 데이터를 메모리에 임시 저장해 응답 속도를 높이는 기법. DB나 외부 API 호출 비용을 줄이고 처리량을 높인다.

## 핵심 개념

### Cache Hit / Miss
- **Cache Hit**: 요청한 데이터가 캐시에 있어 빠르게 반환
- **Cache Miss**: 캐시에 없어 원본 소스(DB 등)에서 조회 후 캐시에 저장
- **Hit Rate**: `Hit 수 / 전체 요청 수`. 일반적으로 80% 이상이면 효과적

### TTL (Time To Live)
캐시 항목이 유효한 시간. 만료되면 자동 삭제된다.
- 너무 짧으면 → 캐시 효과 감소, DB 부하 증가
- 너무 길면 → 오래된 데이터 제공 (Stale Data)

### Cache Invalidation (캐시 무효화)
"캐시 무효화는 컴퓨터 과학의 두 가지 어려운 문제 중 하나다." — Phil Karlton

데이터가 변경됐을 때 캐시를 어떻게 최신 상태로 유지할지가 핵심 과제다.

## 캐싱 전략 비교

| 전략 | 설명 | 장점 | 단점 | 적합한 상황 |
|------|------|------|------|------------|
| **Cache-Aside** (Lazy Loading) | 앱이 직접 캐시 확인 → Miss 시 DB 조회 후 캐시에 저장 | 필요한 데이터만 캐싱, 캐시 장애 시 DB 직접 조회 가능 | 첫 요청은 느림 (Cold Start), 데이터 정합성 관리 필요 | 읽기 중심 워크로드 |
| **Write-Through** | 쓰기 시 캐시와 DB를 동시에 업데이트 | 캐시 항상 최신 상태 | 모든 쓰기에 캐시 저장 비용 발생, 안 읽히는 데이터도 캐싱 | 읽기/쓰기 비율 비슷한 경우 |
| **Write-Back** (Write-Behind) | 쓰기 시 캐시만 업데이트, 나중에 DB에 비동기 반영 | 쓰기 성능 최고 | 캐시 장애 시 데이터 유실 위험 | 쓰기가 매우 빈번한 경우 |
| **Read-Through** | 캐시가 DB 조회를 대행 (앱은 캐시만 바라봄) | 앱 코드 단순화 | 캐시 라이브러리 지원 필요 | 캐시 미스 처리 일관성이 필요할 때 |

## Redis 활용 패턴

```java
// Cache-Aside 패턴 (Spring + Redis)
public Product getProduct(Long id) {
    String key = "product:" + id;
    
    // 1. 캐시 조회
    Product cached = redisTemplate.opsForValue().get(key);
    if (cached != null) {
        return cached; // Cache Hit
    }
    
    // 2. DB 조회 (Cache Miss)
    Product product = productRepository.findById(id)
        .orElseThrow(() -> new NotFoundException());
    
    // 3. 캐시 저장 (TTL 1시간)
    redisTemplate.opsForValue().set(key, product, 1, TimeUnit.HOURS);
    return product;
}

// 캐시 무효화 (데이터 변경 시)
public Product updateProduct(Long id, UpdateRequest req) {
    Product product = productRepository.save(/* ... */);
    redisTemplate.delete("product:" + id); // 캐시 삭제
    return product;
}
```

## 캐시 적용 시 주의사항

- **Cache Stampede (Thundering Herd)**: TTL 만료 직후 다수 요청이 동시에 DB를 조회하는 현상. Mutex Lock이나 확률적 조기 만료로 방지
- **Cache Warm-up**: 서버 재시작 후 캐시가 비어있는 상태에서 DB 부하 폭증. 배포 전 주요 데이터 미리 로드
- **민감 데이터**: 개인정보·권한 정보는 캐싱에 주의. 사용자 간 데이터 오염 방지

## Related Terms

- [[Connection-Pool]] - DB 부하 분산의 다른 축
- [[Concurrency]] - 캐시 접근 시 동시성 고려 필요
- [[ORM]] - ORM 레벨에서도 1차/2차 캐시 존재 (Hibernate)

## References

- [Redis 공식 문서](https://redis.io/docs/)
- [Caching Strategies - AWS](https://aws.amazon.com/caching/best-practices/)
