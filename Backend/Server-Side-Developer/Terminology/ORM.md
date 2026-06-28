# ORM (Object-Relational Mapping)

## Definition

객체와 관계형 DB 테이블을 매핑해 SQL 없이 DB를 조작하는 기술. 코드에서 객체를 다루면 ORM이 SQL로 변환해 실행한다.

## JPA / Hibernate 핵심 개념

### Entity
```java
@Entity
@Table(name = "orders")
public class Order {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @ManyToOne(fetch = FetchType.LAZY)  // 지연 로딩
    @JoinColumn(name = "user_id")
    private User user;
    
    @OneToMany(mappedBy = "order", cascade = CascadeType.ALL)
    private List<OrderItem> items = new ArrayList<>();
    
    @Version  // 낙관적 락
    private Long version;
}
```

### Repository
```java
public interface OrderRepository extends JpaRepository<Order, Long> {
    // JPQL 사용
    @Query("SELECT o FROM Order o JOIN FETCH o.items WHERE o.user.id = :userId")
    List<Order> findWithItemsByUserId(@Param("userId") Long userId);
    
    // 메서드 이름 기반 자동 쿼리 생성
    List<Order> findByUserIdAndStatus(Long userId, OrderStatus status);
}
```

### JPQL (Java Persistence Query Language)
SQL과 유사하지만 테이블명 대신 **엔티티 클래스명**, 컬럼명 대신 **필드명**을 사용한다.
```java
// 네이티브 SQL (비권장, 필요시만)
@Query(value = "SELECT * FROM orders WHERE created_at > :date", nativeQuery = true)

// JPQL (권장)
@Query("SELECT o FROM Order o WHERE o.createdAt > :date")
```

## N+1 문제

ORM 사용 시 가장 흔하고 치명적인 성능 문제. 1개의 쿼리로 N개의 엔티티를 조회한 후, 각 엔티티의 연관 데이터를 가져오기 위해 N개의 추가 쿼리가 발생하는 현상.

```java
// N+1 발생 코드
List<Order> orders = orderRepository.findAll(); // 쿼리 1번
for (Order order : orders) {
    order.getUser().getName(); // User 조회 쿼리 N번 발생 (Lazy Loading)
}
// 결과: 1 + N번 쿼리 실행
```

### 해결 방법

| 방법 | 설명 | 코드 |
|------|------|------|
| **Fetch Join** | JPQL에서 연관 엔티티를 한 번에 로드 | `JOIN FETCH o.user` |
| **EntityGraph** | 쿼리 메서드에 페치 전략 지정 | `@EntityGraph(attributePaths = {"user"})` |
| **Batch Size** | N번 대신 IN 절로 묶어서 조회 | `@BatchSize(size = 100)` 또는 `spring.jpa.properties.hibernate.default_batch_fetch_size=100` |

```java
// Fetch Join으로 N+1 해결
@Query("SELECT o FROM Order o JOIN FETCH o.user WHERE o.status = :status")
List<Order> findWithUserByStatus(@Param("status") OrderStatus status);

// EntityGraph
@EntityGraph(attributePaths = {"user", "items"})
List<Order> findAll();
```

## Eager vs Lazy Loading

| 전략 | 설명 | 기본값 | 주의사항 |
|------|------|--------|---------|
| **Eager Loading** | 엔티티 로드 시 연관 데이터도 즉시 조회 | `@ManyToOne`, `@OneToOne` | 불필요한 데이터까지 항상 로드 |
| **Lazy Loading** | 연관 데이터는 실제 접근 시점에 조회 | `@OneToMany`, `@ManyToMany` | 세션 외부에서 접근 시 LazyInitializationException |

**권장**: 모든 연관관계를 `LAZY`로 설정하고, 필요한 경우에만 Fetch Join으로 명시적 로드.

## ORM vs Raw SQL 트레이드오프

| 항목 | ORM (JPA/Hibernate) | Raw SQL (MyBatis, JDBC) |
|------|---------------------|------------------------|
| 생산성 | 높음. 반복적인 CRUD 코드 자동 생성 | 낮음. SQL 직접 작성 |
| 성능 제어 | 어려움. 생성된 SQL을 완전히 제어하기 힘듦 | 높음. 최적화된 SQL 직접 작성 |
| 복잡한 쿼리 | 불편. 집계, 복잡한 조인은 JPQL/Native SQL 필요 | 자연스러움 |
| DB 종속성 | 낮음. DB 교체 시 설정만 변경 | 높음. DB별 방언 직접 처리 |
| 학습 곡선 | 높음. JPA 동작 원리 이해 필요 | 낮음 |
| 적합한 상황 | 도메인 로직 중심 CRUD 애플리케이션 | 복잡한 리포트 쿼리, 대용량 배치 |

**실용적 조언**: JPA로 기본 CRUD를 처리하고, 복잡한 조회 쿼리는 QueryDSL 또는 네이티브 SQL을 병행 사용하는 것이 일반적인 패턴이다.

## Related Terms

- [[Connection-Pool]] - JPA는 커넥션 풀(HikariCP) 위에서 동작
- [[Concurrency]] - JPA 낙관적/비관적 락으로 동시성 제어
- [[Caching]] - Hibernate 1차 캐시(영속성 컨텍스트), 2차 캐시

## References

- [Spring Data JPA 공식 문서](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/)
- [Hibernate ORM 문서](https://hibernate.org/orm/documentation/)
- [N+1 문제 해결 - Baeldung](https://www.baeldung.com/spring-hibernate-n1-problem)
