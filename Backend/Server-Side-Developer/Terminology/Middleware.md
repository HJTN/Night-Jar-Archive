# Middleware (미들웨어)

## Definition

요청·응답 사이에 실행되는 공통 처리 레이어. 인증, 로깅, 에러 핸들링 등 여러 핸들러에 걸쳐 반복되는 로직을 한 곳에서 처리한다.

## 요청-응답 파이프라인에서의 역할

```
클라이언트 요청
      ↓
[Middleware 1: 로깅] → 요청 기록
      ↓
[Middleware 2: 인증] → JWT 검증, 사용자 정보 주입
      ↓
[Middleware 3: 입력 검증] → Request Body 유효성 검사
      ↓
[비즈니스 로직 핸들러] → 실제 처리
      ↓
[Middleware 3: 에러 핸들링] → 예외 캐치 및 표준 에러 응답
      ↓
[Middleware 2: 응답 압축] → gzip 압축
      ↓
[Middleware 1: 응답 로깅] → 응답 상태·소요시간 기록
      ↓
클라이언트 응답
```

미들웨어는 **체인(Chain)** 형태로 연결되고, 각 미들웨어는 다음 미들웨어를 호출하거나 체인을 조기에 끊을 수 있다.

## 미들웨어 유형별 예시

### 인증 미들웨어
```java
// Spring Security Filter
public class JwtAuthFilter extends OncePerRequestFilter {
    @Override
    protected void doFilterInternal(HttpServletRequest request,
                                    HttpServletResponse response,
                                    FilterChain chain) throws IOException, ServletException {
        String token = extractToken(request);
        if (token != null && jwtUtil.isValid(token)) {
            Authentication auth = jwtUtil.getAuthentication(token);
            SecurityContextHolder.getContext().setAuthentication(auth);
        }
        chain.doFilter(request, response); // 다음 필터로 전달
    }
}
```

### 로깅 미들웨어 (Express.js)
```javascript
app.use((req, res, next) => {
    const start = Date.now();
    res.on('finish', () => {
        console.log(`${req.method} ${req.path} ${res.statusCode} ${Date.now() - start}ms`);
    });
    next(); // 다음 미들웨어로
});
```

### 에러 핸들링 미들웨어
```java
// Spring @ControllerAdvice
@RestControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(EntityNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleNotFound(EntityNotFoundException e) {
        return ResponseEntity.status(404)
            .body(new ErrorResponse("NOT_FOUND", e.getMessage()));
    }
    
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleGeneral(Exception e) {
        log.error("Unhandled exception", e);
        return ResponseEntity.status(500)
            .body(new ErrorResponse("INTERNAL_ERROR", "서버 오류가 발생했습니다."));
    }
}
```

## Express vs Spring 미들웨어/필터 체인 비교

| 항목 | Express.js (미들웨어) | Spring (Filter/Interceptor) |
|------|---------------------|---------------------------|
| 위치 | HTTP 요청 처리 파이프라인 | Filter: 서블릿 컨테이너 레벨 / Interceptor: 스프링 MVC 레벨 |
| 등록 방식 | `app.use()` | `@Component` + 자동 등록, 또는 `WebMvcConfigurer` |
| 실행 순서 | 등록 순서대로 | `@Order` 또는 `Ordered` 인터페이스 |
| 인증/보안 | passport 등 | Spring Security (FilterChain) |
| 응답 접근 | `res` 객체 직접 조작 | `HttpServletResponse` 래핑 |

## 공통 미들웨어 목록

| 미들웨어 종류 | 역할 | Spring 구현체 |
|-------------|------|--------------|
| 인증/인가 | JWT 검증, 세션 확인 | Spring Security Filter |
| 로깅 | 요청/응답 로그 기록 | CommonsRequestLoggingFilter, 커스텀 Filter |
| CORS | Cross-Origin 요청 허용 설정 | CorsFilter |
| 압축 | gzip 응답 압축 | GzipHttpOutputMessage (자동) |
| 요청 제한 | Rate Limiting (초당 요청 수 제한) | Bucket4j + Filter |
| 에러 핸들링 | 표준 에러 응답 포맷 | `@ControllerAdvice` |
| 입력 검증 | Request Body 유효성 검사 | `@Valid` + MethodArgumentNotValidException |

## Related Terms

- [[JWT]] - JWT 검증은 인증 미들웨어에서 처리
- [[Concurrency]] - 미들웨어도 다중 스레드 환경에서 실행됨

## References

- [Spring Security Filter Chain](https://docs.spring.io/spring-security/reference/servlet/architecture.html)
- [Express.js Middleware](https://expressjs.com/en/guide/using-middleware.html)
