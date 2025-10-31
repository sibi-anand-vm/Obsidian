
This document contains the full setup for a Spring Boot Product Service with JPA, Eureka Client, Spring Web, and MySQL.

---
## 1. pom.xml Dependencies

```xml
<dependencies>
    <!-- Spring Web -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!-- Spring Data JPA -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>

    <!-- MySQL Driver -->
    <dependency>
        <groupId>com.mysql</groupId>
        <artifactId>mysql-connector-j</artifactId>
        <scope>runtime</scope>
    </dependency>

    <!-- Eureka Client -->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>

    <!-- Lombok (optional) -->
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
</dependencies>
```

---

## 2. application.properties

```properties
# Application name
spring.application.name=productServices

# MySQL config
spring.datasource.url=jdbc:mysql://localhost:3306/productDB
spring.datasource.username=root
spring.datasource.password=ACCESS@GRANt42
spring.jpa.hibernate.ddl-auto=validate
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect

# Eureka config
eureka.client.service-url.defaultZone=http://localhost:8761/eureka/
eureka.client.register-with-eureka=true
eureka.client.fetch-registry=true
eureka.instance.prefer-ip-address=true
```

> ⚠️ Note: Ensure `localhost` spelling is correct.

---

## 3. ProductServicesApplication.java

```java
package com.example.productservices;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.EnableEurekaClient;

@SpringBootApplication
@EnableEurekaClient
public class ProductServicesApplication {

    public static void main(String[] args) {
        SpringApplication.run(ProductServicesApplication.class, args);
    }
}
```

---

## 4. Quick Checklist

- Ensure Eureka Server is running at `localhost:8761`.
    
- Create `productDB` in MySQL.
    
- Use `spring.jpa.hibernate.ddl-auto=validate` if tables already exist.
    
- Add `@Entity` classes and corresponding `@Repository` interfaces for JPA.
    
- Add REST endpoints in `@RestController` classes.
    

---

This file can be used as a reference for setting up the Product Service project in one go.