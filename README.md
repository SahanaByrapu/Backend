
### Spring Boot

|  S.No | Topics |
|------- | ------ |
|  1. | **Introduction to Spring Boot:** |
|  | what problem it solved
|  | Its features and advantages
| | |
| 2. | **Setting up initial Spring boot Project** |
| |Understand Layered Architecture |
| |
|3. |**Understand Maven pom.xml a bit (as Maven and Java is a pre-requisite for learning springboot)**|
| |
|4.|**Spring Boot Basic Topics**|
| |**Annotations:**|
| |@SpringBootApplication|
| |@ Controller|
| |@RestController|
| |@RequestMapping|
| |@GetMapping, @PostMappin|g, @PutMapping, @DeleteMapping
| |@Autowired|
| |@Component|
| |@Service|
| |@Repository|
| |@ComponentScan|
| |@ Configuration|
| |@Value|
| |@Qualifier|
| |@Profile|
| |@EnableAutoConfiguration|
| |@Entity|
| |@Transactional|
| |@EnableCaching|
| |@Async|
| |@EnableScheduling etc…|
| |
|5. |**Dependency Injection and Beans**|
| |
|6. |**Spring Boot Data Access**|
| |Spring JPA|
| |Spring JDBC|
| |QueryMethod|
| |
|7. |**RESTful APIs with SpringBoot**|
| |
|8.|**SpringBoot Security**|
| |Securing our REST APIs|
| |
|9. |**Spring Boot Logging**|
| |**Spring Boot Exception Handling**|
| |**Spring Boot Caching**|
| |
|11.|**Spring Boot Interceptor**|
| |
|12. |**Spring Boot Scheduling**|
| |
|13. |**SpringBoot Testing**|
| |Mockito|


### Microservices topics in SpringBoot

|  S.No | Topics |
|--------|---------|
|1.|**Introduction to Microservices**|
| |
|2. |**Service Discovery using Eureka**|
| |Microservice Registering|
| |
|3.|**Tracing the request in multiple Microservices**|
| |Sleuth and Zipkin|
| |Sleuth links the trace id with your request|
| |Zipkin help to visualize using the trace id|
| |
|4. |**Spring Boot Profiles**|
| |different properties based on profiles (like QA, Production)|
| |
|5. |**Spring Cloud Config Servers:**|
| |its Configuration managmenet|
| |
|6. |**Communition between different microservies**||
| |SYNC|
| |ASYNC (messaging queue)|
| |
|7.|**API Gateway**|
| |
|8.|**Circuit Breaker**|
| |
|9. |**CQRS (Command Query Responsibility Segregation)**|
| |
|10.|**Deployment and Containerization**|
| |creating executable JARs and WARs|
| |


### UNIT TESTING
| Unit Testing-JUnit | |
| ----------------- | ---- |
|**1. Available Frameworks:**|What is a unit test?|
|Junit|Difference between unit vs integration vs functional tests|
|TestNG etc.| AAA (Arrange-Act-Assert)|
| |Maven/Gradle dependencies|
| |Test Lifecycle|
|**2.Basic Annotations:**|
|| • @Test|
||| • @BeforeEach, @AfterEach|
|| • @BeforeAll, @AfterAll|
|| • @DisplayName|
|| • @Disable|
||etc.|
|**3.Assertions:**|
| • assertEquals, assertNotEquals|
| • assertTrue, assertFalse|
| • assertNull, assertNotNull|
| • assertThrows for exception testing|
|Parameterized Tests|
|Test Repetition|
| • @RepeatedTest(n)|
| |
|**4.Mocking**|
|**Available Frameworks:**|**Mockito Core Concepts:**|
|Mockito| • @Mock and Mockito.mock(Class.class)|
|EasyMock|  • @InjectMocks for injecting mocks|
|JMock| • @BeforeEach with MockitoAnnotations.openMocks(this)|
| | • Testing Private/Static Methods (PowerMock or some other approach)|
| |**Stubbing Behavior**|
| | • when(...).thenReturn(...)|
| | • when(...).thenThrow(...)|
| |**Verifying Calls**|
| | • verify(...) after method call|
| | • verifyNoMoreInteractions(...)|
| |**Void Method Stubbing**|
| | • doNothing().when(mock).method()|
| | • doThrow(...).when(...)|
| |**Argument Matchers:**|
| | • any(), eq(), anyString(), anyInt(), etc.|
| | • Mixing matchers with exact values (and why it fails)|
| |**Behavior Verification:**|
| |Verify how many times called: times(n), never(), atLeastOnce()|
| |**Spies vs Mocks:**|
| | ○ Mockito.spy() for partial mocking|
| | ○ Difference between mock() and spy()|
| ||
|**5.Testing Configuration, Properties, and Profiles** |**Unit tests with different Spring profiles.**|
| |**How to mock @Value, Environment, or @ConfigurationProperties.**|
| |**Overriding properties for test-only behavior.**|
| | |
|**6.Assertions & Matchers**|  |
|**Frameworks:**| |
| AssertJ | |
| Hamcrest| |
| | |
|**7.Some Advanced Topics**. |  |
| |**Test-Driven Development (TDD)**|
| |Write failing test first, then code|
| |**Test Coverage:**|
| |**• Tools:** JaCoCo, IntelliJ coverage tool|
| |**CI integration**|
| |Run tests in GitHub Actions, GitLab CI/CD, Jenkins.|
| |**Test Reports**|
| |Generate HTML/XML test reports for build tools.|
| |
|**8.AI + Unit Testing** | |
| |Code Suggestion Tools (AI-Powered IDE Extensions)||
| |Using AI in CI/CD (Future-Forward)|
| |AI suggests missing test cases for changed methods|
| |AI flags flaky or redundant tests|
| |Autogenerate Missing Tests|
