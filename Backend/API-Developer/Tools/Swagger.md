# Swagger

> OpenAPI 스펙 기반 API 설계·문서화·코드 생성 도구

## Overview

Swagger는 OpenAPI Specification(OAS)를 기반으로 API를 설계하고 문서화하는 도구 모음이다. Spring Boot에서는 `springdoc-openapi` 라이브러리로 코드 어노테이션에서 OpenAPI 스펙을 자동 생성하고, Swagger UI로 브라우저에서 직접 API를 테스트할 수 있다.

## Key Features

- **Swagger UI**: 자동 생성된 인터랙티브 API 문서, 브라우저에서 직접 테스트
- **Swagger Editor**: YAML/JSON으로 OpenAPI 스펙 작성·검증 (editor.swagger.io)
- **Swagger Codegen**: 스펙에서 클라이언트 SDK·서버 스텁 코드 자동 생성
- **springdoc-openapi**: Spring Boot 어노테이션 → OpenAPI 스펙 자동 생성

## Installation & Setup

### Spring Boot — springdoc-openapi 연동

```xml
<!-- build.gradle (Kotlin DSL) -->
implementation("org.springdoc:springdoc-openapi-starter-webmvc-ui:2.5.0")
```

```yaml
# application.yml
springdoc:
  api-docs:
    path: /v3/api-docs
  swagger-ui:
    path: /swagger-ui.html
    operations-sorter: alpha
```

접속: `http://localhost:8080/swagger-ui.html`

## Common Usage

### 주요 어노테이션

```java
// Controller 레벨 문서화
@Tag(name = "Users", description = "사용자 관리 API")
@RestController
@RequestMapping("/v1/users")
public class UserController {

    // 엔드포인트 설명
    @Operation(
        summary = "사용자 단건 조회",
        description = "userId로 특정 사용자 정보를 조회합니다."
    )
    @ApiResponses({
        @ApiResponse(responseCode = "200", description = "조회 성공"),
        @ApiResponse(responseCode = "404", description = "사용자 없음",
            content = @Content(schema = @Schema(implementation = ErrorResponse.class)))
    })
    @GetMapping("/{userId}")
    public ResponseEntity<UserResponse> getUser(
        @Parameter(description = "사용자 ID", example = "1")
        @PathVariable Long userId
    ) { ... }
}

// DTO 스펙 문서화
@Schema(description = "사용자 생성 요청")
public record CreateUserRequest(
    @Schema(description = "이름", example = "홍길동", required = true)
    @NotBlank String name,

    @Schema(description = "이메일", example = "hong@example.com")
    @Email String email
) {}
```

### OpenAPI 전역 설정

```java
@Configuration
public class OpenApiConfig {

    @Bean
    public OpenAPI openAPI() {
        return new OpenAPI()
            .info(new Info()
                .title("Example API")
                .description("API 문서")
                .version("v1.0.0"))
            .components(new Components()
                .addSecuritySchemes("bearerAuth",
                    new SecurityScheme()
                        .type(SecurityScheme.Type.HTTP)
                        .scheme("bearer")
                        .bearerFormat("JWT")))
            .addSecurityItem(new SecurityRequirement().addList("bearerAuth"));
    }
}
```

## Tips & Shortcuts

- `/v3/api-docs` 엔드포인트에서 OpenAPI JSON 다운로드 → Postman에 임포트 가능
- `@Hidden` 어노테이션으로 내부 API를 문서에서 숨길 수 있음
- Swagger UI에서 `Authorize` 버튼으로 JWT 토큰 입력 후 인증 API 테스트
- `springdoc.packages-to-scan`으로 특정 패키지만 스캔해 성능 최적화

## References

- [springdoc-openapi 공식 문서](https://springdoc.org/)
- [OpenAPI 3.0 스펙](https://spec.openapis.org/oas/v3.0.3)
- [Swagger Editor (온라인)](https://editor.swagger.io/)
