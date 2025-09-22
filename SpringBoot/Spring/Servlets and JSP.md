- Java Servlet is a Java program that runs on a Java-enabled web server or application server. It handles client requests, processes them and generates responses dynamically. 

- Servlets are the backbone of many server-side Java applications due to their efficiency and scalability.

****Key Features:****

- Servlets work on the server side.
- Servlets are capable of handling complex requests obtained from the web server.
- Generate dynamic responses efficiently.

## Java Servlets Architecture

- It is responsible for handling important tasks like load balancing, session management and resource allocation, it make sure that all the requests are process efficiently under high traffic. 
- The container distribute requests across multiple instances, which helps improve the system performance.
![[Pasted image 20250922115442.png]]

#### Life Cycle of a Servlet

The entire life cycle of a Servlet is managed by the Servlet container, which uses the ****jakarta.servlet.Servlet**** interface to understand the Servlet object and manage it.
![[Pasted image 20250922120154.png]]

### ****1. Loading a Servlet****

The first stage of the Servlet lifecycle involves loading and initializing the Servlet. The Servlet container performs the following operations:

- ****Loading:**** The Servlet container loads the Servlet class into memory.
- ****Instantiation:**** The container creates an instance of the Servlet using the no-argument constructor.

The Servlet container can load the Servlet at one of the following times:

- During the initialization of the web application (if the Servlet is configured with a zero or positive integer value in the deployment descriptor).
- When the Servlet is first requested by a client (if lazy loading is enabled).

### ****2. Initializing a Servlet****

After the Servlet is instantiated, the Servlet container initializes it by calling the init(ServletConfig config) method. This method is called only once during the Servlet's life cycle.

### ****3. Handling request****

Once the Servlet is initialized, it is ready to handle client requests. The Servlet container performs the following steps for each request:

- ****Create Request and Response Objects****
    - The container creates `ServletRequest` and `ServletResponse` objects.
    - For HTTP requests, it creates `HttpServletRequest` and `HttpServletResponse` objects.
- ****Invoke the service() Method****
    - The container calls the service(ServletRequest req, ServletResponse res) method.
    - The service() method determines the type of HTTP request (GET, POST, PUT, DELETE, etc.) and delegates the request to the appropriate method (doGet(), doPost(), etc).

### ****4. Destroying a Servlet****

When the Servlet container decides to remove the Servlet, it follows these steps which are listed below

- ****Allow Active Threads to Complete:**** The container ensures that all threads executing the service() method complete their tasks.
- ****Invoke the destroy() Method:**** The container calls the destroy() method to allow the Servlet to release resources (e.g., closing database connections, freeing memory).
- ****Release Servlet Instance:**** After the destroy() method is executed, the Servlet container releases all references to the Servlet instance, making it eligible for garbage collection

## Servlet Life Cycle Methods

There are three life cycle methods of a Servlet:

- init()
- service()
- destroy()

![[Pasted image 20250922120257.png]]

Servlet life cycle can be defined as the stages through which the servlet passes from its creation to its destruction.  
The servlet life cycle consists of these stages:

- Servlet is created
- Servlet is initialized
- Servlet is ready to service
- Servlet is servicing
- Servlet is not ready to service
- Servlet is destroyed

### Working of Servlets

1. ****Client Request:**** A client (e.g., browser) sends an HTTP request to the web server.
2. ****Request Forwarded to Servlet:**** The web server passes the request to the Servlet container (like Tomcat).
3. ****Servlet Processing:**** Container calls the servlet's service() method. Based on the request type (GET, POST), it invokes doGet() or doPost().
4. ****Business Logic Execution:**** Servlet processes the request (e.g., reading form data, querying a database).
5. ****Response Generation:**** Servlet creates a response (usually HTML) using HttpServletResponse.
6. ****Response Sent to Client:**** The Web server sends the generated response back to the client.
#### Introduction to JSP

JavaServer Pages (JSP) is a server-side technology that creates dynamic web applications. It allows developers to embed Java code directly into HTML pages and it makes web development more efficient.

JSP is an advanced version of Servlets. It provides enhanced capabilities for building scalable and platform-independent web pages.

### How is JSP More Advantageous than Servlets?

JSP simplifies web development by combining the strengths of Java with the flexibility of HTML. Some advantages of JSP over Servlets are listed below:

- JSP code is easier to manage than Servlets as it separates UI and business logic.
- JSP minimizes the amount of code required for web applications.
- Generate content dynamically in response to user interactions.
- It provides access to the complete range of Java APIs for robust application development.
- JSP is suitable for applications with growing user bases.

### Key Features of JSP

- It is platform-independent; we can write once, run anywhere.
- It simplifies database interactions for dynamic content.
- It contains predefined objects like request, response, session and application, reducing development time.
- It has built-in mechanisms for exception and error management.
- It supports custom tags and tag libraries.

## JSP Architecture

JSP follows a three-layer architecture:

- ****Client Layer****: The browser sends a request to the server.
- ****Web Server Layer****: The server processes the request using a JSP engine.
- ****Database/Backend Layer****: Interacts with the database and returns the response to the client.

### JSP Elements

We will learn several elements available in JSP with suitable examples. In JSP elements can be divided into 4 different types.

- Expression
- Scriptlets
- Directives
- Declarations

### 1. Expression

This tag is used to output any data on the generated page. These data are automatically converted to a string and printed on the output stream.

****Syntax:****

> <%= "Anything" %>

****Note****: JSP Expressions start with Syntax of JSP Scriptles are with <%=and ends with %>.  Between these, you can put anything that will convert to the String and that will be displayed.

****Example:****

> <%="HelloWorld!" %>

### 2. Scriplets

This allows inserting any amount of valid Java code. These codes are placed in the _jspService() method by the JSP engine.

****Syntax****:

> <%
> 
> // Java codes
> 
> %>

Note: JSP Scriptlets begins with <% and ends %> . We can embed any amount of Java code in the JSP Scriptlets. JSP Engine places these codes in the _jspService() method.

****Example:****

> <%  
> String name = "Geek";  
> out.println("Hello, " + name);  
> %>

Variables available to the JSP Scriptlets are:

-  Request
-  Response
-  Session
-  Out

### 3. Directives

A JSP directive starts with <%@ characters. In the directives, we can import packages, define error-handling pages or configure session information for the JSP page.

****Syntax:****

> <%@ directive attribute="value" %>  

#### Types of Directives:

- page: It defines page settings.
- include: It includes other files.
- taglib: It declares a custom tag library.

### 4. Declarations

This is used for defining functions and variables to be used in the JSP.

****Syntax:****

> <%!  
> //java codes  
> %>

****Note****: JSP Declaratives begins with <%! and ends %> with We can embed any amount of java code in the JSP Declaratives. Variables and functions defined in the declaratives are class-level and can be used anywhere on the JSP page. 

### Example of a JSP Web Page

```
<!DOCTYPE html> 
<html> 
<head>     
<title>A Web Page</title> </head> 
<body>    
<% out.println("Hello there!"); %> 
</body> 
</html>
```

### Why Use JSP?

JSP is powerful because it allows us :

- Embed Java logic directly into HTML.
- To create dynamic pages that respond to user actions.
- To customize content for each user or session.