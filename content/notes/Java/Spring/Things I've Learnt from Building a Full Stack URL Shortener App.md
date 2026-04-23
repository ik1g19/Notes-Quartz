---
custom-width: 24
---
Typical Spring project structure:
- **Controller**: receives HTTP requests, returns responses
- **Service**: business logic
- **Repository**: DB access
- **Entity**: persistence model
- **DTO**: API request/response models
- **Exception handling**: centralised errors with `@ControllerAdvice`

Spring modules used:
- Spring Web
- Spring Data JPA
- PostgreSQL driver
- Bean Validation
- Lombok optionally
- Spring Security later if adding auth

`pom.xml` holds the Spring dependencies, Spring initializr configures this for you

# Postgres Setup - Docker

The backend needs a db to run, I installed the official postgres container using

```shell
docker pull postgres
```

Started a container using

```shell
docker run -itd -e POSTGRES_USER=myuser -e POSTGRES_PASSWORD=mypassword -p 5432:5432 --name mypostgres postgres
```

Then connected using the `psql` terminal using

```shell
PGPASSWORD=mypassword psql -h localhost -p 5432 -U myuser
```

Then use `\l` to list the databases

To connect using the `psql` client I used

```shell
docker exec -it mypostgres psql -U myuser 
```

In `psql` I made a database with

```sql
CREATE DATABASE url_shortener;
```

# Postgres Setup - Podman

```shell
podman pull postgres:latest
```

```shell
podman volume create postgresapp
```

```shell
podman run -dt --name my-postgres -e POSTGRES_PASSWORD=1234 -p 5432:5432 postgres
```

`-e` is used to specify environment variables
`-dt` runs in detached mode

```shell
podman exec -it my-postgres psql -U postgres
```

## Spring Postgres Setup

```
spring.datasource.url=jdbc:postgresql://localhost:5432/url_shortener
spring.datasource.username=app_user
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

### Example Project Structure

```
com.company.project  
├── ProjectApplication.java  
├── config  
│   ├── SecurityConfig.java  
│   ├── DatabaseConfig.java  
│   └── SwaggerConfig.java  
├── controller  
│   ├── UserController.java  
│   └── ProductController.java  
├── service  
│   ├── UserService.java  
│   ├── UserServiceImpl.java  
│   ├── ProductService.java  
│   └── ProductServiceImpl.java  
├── repository  
│   ├── UserRepository.java  
│   └── ProductRepository.java  
├── model  
│   ├── entity  
│   │   ├── User.java  
│   │   └── Product.java  
│   └── dto  
│       ├── UserDTO.java  
│       ├── CreateUserRequest.java  
│       └── ProductDTO.java  
├── exception  
│   ├── GlobalExceptionHandler.java  
│   ├── ResourceNotFoundException.java  
│   └── ValidationException.java  
├── mapper  
│   ├── UserMapper.java  
│   └── ProductMapper.java  
├── security  
│   ├── JwtTokenProvider.java  
│   └── CustomUserDetailsService.java  
└── util  
    ├── DateUtil.java  
    └── ValidationUtil.java
```

# Creating First Entity

```java
@Entity
@Table(name = "short_urls")
public class ShortUrl {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false, length = 2048)
    private String originalUrl;

    @Column(nullable = false, unique = true, length = 20)
    private String shortCode;

    @Column(nullable = false)
    private LocalDateTime createdAt;

    @Column(nullable = false)
    private Long clickCount = 0L;

    // getters/setters
}
```

IntelliJ lets you generate Getter/Setters

`Code>Generate>Getters/Setters` or `Alt` `Insert`


> [!INFO] Entiity
> Represents a table in the database
> Each instance of the class corresponds to a row in the table
> Class=table
> Object=row
> Fields=columns

[[Spring Boot 3 Notes#JPA Annotations|My Udemy Notes on this]]

| Annotation                                            | Meaning                                                                                                                 |
| ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `@Entity`                                             | Tells JPA (Java Persistence API) that this class should be treated as a database entity                                 |
| `@Table(name = "short_urls")`                         | Specifies the exact table name in the database                                                                          |
| `@Id`                                                 | Marks the field as the primary key of the table                                                                         |
| `@GeneratedValue(strategy = GenerationType.IDENTITY)` | Controls how the ID is generated<br><br>`IDENTITY` means the database auto-generates it (e.g., auto-increment in MySQL) |
| `@Column(...)`                                        | Defines how each field maps to a column in the database                                                                 |

Connect to pg database to verify table was created by Hibernate

```postgres
\connect url_shortener
```

# Create Repository

> [!INFO] Repository
> An interface that represents a collection of operations mapped to a specific domain model or entity

```java
@Repository
public interface ShortUrlRepository extends JpaRepository<ShortUrlEntity, Long> {
    Optional<ShortUrlEntity> findByShortCode(String shortCode);
    boolean existsByShortCode(String shortCode);
}
```

Spring (via Spring Data JPA) **generates the implementation for you at runtime**.

> [!INFO]
> At startup:
> 
> 1. Spring scans for repository interfaces
> 2. It sees your `ShortUrlRepository`
> 3. It creates a **proxy class** (a runtime-generated implementation)
> 4. That proxy is what gets injected into your service
> 
> 👉 So when you call:
> 
> `shortUrlRepository.findByShortCode(shortCode);`
> 
> you’re actually calling a **generated implementation**, not the interface itself.

Spring parses the method name:

```java
findByShortCode
```

and interprets it as:

```SQL
 SELECT * FROM short_urls WHERE short_code = ?
```

It builds the query automatically using naming conventions.

# Create Service

> [!INFO] Repository vs Controller vs Service
> - **Controller layer**: Handles HTTP requests and routes them to the correct services.
> - **Service layer**: Contains business logic — how things work in your app. _@Service_ annotates classes at the service layer
> - **Repository layer**: Talks to the database. _@Repository_ annotates classes at the persistence layer, which will act as a database repository.

```java
@Service
public class ShortUrlService {

    private final ShortUrlRepository shortUrlRepository;

    public ShortUrlService(ShortUrlRepository shortUrlRepository) {
        this.shortUrlRepository = shortUrlRepository;
    }

    public ShortUrlEntity create(String originalUrl) {
        ShortUrlEntity shortUrl = new ShortUrlEntity();
        shortUrl.setOriginalUrl(originalUrl);
        shortUrl.setShortCode(UUID.randomUUID().toString().substring(0, 6));
        shortUrl.setCreatedAt(LocalDateTime.now());
        shortUrl.setClickCount(0L);

        return shortUrlRepository.save(shortUrl);
    }

    public Optional<ShortUrlEntity> findByShortCode(String shortCode) {
        return shortUrlRepository.findByShortCode(shortCode);
    }
}
```

> [!INFO]
> When you call something like:
> 
> ```java
> shortUrlRepository.save(entity);
> ```
> 
> you’re using a Spring Data JPA repository (part of Spring Data JPA).
> 
> 👉 `save()` tells JPA/Hibernate:
> 
> > “Make the database reflect this object.”

## What Hibernate does:

### 1. If the entity is **new** (no ID yet)

- JPA performs an **INSERT**
- A new row is created in the table

```SQL
INSERT INTO short_urls (...)
```

### 2. If the entity already exists (has an ID)

- JPA performs an **UPDATE**

```SQL
UPDATE short_urls SET ... WHERE id = ?
```

Calling `save()` does **not always instantly hit the database**.

JPA uses something called a **persistence context**:

- Your entity becomes “managed”
- Changes may be delayed until:
    - transaction commit
    - or a flush happens

## Why the returned object matters

```java
ShortUrlEntity saved = repository.save(entity);
```

- `saved` may contain:
    - generated ID
    - updated fields
- Always use the returned object going forward

# Create Endpoint (`POST`)

## Create request DTO

```java
public class CreateShortUrlRequest {

    @NotBlank
    private String originalUrl;

    public void setOriginalUrl(String originalUrl) {
        this.originalUrl = originalUrl;
    }
}
```

> [!INFO] DTO - Data Transfer Objects
> - **POJOs that serve as data carriers between processes, layers, or services**
> - Their only purpose is to define the shape of the data passed to or from the client

# Create controller

```java
@RestController
@RequestMapping("/api/urls")
public class ShortUrlController {

    private final ShortUrlService shortUrlService;

    public ShortUrlController(ShortUrlService shortUrlService) {
        this.shortUrlService = shortUrlService;
    }

    @PostMapping
    public ResponseEntity<ShortUrlEntity> createShortUrl(@Valid @RequestBody CreateShortUrlRequest request) {
        ShortUrlEntity saved = shortUrlService.create(request.getOriginalUrl());
        return ResponseEntity.ok(saved);
    }
}
```

The parameter to `ok` is the body of the response

# Security Config for Disabling CSRF

I had to add this security configuration for the API to allow me to make POST requests without a CSRF token for now

```java
@Configuration
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
                .csrf(AbstractHttpConfigurer::disable)
                .sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
                .authorizeHttpRequests(auth -> auth.anyRequest().authenticated())
                .httpBasic(Customizer.withDefaults())
                .formLogin(AbstractHttpConfigurer::disable);

        return http.build();
    }
}
```