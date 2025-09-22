### 1. Using **`@PathVariable`**

```java
@GetMapping("/user/{id}") 
public String getUser(@PathVariable int id) { 
    return "User ID: " + id; 
}
```

- URL → `/user/101`
    
- Output → `User ID: 101`
    
---

### 2. Using **`@RequestParam`**

```java
@GetMapping("/user") 
public String getUser(@RequestParam int id) {     
	return "User ID: " + id; 
}
```

- URL → `/user?id=101`
    
- Output → `User ID: 101`
    

---

## 🔑 Why Annotations Are Needed

- Without `@PathVariable` or `@RequestParam`, Spring **doesn’t know** whether `id` comes from:
    
    - URL path → `/user/101`
        
    - Query string → `/user?id=101`
        
    - Form data, request body, etc.
        

So the plain `int id` in method signature won’t work unless annotated.