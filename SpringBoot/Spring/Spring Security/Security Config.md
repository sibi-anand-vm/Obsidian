# 🧩 Spring SecurityConfig — Notes

## 1️⃣ Overview

This configuration defines how Spring Security protects your web application. It sets up authentication, session management, and disables CSRF for a stateless REST API setup.

```java
package com.testing.SpringSecurity.config;

import org.springframework.context.annotation.Bean;
import org.springframework.security.config.Customizer;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.security.web.SecurityFilterChain;


@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {

        http.csrf(customizer -> customizer.disable());
        http.authorizeHttpRequests(request -> request.anyRequest().authenticated());
        http.formLogin(Customizer.withDefaults());
        http.httpBasic(Customizer.withDefaults());
        http.sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS));
        return http.build();
    }
}
```

---
### 🧩 Class Overview
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

```

- `@Configuration` → Marks this as a Spring configuration class.
    
- `@EnableWebSecurity` → Enables Spring Security’s web features and integrates it into your application.
    
- Together, these tell Spring to load this class as your main security configuration.

## 2️⃣ Bean Explanation

### `@Bean`

- Declares a Spring bean that defines your **security filter chain**.
    
- Spring calls this method at startup to configure web security.
    

### `HttpSecurity`

- The main configuration object for Spring Security.
    
- Allows customizing authentication, authorization, CSRF, sessions, etc.
    

---

## 3️⃣ Step-by-Step Breakdown

### 🔹 `http.csrf(customizer -> customizer.disable());`

- **Disables CSRF protection.**
    
- Default: CSRF is **enabled** in Spring Security.
    
- CSRF tokens are needed when using browser-based sessions.
    
- Safe to disable when building **stateless REST APIs** or using **JWT authentication**.
    

> ⚠️ If using form login sessions, do **not** disable CSRF.

---

### 🔹 `http.authorizeHttpRequests(request -> request.anyRequest().authenticated());`

- Every incoming request must be **authenticated**.
    
- No endpoint is public by default.
    
- You can later modify it to allow some endpoints:
    
    ```java
    request.requestMatchers("/public/**").permitAll()
           .anyRequest().authenticated();
    ```
    

---

### 🔹 `http.formLogin(Customizer.withDefaults());`

- Enables **form-based login**.
    
- Provides a **default Spring login page**.
    
- Typically used for web applications accessed via a browser.
    

---

### 🔹 `http.httpBasic(Customizer.withDefaults());`

- Enables **HTTP Basic authentication**.
    
- Ideal for REST clients like **Postman** or **curl**.
    
- Example:
    
    ```bash
    curl -u jack:pass1234 http://localhost:8080/getStudents
    ```
    

---

### 🔹 `http.sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS));`

- Configures **session creation policy**.
    
- `STATELESS` → No session is created or used.
    
- Each request must be independently authenticated.
    
- Common in **REST APIs** and **JWT-based security**.
    

**Other options:**

- `ALWAYS` → Always create a session.
    
- `NEVER` → Never create, but use existing if available.
    
- `IF_REQUIRED` → Create session only when needed (default).
    

---

### 🔹 `return http.build();`

- Builds and returns the **SecurityFilterChain** with all configured security rules.
    

---

## 4️⃣ TL;DR Summary

|Configuration|Purpose|
|---|---|
|`csrf().disable()`|Disable CSRF (safe for APIs)|
|`authorizeHttpRequests().anyRequest().authenticated()`|All requests need authentication|
|`formLogin()`|Enable login form for browsers|
|`httpBasic()`|Enable Basic Auth for REST clients|
|`sessionCreationPolicy(STATELESS)`|Disable session — stateless mode|

---

## 5️⃣ Example Scenario

- You are building a REST API (no frontend session handling).
    
- Each client (browser/Postman/frontend) sends credentials with every request.
    
- The server authenticates every request separately.
    
- No CSRF tokens or HTTP sessions are used.
    

✅ Perfect for **microservices**, **JWT-based APIs**, or **Postman testing** environments.