![[Pasted image 20250922075252.png]]
## Simple steps

- Load Spring context from classpath file spring.xml using ClassPathXmlApplicationContext.
    
- Look up a bean with id/name "dev" from the context via getBean and cast to Dev.
- Invoke build() on that Dev bean instance.[spring](https://docs.spring.io/spring-framework/reference/core/beans/basics.html)
## Why it’s used

- The ApplicationContext creates and wires beans defined in XML, so code doesn’t manually construct dependencies.[spring+1](https://docs.spring.io/spring-framework/reference/core/beans/introduction.html)
    
- This is an example of IoC/DI: the container manages object creation and lifecycle.[spring+1](https://docs.spring.io/spring-framework/reference/core/beans/introduction.html)
## Notes

- spring.xml must be on the classpath (e.g., resources folder).
    
- Modern Spring often prefers Java or annotation config instead of XML, but this snippet is valid for XML setups