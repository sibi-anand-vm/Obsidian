# Spring Security — BCrypt Implementation Notes

## 1️⃣ Overview

- Use **BCryptPasswordEncoder** to securely store user passwords.
    
- Avoid storing plain text passwords in the database.
    
- Spring Security automatically matches raw passwords from clients with the BCrypt-hashed password in DB.
    

---

## 2️⃣ Security Configuration (`SecurityConfig`)

```java
@Autowired
UserDetailsService userDetailsService;

@Bean
public AuthenticationProvider authenticationProvider(){
    DaoAuthenticationProvider provider = new DaoAuthenticationProvider();
    provider.setPasswordEncoder(new BCryptPasswordEncoder(12)); // Strength 12
    provider.setUserDetailsService(userDetailsService);
    return provider;
}
```

- `DaoAuthenticationProvider` uses `UserDetailsService` to fetch users from DB.
    
- `BCryptPasswordEncoder` ensures passwords are hashed with BCrypt.
    
- Client sends **raw password** in Basic Auth; Spring Security hashes and compares it with DB.
    

### Security Filter Chain

```java
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    http.csrf(AbstractHttpConfigurer::disable);
    http.authorizeHttpRequests(request -> request.anyRequest().authenticated());
    http.formLogin(Customizer.withDefaults());
    http.httpBasic(Customizer.withDefaults());
    http.sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS));
    return http.build();
}
```

- CSRF disabled for stateless APIs.
    
- All requests require authentication.
    
- Stateless session management.
    
- Supports both form login and HTTP Basic.
    

---

## 3️⃣ User Registration (`UserController` + `UserService`)

### Controller

```java
@PostMapping("/register")
public Users registerUser(@RequestBody Users user){
    return userService.registerUser(user);
}
```

- Endpoint to register a new user.
    

### Service

```java
public Users registerUser(Users user){
    BCryptPasswordEncoder encoder = new BCryptPasswordEncoder(12);
    user.setPassword(encoder.encode(user.getPassword()));
    return userDao.save(user);
}
```

- Password is **hashed using BCrypt** before saving.
    
- Strength 12 is used for hashing complexity.
    
- Saves user to database securely.
    

---

## 4️⃣ Key Points

1. All passwords in DB must be BCrypt-hashed.
    
2. Raw password is sent by client in **Basic Auth** or form login.
    
3. Spring Security automatically matches raw password with stored hash.
    
4. Using `NoOpPasswordEncoder` for production is unsafe.
    
5. Always prefer `BCryptPasswordEncoder` or other secure encoders.
    

---

## 5️⃣ Example Flow

1. Client registers user with raw password `pass1234` in `/register` endpoint .
    
2. `UserService` encodes password using BCrypt and saves to DB.
    
3. Client logs in via Basic Auth with username and raw password.
    
4. Spring Security hashes the raw password and compares with DB hash.
    
5. Authentication succeeds 