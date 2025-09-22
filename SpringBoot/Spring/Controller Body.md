# 🚀 Spring Boot Annotations Cheat Sheet

## 1. `@RestController`
- Combines **`@Controller` + `@ResponseBody`**.
- Used to create **REST APIs**.
- Methods return data directly (usually JSON or String), not a view.

```java
@RestController
public class HelloController {
    @GetMapping("/hello")
    public String sayHello() {
        return "Hello World!";
    }
}
```

## 2. `@RequestMapping`

- General-purpose mapping annotation.
- Can be used for **GET, POST, PUT, DELETE**, etc.
- Often replaced by `@GetMapping`, `@PostMapping`, etc. for clarity.
    
```java
@RestController
@RequestMapping("/api") // Base path 
public class UserController {  
    
@RequestMapping("/users") // Defaults to GET if not specified     
public String getUsers() {   
      
return "All Users";     
	}
}
```

---

## 3. `@GetMapping`

- Shortcut for `@RequestMapping(method = RequestMethod.GET)`.
- Used for **HTTP GET requests** (read data).
    

```java
@GetMapping("/user/{id}") 
public String getUser(@PathVariable int id) {     
	return "User ID: " + id; 
}
```

---

## 4. `@RequestBody`

- Binds the **HTTP request body (JSON/XML)** to a Java object.
- Used in **POST/PUT** methods when sending data.
    

```java
@PostMapping("/user") 
public String addUser(@RequestBody User user) {     
	return "Added user: " + user.getName(); 
}
```

# 🚀 Spring Boot `@PostMapping` (POST Controller)

## 1. What is `@PostMapping`?
- A **specialized shortcut** for `@RequestMapping(method = RequestMethod.POST)`.
- Used to handle **HTTP POST requests** (create/add data).
- Often combined with `@RequestBody` to accept JSON/XML input.

---

## 2. Example: Adding a User

```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api")
public class UserController {

    // Handle POST request to /api/user
    @PostMapping("/user")
    public String addUser(@RequestBody User user) {
        return "✅ User added: " + user.getName() + " (ID: " + user.getId() + ")";
    }
}
```