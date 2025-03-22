# Spring 핵심 구조 요약

Spring은 Java 기반의 애플리케이션을 개발하기 위한 프레임워크로, 복잡한 설정 없이도 효율적인 웹 백엔드를 개발할 수 있게 해준다.

## 1. 전체 구조 개요

Spring Boot 프로젝트는 보통 아래와 같은 계층 구조를 따른다


Controller → Service → Repository → Database
                        ↓
                  (Domain/Entity)

- Controller: HTTP 요청/응답 처리
- Service: 비즈니스 로직 처리
- Repository: DB 접근 (JPA 등 사용)
- Domain: 엔티티 객체, 테이블과 1:1 매핑

---

## 2. 주요 애노테이션

- `@RestController`: JSON 형태의 응답을 제공하는 컨트롤러
- `@Service`: 비즈니스 로직 계층을 나타냄
- `@Repository`: DB와의 통신 담당 (JPA 인터페이스 주입됨)
- `@Entity`: 데이터베이스 테이블과 매핑되는 클래스
- `@Autowired`: 의존성 주입 (DI)

---

## 3. DI와 IoC

- **DI(Dependency Injection)**: 객체 간 의존성을 직접 생성하지 않고 외부에서 주입 받는 방식
- **IoC(Inversion of Control)**: 객체 생성과 관리를 개발자가 아닌 Spring이 제어

예시
```java
@Service
public class BookService {
    private final BookRepository bookRepository;

    @Autowired
    public BookService(BookRepository bookRepository) {
        this.bookRepository = bookRepository;
    }
}
```

---

## 4. 예외 처리

- `@ControllerAdvice` + `@ExceptionHandler` 조합으로 전역 예외 처리 가능
- 응답 통일성 확보 및 예외 발생 시 사용자에게 명확한 메시지 제공

---

## 5. 테스트 전략

- `@WebMvcTest`: Controller 단위 테스트
- `@SpringBootTest`: 통합 테스트
- `MockMvc`: 실제 HTTP 요청 시뮬레이션

---

## 6. 보안 (Spring Security)

- JWT, 세션, OAuth2 등 인증 방식 설정 가능
- `SecurityFilterChain`으로 보안 필터 정의

---

## 7. RestDocs로 API 문서 자동화

- 테스트 코드에 기반하여 Swagger 없이도 자동 문서화 가능

```java
this.mockMvc.perform(get("/api/users"))
  .andExpect(status().isOk())
  .andDo(document("user-list"));
```

---

## 8. 설정 파일

- `application.yml` 또는 `application.properties`
- DB 설정, 포트, 로그 등 전반적인 환경 설정 포함

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: user
    password: pass
```

---

## 9. 폴더 구조 예시

```
src
└── main
    ├── java
    │   └── com.example.project
    │       ├── controller
    │       ├── service
    │       ├── repository
    │       ├── domain
    │       └── config
    └── resources
        ├── application.yml
        └── static/templates
```

---

## 10. 자주 사용하는 의존성 (Gradle 기준)

```groovy
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    implementation 'org.springframework.boot:spring-boot-starter-security'
    implementation 'com.mysql:mysql-connector-j'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
}
```

---

추가로 공부한 내용은 각 항목별 `.md` 파일로 분리해서 링크 연결 예정.
