![[Pasted image 20250930110837.png]]

#### Classes
![[Pasted image 20250930114123.png]]

# Docker Compose Setup for IntelliJ Project

This project uses **Docker Compose** to spin up a PostgreSQL container along with reserved volumes and a custom network. The configuration file is named `docker-compose.yml`.

---

## docker-compose.yml

```yaml
services:  
  postgres:  
    container_name: ms_pg_sql  
    image: postgres:latest  
    environment:  
      POSTGRES_USER: alibou  
      POSTGRES_PASSWORD: alibou  
      PGDATA: /var/lib/postgresql/data  
      
networks:  
  microservices-net:  
    driver: bridge  
    
volumes:  
  postgres:  
  pgadmin:  
  mongo:
```

---

## Explanation

### Services

- **postgres**
    
    - Runs a container based on the official `postgres:latest` image.
        
    - Container is named `ms_pg_sql` for easier reference.
        

### Environment Variables

- **POSTGRES_USER=alibou** → Creates an admin user called `alibou` at first start.
    
- **POSTGRES_PASSWORD=alibou** → Sets the password for the `alibou` user.
    
- **PGDATA=/var/lib/postgresql/data** → Defines where Postgres stores data files inside the container.
    

### Networks

- **microservices-net**
    
    - A user-defined bridge network.
        
    - Containers attached can communicate by service name.
        
    - Provides isolation and automatic DNS resolution.
        

### Volumes

- **postgres, pgadmin, mongo**
    
    - Declared as named volumes.
        
    - Ensure persistent storage beyond container lifecycle.
        
    - Example (for persistence):
        
```yaml
        volumes:
          - postgres:/var/lib/postgresql/data
```
        

---

## How to Use

1. Place `docker-compose.yml` in your IntelliJ project root.
    
2. Run:
    
    ```bash
    docker-compose up -d
    ```
    
    This will start PostgreSQL in the background.
    
3. To stop containers:
    
    ```bash
    docker-compose down
    ```
    
4. To inspect the network:
    
    ```bash
    docker network ls
    docker network inspect microservices-net
    ```
    

---
