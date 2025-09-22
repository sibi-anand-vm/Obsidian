### 📦 **GAV (GroupId, ArtifactId, Version)**

Every Maven dependency or project is uniquely identified by its **GAV coordinates**:

- **GroupId** → identifies the group or organization (e.g., `org.springframework.boot`)
    
- **ArtifactId** → the name of the project/module (e.g., `spring-boot-starter-web`)
    
- **Version** → the version of that artifact (e.g., `3.2.2`)
    

👉 Together, `org.springframework.boot:spring-boot-starter-web:3.2.2` uniquely identifies the dependency.

💡 Sometimes you’ll also see **Packaging** (like `jar`, `war`, `pom`), making it **GAVP**.

## 🏗<font color="#4f81bd"> Archetypes</font>

A **Maven archetype** is a **project template**.  
It generates a project with a predefined structure and starter `pom.xml`.

Think of it like a **cookie cutter** 🍪 → instead of shaping each cookie (project) manually, you use a cutter (archetype) to get the right shape instantly.

In Java build tooling, an archetype is a Maven project template used to generate a new project skeleton quickly and consistently, with placeholders filled from developer input to match groupId, artifactId, package, and other properties.