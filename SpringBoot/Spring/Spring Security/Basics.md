# 🔗 Flow of a Client Request in a Spring MVC App

## 1️⃣ Client (Browser / Postman / Frontend App)
→ Sends an **HTTP request** to the server (like `/login`, `/api/users`, etc.)

---

## 2️⃣ Filters (Servlet Filters)

- These are part of the **Servlet container** (not Spring-specific).  
- Each filter can:
  - Inspect or modify the request (`HttpServletRequest`)
  - Add headers, log info, check authentication, etc.
  - Block or forward the request

**Examples:**
- `OncePerRequestFilter`
- `CharacterEncodingFilter`
- `JwtAuthFilter`

---

## 3️⃣ DispatcherServlet (Front Controller)

- Acts as the **central Spring MVC controller**.
- Receives the processed request (after filters) and:
  - Finds the **appropriate controller** using handler mappings.
  - Delegates the request to that controller method.

---

## 4️⃣ Controller Layer

Your `@Controller` or `@RestController` methods handle the request logic.

```java
@GetMapping("/users")
public ResponseEntity<List<User>> getUsers(HttpServletRequest request) {
    String ip = request.getRemoteAddr(); // Access client info
    return ResponseEntity.ok(service.getUsers());
}
```

## 5️⃣ Response Phase

- The response goes **back through the same filters** in reverse order.
    
- Filters can again modify the `HttpServletResponse` (e.g., add headers, compress data, etc.)
    
- Finally, the **client receives the response**.
    
---
## 🧠 Using `HttpServletRequest`

You can use it in your controller or filter to extract request metadata:
```java
String uri = request.getRequestURI();
String method = request.getMethod();
String ip = request.getRemoteAddr();
String header = request.getHeader("User-Agent");
```

# Spring Security: Custom Username & Password

## 1️⃣ Set Credentials in `application.properties`
```properties
# Set your own Spring Security default credentials
spring.security.user.name=jack
spring.security.user.password=pass1234
```

## 2️⃣ Explanation

- When you add **Spring Security** dependency, by default:

    - It auto-generates a **random password**        
    - Default username is `user`    
- By defining the above properties, you **override the default username and password**.