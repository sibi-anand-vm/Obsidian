ot# 🧩 Exception Handling in Spring Boot

## 1. Traditional Way (try–catch in Controller)

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @Autowired
    private UserService userService;

    @GetMapping("/{id}")
    public ResponseEntity<?> getUser(@PathVariable Long id) {
        try {
            User user = userService.getUserById(id);
            return ResponseEntity.ok(user);
        } catch (UserNotFoundException e) {
            return ResponseEntity.status(HttpStatus.NOT_FOUND)
                                 .body("User not found: " + e.getMessage());
        } catch (Exception e) {
            return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
                                 .body("Something went wrong: " + e.getMessage());
        }
    }
}
```
### ⚠️ Problems

- Repeated `try–catch` blocks
    
- Hard to maintain and test
    
- No global handling

### 2. Using `@ExceptionHandler` in Controller
```java
@RestController
@RequestMapping("/users")
public class UserController {

    @Autowired
    private UserService userService;

    @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) {
        return userService.getUserById(id);
    }

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handleUserNotFound(UserNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND)
                             .body("User not found: " + ex.getMessage());
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleGeneralException(Exception ex) {
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
                             .body("Error: " + ex.getMessage());
    }
}

```

### ✅ Pros

- Cleaner than traditional try–catch
    
- Handles exceptions per controller

### 🚫 Cons

- Limited to one controller only

#### 3. Global Handling with `@ControllerAdvice`
```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handleUserNotFound(UserNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND)
                             .body("User not found: " + ex.getMessage());
    }

    @ExceptionHandler(InvalidInputException.class)
    public ResponseEntity<String> handleInvalidInput(InvalidInputException ex) {
        return ResponseEntity.status(HttpStatus.BAD_REQUEST)
                             .body("Invalid input: " + ex.getMessage());
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleOtherExceptions(Exception ex) {
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
                             .body("Something went wrong: " + ex.getMessage());
    }
}

```

### ✅ Pros

- Centralized exception handling
    
- Cleaner & reusable
    
- Consistent error structure across controllers
    
---

## 4. Custom Error Response DTO
```java
public class ErrorResponse {
    private String message;
    private String path;
    private int status;
    private LocalDateTime timestamp;

    // Constructor, Getters, Setters
}

@ExceptionHandler(UserNotFoundException.class)
public ResponseEntity<ErrorResponse> handleUserNotFound(UserNotFoundException ex, WebRequest request) {
    ErrorResponse error = new ErrorResponse(
        ex.getMessage(),
        request.getDescription(false),
        HttpStatus.NOT_FOUND.value(),
        LocalDateTime.now()
    );
    return new ResponseEntity<>(error, HttpStatus.NOT_FOUND);
}

```

| Approach                    | Scope          | Pros                      | Cons                  |
| --------------------------- | -------------- | ------------------------- | --------------------- |
| **Traditional (try–catch)** | Per method     | Simple                    | Repetitive, messy     |
| **@ExceptionHandler**       | Per controller | Cleaner                   | Not global            |
| **@ControllerAdvice**       | Global         | Centralized, maintainable | Slight setup overhead |

💡 **Tip:** Use `@RestControllerAdvice` if you return JSON responses (REST APIs).  
Use `@ControllerAdvice` if you return views (HTML pages).