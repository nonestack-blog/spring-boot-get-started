![display](https://repository-images.githubusercontent.com/704718611/8fc94bf1-c498-4517-b014-3193e987b92d)

Spring Boot is a popular framework that simplifies and accelerate the process of developing a java based application  

## <a name="what-you-will-build" aria-label="what-you-will-build" id="what-you-will-build" href="#what-you-will-build"></a>What You Will build
You will build a Spring Boot web application.

## <a name="what-you-need" aria-label="what-you-need" id="what-you-need" href="#what-you-need"></a>What You Need
- A favorite text editor or IDE
- JDK 1.8 or later
- Gradle 4+ or Maven 3.2+

## <a name="setup-project-with-spring-initializr" aria-label="setup-project-with-spring-initializr" id="setup-project-with-spring-initializr" href="#setup-project-with-spring-initializr"></a>Setup Project With Spring Initializr

- Navigate to [Spring initializr](https://start.spring.io).
- Define the project name example: `spring-boot-get-started`
- Choose Project **Maven** and the language  **Java**.
- Choose Your **Java** version ex: **17**
- Click add dependencies and select:
    - Spring Web

- Click Generate.

Unzip the Downloaded Zip and open the Project using your favorite text editor or IDE

## <a name="application-class" aria-label="application-class" id="application-class" href="#application-class"></a>Application class

The main class for our application, serve as an entry point for our Spring boot application

```java
@SpringBootApplication
public class SpringBootGetStartedApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringBootGetStartedApplication.class, args);
    }

}
```

The class is annotated with ```@SpringBootApplication``` which is a combination of several annotation : 
  - ```@EnableAutoConfiguration``` Attempting to **auto-configure** beans, usually applied to classes based on your classpath and what beans you have defined
  - ```@ComponentScan``` Sets up component scanning directives for any  ***@Configuration*** ***@Component*** ***@Service***.

```SpringApplication.run()``` method to launch the spring boot application. once you lunch the app it will be running on port **8080**, you can set it under the ```application.properties```  ```server.port=8081```, This web application relies on **annotation-based** configuration, which means it's entirely **Java-based**, eliminating the need to manually configure the web application infrastructure. This approach allows you to **focus** more on the business logic

## <a name="web-application" aria-label="web-application" id="web-application" href="#web-application"></a>Web Application
under the src package create the class ```GreetingController``` 

```java
@RestController
public class GreetingController {

	@GetMapping("/")
	public String index() {
		return "Greetings from Nonestack!";
	}

}
```

- The class is annotated with a ```@RestController```, meaning it is ready to be used by Spring MVC to handle web requests. 
- Spring Boot use a singleton servlet than it will delegate the request to the corresponded ```@Controller``` or ```@RestController```
- ```@GetMapping``` maps the path ```/``` to the index() method. When call the endpoint ```http://localhost:8080/```, the method returns text. That is because ```@RestController``` combines ```@Controller``` and ```@ResponseBody```, two annotations that results in web requests returning data rather than a view.

## <a name="run-the-application" aria-label="run-the-application" id="run-the-application" href="#run-the-application"></a>Run the Application
To run the application, run the following command based on your project management 
- Maven ```./mvnw spring-boot:run```
- Gradle ```./gradlew bootRun```

## <a name="test" aria-label="test" id="test" href="#test"></a>Test

Add the flowing test dependency to you ```pom.xml``` file
```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-test</artifactId>
  <scope>test</scope>
</dependency>
```

If you use Gradle, add the following dependency to your ```build.gradle``` file
```gradle
testImplementation('org.springframework.boot:spring-boot-starter-test')
```

Write the unit test  ```GreetingControllerTest.java``` under the ```src/test/java/com/nonestack/springbootgetstarted``` folder 

```java
@SpringBootTest
@AutoConfigureMockMvc
public class GreetingControllerTest {

  @Autowired
  private MockMvc mvc;

  @Test
  public void getHello() throws Exception {
    mvc.perform(MockMvcRequestBuilders.get("/").accept(MediaType.APPLICATION_JSON))
            .andExpect(status().isOk())
            .andExpect(content().string(equalTo("Greetings from Nonestack!")));
  }
}
```

**MockMvc**, from Spring Test, allows you to send HTTP requests and check the results using builder classes. Use ```@AutoConfigureMockMvc``` and ```@SpringBootTest``` to inject a MockMvc instance. ```@SpringBootTest``` creates the full application context, while ```@WebMvcTest``` focuses on the web layers. Spring Boot automatically identifies the main application class, but you can override or narrow it down if needed.

## <a name="summary" aria-label="summary" id="summary" href="#summary"></a>Summary

Congratulations 🎉 ! You've created quick Spring Boot Web Application to get started.

## <a name="github" aria-label="github" id="github" href="#github"></a>Github
The tutorial can be found here on [GitHub](https://github.com/nonestack-blog/spring-boot-get-started) 👋

## <a name="blog" aria-label="blog" id="blog" href="#blog"></a>Blog

Check new tutorials on [nonestack](https://www.nonestack.com) 👋
