```
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
 
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
			<!-Exclude Jersey, use SpringMVC Rest->
			<exclusions>
				<exclusion>
					<groupId>com.sun.jersey</groupId>
					<artifactId>jersey-client</artifactId>
				</exclusion>
				<exclusion>
					<groupId>com.sun.jersey</groupId>
					<artifactId>jersey-core</artifactId>
				</exclusion>
				<exclusion>
					<groupId>com.sun.jersey.contribs</groupId>
					<artifactId>jersey-apache-client4</artifactId>
				</exclusion>
			</exclusions>
		</dependency>

```

```properties
spring.application.name=user-service
server.port=8081

eureka.client.serviceUrl.defaultZone=http://localhost:8761/eureka/
eureka.client.register-with-eureka=true
eureka.client.fetch-registry=true
eureka.instance.prefer-ip-address=true

```

```
<dependencyManagement>
<dependencies>
<dependency>
<groupId>org.springframework.cloud</groupId>
<artifactId>spring-cloud-dependencies</artifactId>

<version>2025.0.0</version>

<type>pom</type>

<scope>import</scope>
</dependency>
</dependencies>

</dependencyManagement>
```

```
<build>  
    <plugins>       <plugin>          <groupId>org.springframework.boot</groupId>  
          <artifactId>spring-boot-maven-plugin</artifactId>  
       </plugin>    </plugins></build>
```