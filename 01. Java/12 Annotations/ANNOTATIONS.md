# **Annotations in Java**  

## **1. Overview of Annotations**  
Annotations in Java provide a way to add **metadata** (additional information) to Java code without altering its functionality.  

### **Key Characteristics:**  
- **Do not modify program behavior** directly but can influence compilation or runtime processing.  
- Can be applied to **classes, methods, fields, parameters, and other program elements**.  
- Processed at:  
  - **Compile-time** (e.g., `@Override`, `@Deprecated`)  
  - **Runtime** (via Reflection, e.g., Spring `@Autowired`)  

### **Example of Built-in Annotations:**  
- `@Override` – Indicates method overriding.  
- `@Deprecated` – Marks code as obsolete.  
- `@SuppressWarnings` – Suppresses compiler warnings.  

---

## **2. Creating Custom Annotations**  
Annotations are defined using the `@interface` keyword.  

### **Syntax:**  
```java
public @interface MyAnnotation {
    String value() default "defaultValue"; // Optional element with default value
    int version() default 1;               // Another element
}
```

### **Annotation Elements:**  
- Can have **primitive types, `String`, `Class`, enums, other annotations, or arrays** of these.  
- **Default values** can be provided using `default`.  

### **Example Usage:**  
```java
@MyAnnotation(value = "customValue", version = 2)
public class MyClass { ... }
```

---

## **3. Processing Annotations (Using Reflection)**  
Annotations can be read at runtime using **Java Reflection API**.  

### **Example: Reading Method Annotations**  
```java
Method[] methods = MyClass.class.getDeclaredMethods();
for (Method method : methods) {
    if (method.isAnnotationPresent(MyAnnotation.class)) {
        MyAnnotation annotation = method.getAnnotation(MyAnnotation.class);
        System.out.println("Value: " + annotation.value());
    }
}
```

### **Key Reflection Methods:**  
- `isAnnotationPresent(Class)` → Checks if an annotation exists.  
- `getAnnotation(Class)` → Retrieves the annotation instance.  
- `getAnnotations()` → Returns all annotations.  

---

## **4. JavaDoc and Annotations**  
By default, annotations **do not appear** in JavaDoc. To include them:  

### **Using `@Documented` Meta-Annotation**  
```java
import java.lang.annotation.Documented;

@Documented
public @interface Service {
    String serviceName();
}
```
Now, `@Service` will appear in generated JavaDoc.  

### **Generating JavaDoc (IntelliJ/Eclipse):**  
1. **IntelliJ:**  
   - `Tools > Generate JavaDoc`  
   - Configure output directory and scope.  
2. **Eclipse:**  
   - `Project > Generate Javadoc`  

---

## **5. Meta-Annotations (Annotations for Annotations)**  
Meta-annotations define **how annotations behave**.  

### **Key Meta-Annotations:**  

| Meta-Annotation | Purpose | Example |
|-----------------|---------|---------|
| `@Retention` | Specifies **how long** the annotation is retained. | `@Retention(RetentionPolicy.RUNTIME)` |
| `@Target` | Defines **where** the annotation can be applied. | `@Target(ElementType.METHOD)` |
| `@Documented` | Ensures annotation appears in JavaDoc. | `@Documented` |
| `@Inherited` | Allows subclasses to **inherit** parent class annotations. | `@Inherited` |
| `@Repeatable` | Allows **multiple** annotations of the same type. | `@Repeatable(Schedules.class)` |

### **Example: Defining Retention & Target**  
```java
import java.lang.annotation.*;

@Retention(RetentionPolicy.RUNTIME) // Available at runtime
@Target({ElementType.METHOD, ElementType.TYPE}) // Applicable to methods & classes
public @interface Loggable { }
```

---

## **6. Practical Use Cases**  

### **A. Custom Service Annotation (Dependency Injection-like)**  
```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface Service {
    String serviceName();
}

@Service(serviceName = "userService")
public class UserService { ... }
```

### **B. Logging Framework (AOP-like)**  
```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface LogExecutionTime { }

// Aspect processing (using reflection)
public class LoggingAspect {
    public static void logIfAnnotated(Object obj) throws Exception {
        for (Method method : obj.getClass().getMethods()) {
            if (method.isAnnotationPresent(LogExecutionTime.class)) {
                long startTime = System.currentTimeMillis();
                method.invoke(obj);
                long endTime = System.currentTimeMillis();
                System.out.println("Execution time: " + (endTime - startTime) + "ms");
            }
        }
    }
}
```

---

## **7. Annotations in Aspect-Oriented Programming (AOP)**  
In **Spring AOP**, annotations define **pointcuts** (where advice should apply).  

### **Example: Spring `@Transactional`**  
```java
@Target({ElementType.METHOD, ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
public @interface Transactional { }

// Usage
@Transactional
public void saveUser(User user) { ... }
```

### **Pointcut Matching Annotations (Spring AOP)**  
```java
@Aspect
public class TransactionAspect {
    @Around("@annotation(Transactional)")
    public Object manageTransaction(ProceedingJoinPoint pjp) throws Throwable {
        // Start transaction
        Object result = pjp.proceed();
        // Commit transaction
        return result;
    }
}
```

---

## **8. Best Practices & Limitations**  

### **Best Practices:**  
✔ Use annotations for **metadata**, not business logic.  
✔ Prefer **runtime retention** only when necessary.  
✔ Use `@Target` to restrict where annotations apply.  

### **Limitations:**  
❌ Cannot **modify behavior** directly (unlike AspectJ weaving).  
❌ Overuse can make code **harder to debug**.  

---

## **9. Conclusion**  
- Annotations provide **metadata** without changing code behavior.  
- Can be processed at **compile-time** or **runtime** (via reflection).  
- **Meta-annotations** (`@Retention`, `@Target`, etc.) control annotation behavior.  
- Widely used in:  
  - **Frameworks (Spring, Hibernate)**  
  - **Code documentation (`@Documented`)**  
  - **AOP (AspectJ, Spring AOP)**  

Annotations enhance **readability, maintainability, and reduce boilerplate** in modern Java applications.  

---

### **Further Exploration:**  
- **Annotation Processors** (Compile-time annotation processing)  
- **Bytecode Manipulation** (ASM, Javassist for advanced use cases)  
- **Spring Stereotype Annotations** (`@Component`, `@Service`, `@Repository`)  

This concludes the detailed breakdown of Java annotations. 🚀