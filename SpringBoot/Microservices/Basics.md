![[Pasted image 20250929144523.png]]

#### Arch
![[Pasted image 20250929144606.png]]

#### Plan
![[Pasted image 20250929144755.png]]

### **Eureka Server Setup (3 Steps)**

**Step 1 – Create Project**

- Use start.spring.io
    
- Add dependencies:
    
    - **Eureka Server (Netflix)**
        
    - **Spring Boot DevTools**
        
---

**Step 2 – Add Configuration**  

In application.properties:

```
server.port=8761 

eureka.client.fetch-registry=false
eureka.client.register-with-eureka=false
eureka.instance.prefer-ip-address=true
```

## fetch-registry=false

- Disables downloading the registry from a Eureka server, so the application will not cache or discover other services through Eureka.[spring](https://docs.spring.io/spring-cloud-netflix/reference/configprops.html)
    
- Commonly set on a standalone Eureka server so it doesn’t try to act like a client fetching its own or other registries.[springframework+1](https://springframework.guru/eureka-service-registry/)
    
## register-with-eureka=false

- Prevents the application from registering itself as an instance in Eureka, so it won’t appear in the service registry or be discoverable by others.[stackoverflow+1](https://stackoverflow.com/questions/57639611/what-is-the-use-of-fetchregistry-property-in-eureka-server)
    
- Also typical for a dedicated Eureka server, which should not register itself as a client in single-server setups.[studytonight+1](https://www.studytonight.com/post/service-discovery-using-eureka-in-spring-microservices)
    
## prefer-ip-address=true

- Instructs the Eureka client to advertise its IP address instead of hostname in its instance metadata, which helps avoid DNS/hostname resolution issues in certain networks or containers.[spring](https://docs.spring.io/spring-cloud-netflix/reference/configprops.html)
---

**Step 3 – Enable Eureka Server**  
In `EurekaServerApplication.java`:

```
@SpringBootApplication 
@EnableEurekaServer 
public class EurekaServerApplication {    
		public static void main(String[] args) {            SpringApplication.run(EurekaServerApplication.class, args);    
 } 
 }
```

---

✅ Run the project → open [http://localhost:8761](http://localhost:8761) → Eureka Dashboard is ready.



