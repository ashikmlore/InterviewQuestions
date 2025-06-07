### 1. What is Spring Boot? Why do we use it?
Answer:
Spring Boot is a tool that helps us build standalone, production-ready Spring applications easily. It removes a lot of configuration work and adds default settings so we can focus on writing code.

Why we use it:

- No need for complex XML configuration

- Has built-in server like Tomcat

- Auto-configuration of components

- Faster development

Example:
```bash
@SpringBootApplication
public class MyApp {
  public static void main(String[] args) {
    SpringApplication.run(MyApp.class, args);
  }
}
```
### 2. What is @SpringBootApplication?
Answer:
It’s a combination of three annotations:

- **@Configuration:** marks class as source of bean definitions

- **@EnableAutoConfiguration:** auto-configures beans

- **@ComponentScan:** scans for components in package

Example:
```bash
@SpringBootApplication
public class MyApp { }
```
This is like telling Spring Boot: "Start here!"

### 3. What is dependency injection in Spring Boot?
Answer:
Dependency Injection (DI) means Spring creates objects (like services or components) and gives them to your classes so you don’t create them manually.

Example:
```bash
@Service
public class MyService {
  public String getMessage() {
    return "Hello";
  }
}

@RestController
public class MyController {
  private final MyService myService;

  public MyController(MyService myService) {
    this.myService = myService;
  }

  @GetMapping("/")
  public String hello() {
    return myService.getMessage();
  }
}
```
Here, Spring injects MyService into MyController.

### 4. What is a REST API in Spring Boot?
Answer:
REST API allows us to expose data using HTTP methods (GET, POST, PUT, DELETE).

Example:
```bash
@RestController
public class HelloController {

  @GetMapping("/hello")
  public String sayHello() {
    return "Hello World!";
  }
}
```
Visiting /hello will show "Hello World!"

### 5. What is @RestController?
Answer:
@RestController = @Controller + @ResponseBody.

It means the method returns data (like JSON), not a webpage.

### 6. How do you connect to a database in Spring Boot?
Answer:
Use application.properties or application.yml file:

properties
```bash
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=pass
spring.jpa.hibernate.ddl-auto=update
```
Add JPA dependency and create entity + repository:

```bash
@Entity
public class User {
  @Id
  @GeneratedValue
  private Long id;
  private String name;
}


public interface UserRepository extends JpaRepository<User, Long> { }
```
### 7. What is @Entity and @Id?
Answer:

- @Entity: Tells Spring this class maps to a database table.

- @Id: Marks the primary key field.

### 8. What is Spring Boot Starter?
Answer:
Starters are dependencies that include everything needed for a specific feature.

Example:

- spring-boot-starter-web: for web apps

- spring-boot-starter-data-jpa: for database access with JPA

- spring-boot-starter-security: for security features

You add them in pom.xml (Maven) or build.gradle.

### 9. What is application.properties or application.yml?
Answer:
This file stores configuration like:

- Database settings

- Server port

- Custom properties

Example:

properties
```bash
server.port=8081
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
```
### 10. How do you handle exceptions in Spring Boot?
Answer:
Use @ControllerAdvice and @ExceptionHandler.

Example:

```bash
@ControllerAdvice
public class GlobalExceptionHandler {
  @ExceptionHandler(Exception.class)
  public ResponseEntity<String> handleAll(Exception e) {
    return new ResponseEntity<>("Something went wrong", HttpStatus.INTERNAL_SERVER_ERROR);
  }
}
```

### 11. How do you validate user input in Spring Boot?
Answer:
Use annotations like @NotNull, @Email, @Size with @Valid.

Example:
```bash
public class UserDTO {
  @NotBlank
  private String name;

  @Email
  private String email;
}

@RestController
public class UserController {

  @PostMapping("/users")
  public String createUser(@RequestBody @Valid UserDTO user) {
    return "User created";
  }
}
```
If invalid data is sent, Spring returns a helpful error automatically.

### 12. What is @Autowired?
Answer:
@Autowired tells Spring to inject (give) the required dependency automatically.

Example:
```bash
@Service
public class MyService { }

@RestController
public class MyController {

  @Autowired
  private MyService service;

}
```
### 13. What is the difference between @Component, @Service, and @Repository?
Answer:

All are special types of @Component, but used for different layers:

Annotation	Purpose
@Component	Generic Spring bean
@Service	Business logic layer
@Repository	Data access layer (handles DB errors)

### 14. How do you handle different HTTP methods in Spring Boot?
Answer:
Use these annotations:

- @GetMapping – for reading data

- @PostMapping – for creating data

- @PutMapping – for updating

- @DeleteMapping – for deleting

Example:
```bash
@GetMapping("/users")
public List<User> getUsers() { }

@PostMapping("/users")
public User createUser(@RequestBody User user) { }

@PutMapping("/users/{id}")
public User updateUser(@PathVariable Long id, @RequestBody User user) { }

@DeleteMapping("/users/{id}")
public void deleteUser(@PathVariable Long id) { }
```

### 15. What is @PathVariable and @RequestParam?
Answer:

- @PathVariable: Gets value from URL

- @RequestParam: Gets value from query string

Example:

```bash
@GetMapping("/hello/{name}")
public String sayHello(@PathVariable String name) {
  return "Hello " + name;
}

@GetMapping("/greet")
public String greet(@RequestParam String name) {
  return "Hi " + name;
}
```

### 16. How do you create a custom response object?
Answer:
You can create your own class and return it.

```bash
public class ApiResponse {
  private String status;
  private Object data;

  // constructors, getters, setters
}

@RestController
public class UserController {
  @GetMapping("/user")
  public ApiResponse getUser() {
    return new ApiResponse("success", new User("Ram"));
  }
}
```
### 17. What is @RequestBody and @ResponseBody?
Answer:

- @RequestBody: Takes JSON from the request and converts it to Java object

- @ResponseBody: Converts Java object to JSON for response

In @RestController, this is automatic.

### 18. How do you test a Spring Boot app?
Answer:
Use JUnit and Spring Boot test support.

Example:
```bash
@SpringBootTest
class MyAppTests {

  @Test
  void contextLoads() {
    // Checks if the app starts correctly
  }
}
```

### 19. How to change the default port of Spring Boot?
Answer:
Change it in application.properties:

properties
```bash
server.port=8081
```

### 20. What is Spring Data JPA?
Answer:
Spring Data JPA simplifies database access using interfaces.

Example:

```bash
public interface UserRepository extends JpaRepository<User, Long> {
  List<User> findByName(String name);
}
```
You don’t write SQL – Spring does it for you.

### 21. What is Actuator in Spring Boot?
Answer:
Spring Boot Actuator provides ready-made endpoints to monitor and manage your app (like health, metrics, etc.).

Add this to pom.xml:

```bash
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```
Visit /actuator/health, /actuator/info, etc.

### 22. What is DevTools in Spring Boot?
Answer:
DevTools allows automatic restart and live reload during development.

Add to pom.xml:
```bash
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-devtools</artifactId>
  <scope>runtime</scope>
</dependency>
```
### 23. What is the default server used in Spring Boot?
Answer:
By default, Spring Boot uses Tomcat as the embedded server.

### 24. How to return custom HTTP status codes?
Answer:
Use ResponseEntity.

Example:

```bash
@GetMapping("/status")
public ResponseEntity<String> getStatus() {
  return new ResponseEntity<>("All good", HttpStatus.OK);
}
```
### 25. How to enable CORS in Spring Boot?
Answer:
Use @CrossOrigin on controller/method.

Example:
```bash
@CrossOrigin(origins = "http://localhost:3000")
@RestController
public class MyController { }
```


### 26. What are Spring Profiles?
Answer:
Profiles let you define different configurations for different environments like dev, test, or prod.

Example:

application-dev.properties
```bash
server.port=8081
```
application-prod.properties
```bash
server.port=80
```
Activate profile:
```bash
spring.profiles.active=dev
```
### 27. What is @Scheduled in Spring Boot?
Answer:
@Scheduled is used to run methods at specific intervals (like a cron job).

Example:
```bash
@Component
public class MyTask {

  @Scheduled(fixedRate = 5000)
  public void runTask() {
    System.out.println("Runs every 5 seconds");
  }
}
```
To enable it:
```bash
@SpringBootApplication
@EnableScheduling
public class MyApp { }
```
### 28. What is Spring Security?
Answer:
Spring Security is used to secure your application using login, roles, etc.

Default behavior:

- Basic login form

- Auto-generated password (shown in console)

To customize:

```bash
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
  @Override
  protected void configure(HttpSecurity http) throws Exception {
    http
      .authorizeRequests()
      .antMatchers("/public").permitAll()
      .anyRequest().authenticated()
      .and()
      .formLogin();
  }
}
```

### 29. What is Caching in Spring Boot?
Answer:
Caching stores data temporarily to improve performance.

Enable with:

```bash
@SpringBootApplication
@EnableCaching
public class MyApp { }
```
Example:

```bash
@Service
public class ProductService {

  @Cacheable("products")
  public List<Product> getAllProducts() {
    // fetch from DB
  }
}
```

### 30. How do you upload a file in Spring Boot?
Answer:
Use MultipartFile.

Example:
```bash
@PostMapping("/upload")
public String handleFileUpload(@RequestParam("file") MultipartFile file) {
  // save file
  return "File uploaded";
}
```
Also add:

properties
```bash
spring.servlet.multipart.max-file-size=5MB
spring.servlet.multipart.max-request-size=5MB
```

### 31. How to create a custom exception in Spring Boot?
Answer:
Create a class that extends RuntimeException.

```bash
public class UserNotFoundException extends RuntimeException {
  public UserNotFoundException(String msg) {
    super(msg);
  }
}
```
Handle it:

```bash
@ControllerAdvice
public class ExceptionHandlerClass {
  @ExceptionHandler(UserNotFoundException.class)
  public ResponseEntity<String> handle(UserNotFoundException ex) {
    return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
  }
}
```

### 32. What is CommandLineRunner?
Answer:
It lets you run code just after the application starts.

Example:

```bash
@Component
public class StartupRunner implements CommandLineRunner {
  public void run(String... args) {
    System.out.println("App started!");
  }
}
```

### 33. What is the difference between @GetMapping and @RequestMapping(method = RequestMethod.GET)?
Answer:
Both do the same thing. @GetMapping is a shortcut.

```bash
@GetMapping("/hello") // simpler
@RequestMapping(value = "/hello", method = RequestMethod.GET) // longer
```

### 34. What is H2 Database?
Answer:
H2 is an in-memory database used for testing and development.

Add to pom.xml:
```bash
<dependency>
  <groupId>com.h2database</groupId>
  <artifactId>h2</artifactId>
</dependency>
```
Access console at: http://localhost:8080/h2-console

### 35. What is the difference between @Bean and @Component?
| Annotation   | Meaning                                                         |
|--------------|-----------------------------------------------------------------|
| `@Component` | Used on classes to auto-detect and register as Spring beans     |
| `@Bean`      | Used inside `@Configuration` classes to manually define a bean  |


Example:
```bash
@Configuration
public class AppConfig {

  @Bean
  public MyService myService() {
    return new MyService();
  }
}
```

### 36. What is @Configuration?
Answer:
Tells Spring that this class has bean definitions using @Bean.

### 37. What is the use of application.yml instead of application.properties?
Answer:
application.yml allows a cleaner hierarchical structure.

Example:

yaml
```bash
server:
  port: 8080

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
```

### 38. How do you call another API from Spring Boot?
Answer:
Use **RestTemplate** or **WebClient**.

RestTemplate example:

```bash
@Autowired
RestTemplate restTemplate;

public String callApi() {
  return restTemplate.getForObject("https://api.example.com/data", String.class);
}
```

### 39. What is @Value?
Answer:
It injects values from properties file into your class.

Example:

properties
```bash
app.name=My Spring App
```
```bash
@Value("${app.name}")
private String appName;
```

### 40. What is the difference between Monolith and Microservice?
Monolith	Microservice
All in one app	Divided into small independent services
Easier to develop	Easier to scale
Harder to maintain as it grows	More flexible, harder to manage without proper tools



### 41. What is the difference between @RestController and @Controller?
Answer:

| Annotation       | Used For               | Response Type             |
|------------------|------------------------|----------------------------|
| `@Controller`    | MVC (web page)         | Returns view (HTML/JSP)   |
| `@RestController`| REST APIs (JSON responses) | Returns JSON or XML    |


### 42. What is a filter in Spring Boot?
Answer:
A filter is used to perform tasks before and after a request is processed by a controller, like logging, authentication, etc.

Example:

```bash
@Component
public class MyFilter implements Filter {
  public void doFilter(ServletRequest req, ServletResponse res, FilterChain chain)
      throws IOException, ServletException {
    System.out.println("Request passed through filter");
    chain.doFilter(req, res);
  }
}
```

### 43. What is an interceptor?
Answer:
Interceptors are similar to filters but more powerful. They work at the Spring MVC level.

Example:

```bash
public class MyInterceptor implements HandlerInterceptor {
  public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) {
    System.out.println("Before controller");
    return true;
  }
}
```
Register it:

```bash
@Configuration
public class WebConfig implements WebMvcConfigurer {
  public void addInterceptors(InterceptorRegistry registry) {
    registry.addInterceptor(new MyInterceptor());
  }
}
```

### 44. How do you log in Spring Boot?
Answer:
Use SLF4J with Spring Boot’s built-in logging.

Example:
```bash
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

@RestController
public class MyController {
  private static final Logger logger = LoggerFactory.getLogger(MyController.class);

  @GetMapping("/log")
  public String logExample() {
    logger.info("This is an info message");
    return "Check console";
  }
}
```

### 45. How do you read values from application.properties or application.yml into a class?
Answer:
Use @ConfigurationProperties.

Example:

properties
```bash
app.name=Spring Boot App
```

```bash
@Component
@ConfigurationProperties(prefix = "app")
public class AppConfig {
  private String name;

  // getter and setter
}
```
### 46. What is a DTO in Spring Boot?
Answer:
DTO = Data Transfer Object.
It’s a simple class used to transfer data between layers without exposing your entity directly.

Example:
```bash
public class UserDTO {
  private String name;
  private String email;
}
```

### 47. What is ResponseEntity?
Answer:
ResponseEntity is used to return data along with HTTP status codes, headers, etc.

Example:
```bash
@GetMapping("/response")
public ResponseEntity<String> getResponse() {
  return new ResponseEntity<>("OK", HttpStatus.OK);
}
```
### 48. How do you handle errors globally in Spring Boot?
Answer:
Use @ControllerAdvice.

Example:
```bash
@ControllerAdvice
public class GlobalExceptionHandler {

  @ExceptionHandler(Exception.class)
  public ResponseEntity<String> handleAll(Exception ex) {
    return new ResponseEntity<>("Error: " + ex.getMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
  }
}
```

### 49. How do you secure only certain endpoints?
Answer:
Use role-based access in your SecurityConfig.

Example:
```bash
@Override
protected void configure(HttpSecurity http) throws Exception {
  http
    .authorizeRequests()
    .antMatchers("/public").permitAll()
    .antMatchers("/admin").hasRole("ADMIN")
    .anyRequest().authenticated()
    .and()
    .formLogin();
}
```

### 50. What is the difference between @Entity and @Table?
Answer:

Annotation	Purpose
@Entity	Tells Spring it’s a JPA entity
@Table	(Optional) Specify table name

Example:
```bash
@Entity
@Table(name = "users")
public class User {
  @Id
  private Long id;
}
```

### 51. What is the use of @Transactional?
Answer:
@Transactional makes sure all DB operations in a method are completed successfully — or none at all (rollback on error).

Example:
```bash
@Transactional
public void saveData() {
  userRepo.save(user1);
  userRepo.save(user2); // if this fails, user1 is also rolled back
}
```

### 52. How do you connect to a MySQL/PostgreSQL DB in Spring Boot?
Answer:
Add the dependency and configure:

properties
```bash
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=root
spring.jpa.hibernate.ddl-auto=update
```
### 53. How do you avoid exposing sensitive data in REST responses?
Answer:

- Use DTOs instead of entities

- Use @JsonIgnore to hide specific fields

Example:
```bash
@JsonIgnore
private String password;
```

### 54. How can you return a custom message when no data is found?
Answer:
Throw a custom exception when data is not found.

```bash
if (user == null) {
  throw new UserNotFoundException("User not found");
}
```
And handle it using @ControllerAdvice.

### 55. What are the common HTTP status codes and their meanings?
| Code | Meaning                   |
|------|---------------------------|
| 200  | OK                        |
| 201  | Created                   |
| 400  | Bad Request               |
| 401  | Unauthorized              |
| 403  | Forbidden                 |
| 404  | Not Found                 |
| 500  | Internal Server Error     |


## Spring Boot Actuator
### 1. What is Spring Boot Actuator and what is it used for?
Answer:
Spring Boot Actuator is a sub-project that provides production-ready features to help monitor and manage your application. It includes:

- Endpoints: Exposes operational information via HTTP or JMX (health, metrics, info, etc.)

- Health indicators: Shows application health (database, disk space, custom checks)

- Metrics: Application metrics that can be exported to monitoring systems

- Auditing: Security-related auditing events

- HTTP Tracing: Shows recent HTTP requests

To use it, add the spring-boot-starter-actuator dependency and configure endpoints in application.properties.

### 2. How do you secure Actuator endpoints?
Answer:
To secure Actuator endpoints:

- Add Spring Security dependency (spring-boot-starter-security)

- Configure security in application.properties:

properties
```bash
management.endpoints.web.exposure.include=health,info
management.endpoint.health.show-details=when_authorized
```

- Create a security configuration class:

java
```bash
@Configuration
public class ActuatorSecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
            .requestMatchers(EndpointRequest.toAnyEndpoint()).hasRole("ADMIN")
            .anyRequest().permitAll()
            .and()
            .httpBasic();
    }
}
```


## REST and Web
### 1. How do you create a RESTful web service in Spring Boot?
Answer:
To create a RESTful service in Spring Boot:

- Add spring-boot-starter-web dependency

- Create a controller class with @RestController

- Define methods with appropriate HTTP method annotations (@GetMapping, @PostMapping, etc.)

- Use @RequestMapping at class level for base path

- Return objects which will be automatically converted to JSON/XML

Example:

```bash
@RestController
@RequestMapping("/api/products")
public class ProductController {
    
    @Autowired
    private ProductService productService;
    
    @GetMapping
    public List<Product> getAllProducts() {
        return productService.findAll();
    }
    
    @GetMapping("/{id}")
    public Product getProduct(@PathVariable Long id) {
        return productService.findById(id);
    }
    
    @PostMapping
    public Product createProduct(@RequestBody Product product) {
        return productService.save(product);
    }
}
```
### 12. How can you handle exceptions in Spring Boot REST applications?
Answer:
Several approaches for exception handling:

- **@ExceptionHandler:** Controller-specific exception handling

```bash
@ExceptionHandler(ProductNotFoundException.class)
public ResponseEntity<String> handleProductNotFound(ProductNotFoundException ex) {
    return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
}
```
- **@ControllerAdvice:** Global exception handling

```bash
@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleAllExceptions(Exception ex) {
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
                .body("Error occurred: " + ex.getMessage());
    }
}
```

- **ResponseStatusException:** For simple cases
```bash
@GetMapping("/{id}")
public Product getProduct(@PathVariable Long id) {
    return productService.findById(id)
            .orElseThrow(() -> new ResponseStatusException(
                HttpStatus.NOT_FOUND, "Product not found"));
}
```
- **Custom Error Response Structure:**

```bash
public class ErrorDetails {
    private Date timestamp;
    private String message;
    private String details;
    // constructor, getters, setters
}

@ExceptionHandler(ResourceNotFoundException.class)
public ResponseEntity<ErrorDetails> handleResourceNotFound(ResourceNotFoundException ex) {
    ErrorDetails errorDetails = new ErrorDetails(new Date(), ex.getMessage(), 
        "Resource not found");
    return new ResponseEntity<>(errorDetails, HttpStatus.NOT_FOUND);
}
```


## Advanced Topics
### 1. How does Spring Boot support microservices architecture?
Answer:
Spring Boot is well-suited for microservices through:

1. **Spring Cloud:** Provides tools for common microservice patterns

- Service discovery (Eureka, Consul, Zookeeper)

- Client-side load balancing (Ribbon)

- API Gateway (Spring Cloud Gateway)

- Circuit Breaker (Resilience4j, Hystrix)

- Distributed configuration (Spring Cloud Config)

2. **Embedded Servers:** Each microservice can run independently

3. **Actuator:** Provides health checks and metrics

4. **Spring Cloud Sleuth:** Distributed tracing

5. **Feign Client:** Declarative REST client

6. **Docker Support:** Easy containerization with Spring Boot

### 2. Explain Spring Boot's externalized configuration.
Answer:
Spring Boot allows externalizing configuration so you can work with the same code in different environments. Configuration can come from:

1. Properties files: application.properties or application.yml (in classpath, current directory, or specific location)

2. Profile-specific files: application-{profile}.properties

3. Environment variables

4. Command line arguments

5. JNDI attributes

6. System properties

The properties are loaded in a specific order (later sources override earlier ones):

1. Default properties (specified by SpringApplication.setDefaultProperties)

2. @PropertySource annotations

3. Config data (application.properties/yml files)

4. RandomValuePropertySource

5. OS environment variables

6. Java System properties

7. Command line arguments

Example of using external config:

```bash
@Value("${app.message}")
private String message;

// Or type-safe approach
@ConfigurationProperties(prefix = "app")
public class AppConfig {
    private String message;
    // getter, setter
}
```

### 3. How do you implement caching in Spring Boot?
Answer:
Spring Boot provides caching abstraction through Spring Cache:

1. **Add dependency:** spring-boot-starter-cache

2. **Enable caching:** @EnableCaching on main class

3. **Configure cache provider (in application.properties):**

properties
```bash
spring.cache.type=redis
spring.redis.host=localhost
spring.redis.port=6379
```
4. **Annotate methods:**

- **@Cacheable** - cache method results

- **@CacheEvict** - remove entries from cache

- **@CachePut** - update cache without interfering method execution

- **@Caching** - group multiple cache operations

- **@CacheConfig** - shared cache settings at class level

Example:

```bash
@Service
public class ProductService {
    
    @Cacheable(value = "products", key = "#id")
    public Product getProductById(Long id) {
        // expensive operation
        return productRepository.findById(id).orElseThrow();
    }
    
    @CacheEvict(value = "products", key = "#product.id")
    public Product updateProduct(Product product) {
        return productRepository.save(product);
    }
}
```

### 4. How do you implement security in Spring Boot applications?
Answer:
Spring Security with Spring Boot:

1. **Add dependency:** spring-boot-starter-security

2. **Basic configuration** (auto-configured security with default user)

3. **Customize security:**

```bash
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
            .antMatchers("/public/**").permitAll()
            .antMatchers("/admin/**").hasRole("ADMIN")
            .anyRequest().authenticated()
            .and()
            .formLogin()
            .and()
            .httpBasic();
    }
    
    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.inMemoryAuthentication()
            .withUser("user").password("{noop}password").roles("USER")
            .and()
            .withUser("admin").password("{noop}admin").roles("ADMIN");
    }
}
```
4. **Method-level security:** Use @PreAuthorize, @PostAuthorize, @Secured

5. **Password encoding:** Always encode passwords with PasswordEncoder

6. **OAuth2:** Use spring-security-oauth2 for OAuth support

7. **JWT:** Implement JWT for stateless authentication

### 4. How do you implement internationalization (i18n) in Spring Boot?
Answer:
Spring Boot provides auto-configuration for internationalization:

1. Create message files (e.g., messages.properties, messages_fr.properties)

2. Configure in application.properties:

properties
```bash
spring.messages.basename=messages
spring.messages.encoding=UTF-8
```
3. Use in controllers:

```bash
@RestController
public class GreetingController {
    
    @Autowired
    private MessageSource messageSource;
    
    @GetMapping("/greeting")
    public String greeting(@RequestHeader(name="Accept-Language", required=false) 
                          Locale locale) {
        return messageSource.getMessage("greeting.message", null, locale);
    }
}
```
4. Locale resolution: Can be done via:

- Session attribute

- Cookie

- Accept-Language header (default)

- Custom resolver implementing LocaleResolver

### 5. How do you schedule tasks in Spring Boot?
Answer:
Spring Boot provides task scheduling through Spring's @Scheduled annotation:

1. Enable scheduling: @EnableScheduling on main class

2. Annotate methods with @Scheduled:

```bash
@Component
public class ScheduledTasks {
    
    private static final Logger log = LoggerFactory.getLogger(ScheduledTasks.class);
    
    @Scheduled(fixedRate = 5000)
    public void reportCurrentTime() {
        log.info("The time is now {}", LocalDateTime.now());
    }
    
    @Scheduled(cron = "0 0 9 * * ?")
    public void morningTask() {
        log.info("Good morning! Time for the daily report");
    }
}
```
3. Configuration options:

- **fixedRate:** Execute with fixed period between invocations

- **fixedDelay:** Execute with fixed delay between completion and next invocation

- **cron:** Cron expression for more complex scheduling

4. Configure thread pool (if needed) by implementing SchedulingConfigurer

### 5. How do you monitor a Spring Boot application in production?
Answer:
Monitoring options for Spring Boot applications:

1. **Spring Boot Actuator:** Provides built-in endpoints for health, metrics, etc.

2. **Spring Boot Admin:** UI for monitoring and managing Spring Boot applications

3. **Micrometer:** Application metrics facade (integrates with Prometheus, Graphite, etc.)

4. **Prometheus + Grafana:** Popular monitoring stack

5. **ELK Stack:** For centralized logging (Elasticsearch, Logstash, Kibana)

6. **Distributed Tracing:** Zipkin or Jaeger with Spring Cloud Sleuth

Configuration example for Prometheus:

properties
```bash
management.endpoints.web.exposure.include=health,metrics,prometheus
management.metrics.export.prometheus.enabled=true
```
Example Grafana dashboard can show:

- JVM metrics (memory, threads, GC)

- HTTP request rates and latencies

- Database connection pool metrics

- Cache statistics

- Custom business metrics

## Database and JPA
### 1. How does Spring Boot simplify working with databases?
Answer:
Spring Boot simplifies database work through:

1. **Auto-configuration:** Automatically configures DataSource based on dependencies

2. **Embedded Databases:** Supports H2, HSQLDB, Derby with zero configuration

3. **Spring Data JPA:** Reduces boilerplate code with repositories

4. **Automatic Repository Implementation:** Creates implementations for repository interfaces

5. **Property-based Configuration:** Easy configuration via application.properties:

properties
```bash
spring.datasource.url=jdbc:mysql://localhost/test
spring.datasource.username=dbuser
spring.datasource.password=dbpass
spring.jpa.hibernate.ddl-auto=update
```
6. **Connection Pooling:** Auto-configures HikariCP (default), Tomcat, or Commons DBCP

### 2. Explain the difference between Hibernate and Spring Data JPA.
Answer:

| Aspect              | Hibernate                                         | Spring Data JPA                                                  |
|---------------------|--------------------------------------------------|------------------------------------------------------------------|
| **Purpose**         | ORM implementation                               | Abstraction layer over JPA implementations                       |
| **Main Interface**  | `SessionFactory`                                 | `JpaRepository`                                                  |
| **Query Creation**  | HQL, Criteria API, Native SQL                    | Method names, `@Query`, QueryDSL                                 |
| **Boilerplate Code**| More boilerplate                                 | Less boilerplate                                                 |
| **Transaction Mgmt**| Manual or JTA                                    | Simplified via `@Transactional`                                  |
| **Relationship**    | Direct implementation                            | Works with Hibernate, EclipseLink, etc.                          |



