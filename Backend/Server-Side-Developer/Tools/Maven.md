# Maven

> Java 프로젝트 빌드·의존성 관리 도구

## Overview

Maven은 Java 프로젝트의 빌드, 의존성 관리, 테스트, 패키징, 배포를 자동화하는 도구다. `pom.xml` 파일로 프로젝트 구성을 선언적으로 정의한다. Spring Boot 프로젝트에서 Gradle과 함께 가장 많이 사용된다.

## pom.xml 구조

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project>
    <modelVersion>4.0.0</modelVersion>

    <!-- 프로젝트 식별자 -->
    <groupId>com.example</groupId>
    <artifactId>my-api</artifactId>
    <version>1.0.0-SNAPSHOT</version>
    <packaging>jar</packaging>

    <!-- Spring Boot Parent BOM: 의존성 버전 일관성 보장 -->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.2.0</version>
    </parent>

    <properties>
        <java.version>17</java.version>
    </properties>

    <!-- 의존성 -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <!-- parent에서 버전 관리 → 버전 명시 불필요 -->
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>  <!-- 테스트 클래스패스에만 포함 -->
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <scope>provided</scope>  <!-- 컴파일 시에만 필요 -->
        </dependency>
    </dependencies>

    <!-- 빌드 플러그인 -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <!-- 실행 가능한 fat jar 생성 -->
            </plugin>
        </plugins>
    </build>
</project>
```

## 빌드 라이프사이클

Maven은 순서가 정해진 **Phase**들로 구성된 라이프사이클을 따른다. 특정 Phase를 실행하면 그 이전 Phase들이 모두 순서대로 실행된다.

```
validate → compile → test → package → verify → install → deploy
```

| Phase | 동작 |
|-------|------|
| `validate` | 프로젝트 구조 유효성 검사 |
| `compile` | 소스 코드 컴파일 (`target/classes/`) |
| `test` | 단위 테스트 실행 (실패 시 빌드 중단) |
| `package` | 컴파일된 코드를 JAR/WAR로 패키징 (`target/*.jar`) |
| `verify` | 통합 테스트 실행 및 품질 검사 |
| `install` | 패키지를 로컬 Maven 저장소에 설치 (`~/.m2/`) |
| `deploy` | 패키지를 원격 저장소에 배포 (CI/CD에서 사용) |

## 주요 명령어

```bash
# 기본 빌드 (컴파일 + 테스트 + 패키징)
mvn package

# 테스트 건너뛰고 패키징 (CI 아닌 개발 중 빠른 빌드)
mvn package -DskipTests

# 특정 테스트 클래스만 실행
mvn test -Dtest=OrderServiceTest
mvn test -Dtest=OrderServiceTest#createOrder_success

# 클린 빌드 (target 디렉토리 삭제 후 재빌드)
mvn clean package

# 의존성 트리 확인 (충돌 분석에 유용)
mvn dependency:tree
mvn dependency:tree | grep spring-security

# 의존성 업데이트 확인
mvn versions:display-dependency-updates

# 로컬 저장소에 설치 (멀티 모듈 프로젝트에서 다른 모듈이 참조할 때)
mvn clean install

# Spring Boot 애플리케이션 직접 실행
mvn spring-boot:run
mvn spring-boot:run -Dspring-boot.run.profiles=local
```

## Dependency Scope

| Scope | 컴파일 | 테스트 | 런타임 JAR 포함 | 사용 예 |
|-------|--------|--------|--------------|---------|
| `compile` (기본) | O | O | O | spring-boot-starter-web |
| `test` | X | O | X | spring-boot-starter-test, junit |
| `provided` | O | O | X | lombok, servlet-api |
| `runtime` | X | O | O | DB 드라이버 (mysql-connector) |

## Maven vs Gradle 비교

| 항목 | Maven | Gradle |
|------|-------|--------|
| 설정 파일 | `pom.xml` (XML) | `build.gradle` (Groovy/Kotlin DSL) |
| 빌드 속도 | 느림 (증분 빌드 제한적) | 빠름 (증분 빌드, 캐싱) |
| 학습 곡선 | 낮음 (컨벤션 명확) | 약간 높음 (유연하지만 복잡해질 수 있음) |
| 커스터마이징 | XML로 제한적 | 코드로 유연하게 |
| 생태계 | 성숙, 레거시 프로젝트 다수 | 최신 프로젝트 선호 |

**실용적 선택**: 신규 프로젝트는 빌드 속도 우위로 Gradle을 선호하는 추세. 기존 Maven 프로젝트는 유지.

## References

- [Maven 공식 문서](https://maven.apache.org/guides/)
- [Maven Repository](https://mvnrepository.com/)
