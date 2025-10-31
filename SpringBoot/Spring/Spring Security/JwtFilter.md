# Spring Security JWT Implementation Notes

## 1️⃣ JwtFilter Creation

- Extend `OncePerRequestFilter` to create a custom filter that runs **once per request**.
- Responsibilities of `JwtFilter`:
  1. Extract the JWT token from the `Authorization` header.
```java
     String authHeader = request.getHeader("Authorization");
     if (authHeader != null && authHeader.startsWith("Bearer ")) {
         token = authHeader.substring(7);
     }
```
  2. Extract the username from the token using `JWTService`.
     ```java
     username = jwtService.extractUsername(token);
     ```
  3. Check if user is **not already authenticated** in `SecurityContextHolder`.
     ```java
     if (username != null && SecurityContextHolder.getContext().getAuthentication() == null) {
         ...
     }
     ```
  4. Load user details from `UserDetailsService`.
     ```java
     UserDetails userDetails = userDetailsService.loadUserByUsername(username);
     ```
  5. Validate the token using `JWTService`.
  6. Create a `UsernamePasswordAuthenticationToken` with user details and authorities.
     ```java
     UsernamePasswordAuthenticationToken authToken =
         new UsernamePasswordAuthenticationToken(userDetails, null, userDetails.getAuthorities());
     ```
  7. Set request details to the token for traceability.
     ```java
     authToken.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));
     ```
  8. Store authentication in `SecurityContextHolder`.
     ```java
     SecurityContextHolder.getContext().setAuthentication(authToken);
     ```
  9. Pass the request along the filter chain:
     ```java
     filterChain.doFilter(request, response);
     ```


Single File:
```java
package com.testing.SpringSecurity.config;  
  
import com.testing.SpringSecurity.service.JWTService;  
import jakarta.servlet.FilterChain;  
import jakarta.servlet.ServletException;  
import jakarta.servlet.http.HttpServletRequest;  
import jakarta.servlet.http.HttpServletResponse;  
import org.hibernate.annotations.Comment;  
import org.hibernate.annotations.CompositeTypeRegistration;  
import org.springframework.beans.factory.annotation.Autowired;  
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;  
import org.springframework.security.core.context.SecurityContextHolder;  
import org.springframework.security.core.userdetails.UserDetails;  
import org.springframework.security.core.userdetails.UserDetailsService;  
import org.springframework.stereotype.Component;  
import org.springframework.web.filter.OncePerRequestFilter;  
  
import java.io.IOException;  
  
  
@Component  
public class JwtFilter extends OncePerRequestFilter {  
  
    @Autowired  
    JWTService jwtService;  
  
    @Autowired  
    UserDetailsService userDetailsService;  
  
    @Override  
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {  
  
        String authHeader=request.getHeader("Authorization");  
  
        String token=null;  
        String username=null;  
  
        if(authHeader!=null && authHeader.startsWith("Bearer ")){  
            token=authHeader.substring(7);  
            username=jwtService.extractUsername(token);  
        }  
  
        if(username!=null && SecurityContextHolder.getContext().getAuthentication()==null){  
  
            UserDetails userDetails=userDetailsService.loadUserByUsername(username);  
            if(jwtService.validateToken(token)){  
                UsernamePasswordAuthenticationToken authToken=new UsernamePasswordAuthenticationToken(username,null,userDetails.getAuthorities());  
                SecurityContextHolder.getContext().setAuthentication(authToken);  
            }  
  
        }  
  
        filterChain.doFilter(request,response);  
    }  
}

```

---

## 2️⃣ Registering JwtFilter in SecurityConfig

- Use `addFilterBefore()` to place `JwtFilter` **before** Spring Security’s `UsernamePasswordAuthenticationFilter`.
- This ensures JWT is checked **before default authentication mechanisms**.
  
Example:
```java
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    return http
        .csrf(AbstractHttpConfigurer::disable)
        .authorizeHttpRequests(req -> req
            .requestMatchers("/register", "/login").permitAll()
            .anyRequest().authenticated())
        .sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
        .addFilterBefore(jwtFilter, UsernamePasswordAuthenticationFilter.class)
        .build();
}
```

## 3️⃣ Why `addFilterBefore`?

- Spring Security has a **chain of filters**.
    
- `UsernamePasswordAuthenticationFilter` handles standard form login.
    
- `JwtFilter` must run **before** it so that if a valid JWT exists:
    
    - The user is already authenticated in `SecurityContextHolder`.
        
    - The username/password login filter is skipped.
        
- This allows stateless JWT authentication for all API requests.
    

---

## 4️⃣ Key Points

- `SecurityContextHolder` stores the **authenticated user details** for the current request.
    
- `UsernamePasswordAuthenticationToken` contains:
    
    - `principal` → the `UserDetails` object
        
    - `credentials` → usually `null` after authentication
        
    - `authorities` → roles/permissions of the user
        
- `setDetails()` attaches request metadata (IP, session ID) to the authentication object.
    
- After `JwtFilter`, controllers can use `@AuthenticationPrincipal` or `SecurityContextHolder.getContext().getAuthentication()` to access the user.