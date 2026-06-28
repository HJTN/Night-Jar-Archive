# Concurrency (동시성)

## Definition

여러 작업을 동시에 처리하는 능력. 스레드·비동기 방식으로 구현한다. 서버 개발에서는 수천 개의 요청을 동시에 처리해야 하므로 동시성 제어는 핵심 역량이다.

## 핵심 개념

### Thread vs Process

| 구분 | Thread | Process |
|------|--------|---------|
| 메모리 | 같은 프로세스 내 메모리 공유 | 독립된 메모리 공간 |
| 생성 비용 | 낮음 | 높음 |
| 통신 | 공유 메모리 (빠르지만 위험) | IPC, 메시지 패싱 |
| 격리 | 약함 (한 스레드 오류가 전체에 영향 가능) | 강함 |

### Race Condition (경쟁 조건)
두 스레드가 공유 자원에 동시에 접근할 때 결과가 실행 순서에 따라 달라지는 현상.

```java
// 위험한 코드: count++ 은 read-modify-write 3단계 연산
private int count = 0;
public void increment() { count++; } // 동시 호출 시 값 유실 가능

// 안전한 코드
private AtomicInteger count = new AtomicInteger(0);
public void increment() { count.incrementAndGet(); }
```

### Deadlock (데드락)
두 스레드가 서로 상대방이 가진 락을 기다리며 영원히 멈추는 상태.

```
Thread A: Lock1 보유 → Lock2 대기
Thread B: Lock2 보유 → Lock1 대기
→ 둘 다 영원히 대기
```

**예방법**: 락 획득 순서를 항상 동일하게 유지하거나, tryLock(timeout)으로 획득 실패 시 롤백.

## Java 동시성 메커니즘

### synchronized
```java
public synchronized void increment() { count++; } // 메서드 레벨
public void method() {
    synchronized(this) { /* 블록 레벨 */ }
}
```
간단하지만 세밀한 제어 불가. 재진입(Reentrant) 가능.

### ReentrantLock
```java
private final Lock lock = new ReentrantLock();

public void method() {
    lock.lock();
    try {
        // 임계 구역
    } finally {
        lock.unlock(); // 반드시 finally에서 해제
    }
}
```
tryLock(timeout), 공정성(fairness) 설정 등 세밀한 제어 가능.

### 뮤텍스 vs 세마포어

| 구분 | 뮤텍스 (Mutex) | 세마포어 (Semaphore) |
|------|--------------|---------------------|
| 접근 허용 수 | 1개 스레드 | N개 스레드 설정 가능 |
| 소유권 | 락 획득한 스레드만 해제 | 누구나 해제 가능 |
| 용도 | 상호 배제 (임계 구역 보호) | 리소스 풀 제한 (DB 커넥션 등) |

```java
// 세마포어: 동시 접근을 3개로 제한
Semaphore semaphore = new Semaphore(3);
semaphore.acquire();
try { /* 작업 */ } finally { semaphore.release(); }
```

### CompletableFuture (비동기 처리)
```java
CompletableFuture<User> userFuture = CompletableFuture
    .supplyAsync(() -> userRepository.findById(id))
    .thenApply(user -> enrichUserData(user))
    .exceptionally(e -> User.defaultUser());

// 여러 비동기 작업 병렬 실행
CompletableFuture<Void> all = CompletableFuture.allOf(
    fetchUserAsync(),
    fetchOrderAsync(),
    fetchInventoryAsync()
);
all.join(); // 모두 완료 대기
```

## 낙관적 락 vs 비관적 락

| 구분 | 낙관적 락 (Optimistic Lock) | 비관적 락 (Pessimistic Lock) |
|------|--------------------------|---------------------------|
| 전략 | 충돌이 드물다고 가정. 버전 번호로 충돌 감지 | 충돌 가능성 높다고 가정. DB 레벨에서 SELECT FOR UPDATE |
| 충돌 시 | 애플리케이션에서 재시도 | 다른 트랜잭션은 락 해제까지 대기 |
| 성능 | 읽기 많은 경우 유리 | 쓰기 충돌 많은 경우 안전 |
| JPA 사용 | `@Version` 필드 추가 | `@Lock(PESSIMISTIC_WRITE)` |

```java
// 낙관적 락 - JPA
@Entity
public class Product {
    @Version
    private Long version; // JPA가 자동으로 버전 확인
}

// 비관적 락 - JPA
@Lock(LockModeType.PESSIMISTIC_WRITE)
@Query("SELECT p FROM Product p WHERE p.id = :id")
Optional<Product> findByIdWithLock(Long id);
```

## Related Terms

- [[Connection-Pool]] - 커넥션 풀도 동시 접근 제어가 필요
- [[Caching]] - 캐시 업데이트 시 동시성 문제 발생 가능
- [[ORM]] - JPA의 낙관적/비관적 락

## References

- [Java Concurrency in Practice (Brian Goetz)](https://jcip.net/)
- [JPA Locking - Baeldung](https://www.baeldung.com/jpa-pessimistic-locking)
