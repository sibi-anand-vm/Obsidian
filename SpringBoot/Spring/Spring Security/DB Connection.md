# Spring Security — Database-backed Authentication Notes

## 1️⃣ Steps Involved

1. **Added dependency**
    
    - Spring Security, Spring Data JPA, database driver (e.g., H2, MySQL, PostgreSQL).
        
2. **Add DB config in** `**application.properties**`
    
    - URL, username, password, driver class, and JPA properties.
        
3. **Modified default AuthenticationProvider**
    
    - Configured `DaoAuthenticationProvider` to use custom `UserDetailsService`.
        
    - Set password encoder (`NoOpPasswordEncoder` for testing).
        
4. **Created** `**UserPrincple**` **entity**
    
    - Implements `UserDetails` interface.
        
    - Wraps `Users` entity for Spring Security.
        
5. **Created** `**MyUserDetailService**`
    
    - Implements `UserDetailsService`.
        
    - Loads user from DB using `UserDao`.
        
6. **Created method** `**findUserByUsername**` **in** `**UserDao**`
    
    - Custom JPA query to fetch user by username for authentication.

## 1️⃣ Security Configuration (`SecurityConfig`)

### Overview

- Uses **custom `UserDetailsService`** to authenticate users from the database.
    
- Stateless session, CSRF disabled.
    
- Supports both **form login** and **HTTP Basic authentication**.
    

### Authentication Provider

```java
@Bean
public AuthenticationProvider authenticationProvider(){
    DaoAuthenticationProvider provider = new DaoAuthenticationProvider();
    provider.setPasswordEncoder(NoOpPasswordEncoder.getInstance());
    provider.setUserDetailsService(userDetailsService);
    return provider;
}
```

- **DaoAuthenticationProvider** uses `UserDetailsService` to fetch users.
    
- `NoOpPasswordEncoder` → passwords are stored in plain text (only for testing).
    
- Provides DB-backed authentication.
    

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

- Disables CSRF (safe for stateless APIs).
    
- All requests require authentication.
    
- Stateless session: every request must include credentials.
    

### Optional In-Memory Users (commented)

- Quick testing without database.
    
- Not used in DB-backed setup.
    

---

## 2️⃣ Custom `UserDetailsService` (`MyUserDetailService`)

```java
@Service
public class MyUserDetailService implements UserDetailsService {
    @Autowired UserDao userDao;

    @Override
    public UserDetails loadUserByUsername(String username) {
        Users user = userDao.findUserByUsername(username);
        if (user == null) throw new UsernameNotFoundException("User not found");
        return User.builder()
                   .username(user.getUsername())
                   .password(user.getPassword())
                   .roles("USER")
                   .build();
    }
}
```

- Loads users from the database using `UserDao`.
    
- Returns Spring Security `User` object for authentication.
    

---

## 3️⃣ User Entity (`Users`)

```java
@Entity
public class Users {
    @Id private int id;
    private String username;
    private String password;
}
```

- JPA entity representing a database table.
    
- Stores user credentials.
    
- Accessed via `UserDao`.
    

---

## 4️⃣ User Principal (`UserPrincple`)

```java
public class UserPrincple implements UserDetails {
    private Users user;
    // override UserDetails methods, e.g., getUsername, getPassword
}
```

- Wraps `Users` entity for Spring Security.
    
- Implements `UserDetails` interface.
    
- Can be extended to include roles/authorities.
    

---

## 5️⃣ User DAO (`UserDao`)

```java
@Repository
public interface UserDao extends JpaRepository<Users, Integer> {
    Users findUserByUsername(String username);
}
```

- Spring Data JPA repository.
    
- Provides CRUD operations and custom query to fetch user by username.
    

---

## 6️⃣ Authentication Flow

1. Client sends **login request** (form or basic auth).
    
2. `DaoAuthenticationProvider` calls `MyUserDetailService.loadUserByUsername()`.
    
3. Service fetches user from DB using `UserDao`.
    
4. If user exists, password is checked.
    
5. If valid → authentication succeeds → user can access secured endpoints.
    

---

## ✅ Key Points

- Stateless API → session not stored.
    
- CSRF disabled because session not used.
    
- Database-backed authentication allows dynamic user management.
    
- In-memory users can be used for testing only.