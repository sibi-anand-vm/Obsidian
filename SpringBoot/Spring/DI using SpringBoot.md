# Spring Boot Example Notes

---
## 🌱 Key Concepts in the Example

1. **ApplicationContext**
   - Central interface of Spring IoC container.
   - Responsible for managing beans (objects).
   - We can get beans using:
```java
ApplicationContext context = SpringApplication.run(DemoAppApplication.class, args);
     Devloper dev = context.getBean(Devloper.class);
```

2. **@Component**
   - Marks a class as a **Spring Bean**.
   - Spring will automatically detect and create an object for it.
   - Example:
     ```java
     @Component
     public class Devloper {
         public void build(){
             System.out.println("Hi guys. I am developer");
         }
     }
     ```

2. **@SpringBootApplication**
   - Entry point of a Spring Boot application.
   - Includes:
     - `@Configuration` → allows Java-based configuration.
     - `@EnableAutoConfiguration` → enables auto configuration.
     - `@ComponentScan` → scans for `@Component`, `@Service`, `@Repository`, `@Controller`.

2. **@RestController**
   - Combines `@Controller` + `@ResponseBody`.
   - Used to expose REST APIs.

2. **@RequestMapping**
   - Maps an HTTP request to a method.
   - Example:
     ```java
     @RequestMapping("/")
     public String sayHello() {
         return "Hi 2 everyone";
     }
     ```

---

## 🚀 Code Recap

### `DemoAppApplication.java`
```java
@SpringBootApplication
public class DemoAppApplication {
    public static void main(String[] args) {
        ApplicationContext context = SpringApplication.run(DemoAppApplication.class, args);
        Devloper dev = context.getBean(Devloper.class);
        dev.build();
    }
}
```
