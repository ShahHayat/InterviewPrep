# **OOPs Concepts in Java**

## **1. Overview**
- **Definition**: Object-Oriented Programming (OOP) is a programming paradigm that organizes software design around objects rather than functions and logic.
- **Key Characteristics**:
  - Programs are divided into **objects** (real-world entities like Car, ATM, Bike, etc.).
  - Emphasizes **data hiding** and **encapsulation** for security.
  - Supports **overloading**, **inheritance**, and **polymorphism**.
  - Enhances **code reusability** and **modularity**.

### **Comparison: Procedural vs. OOP**
| **Procedural Programming** | **Object-Oriented Programming (OOP)** |
|----------------------------|---------------------------------------|
| Programs are divided into functions. | Programs are divided into objects. |
| No data hiding; functions and data are loosely coupled. | Objects provide **data hiding**; emphasis on data security. |
| **Overloading is not possible**. | **Overloading is possible**. |
| **Inheritance is not possible**. | **Inheritance is supported**. |
| **No code accessibility control**. | **Access modifiers (public, private, protected) control accessibility**. |
| Examples: C, Pascal, Fortran. | Examples: Java, C#, Python, C++. |

---

## **2. Objects and Classes**
### **Objects**
- An object is an instance of a class.
- **Two key components**:
  1. **Properties/State (Attributes)**: Variables that define the object's characteristics (e.g., `color`, `age`, `brand`).
  2. **Behavior (Methods)**: Actions the object can perform (e.g., `bark()`, `drive()`, `sleep()`).

**Examples**:
- **Dog Object**:
  - Properties: `age`, `color`, `breed`.
  - Behavior: `bark()`, `eat()`, `sleep()`.
- **Car Object**:
  - Properties: `color`, `brand`, `weight`.
  - Behavior: `applyBrake()`, `drive()`, `increaseSpeed()`.

### **Classes**
- A **blueprint/template** for creating objects.
- Defines the structure (attributes and methods) that objects will have.
- **Syntax**:
  ```java
  class ClassName {
      // Fields (variables)
      // Methods (functions)
  }
  ```
- **Example**:
  ```java
  class Student {
      int age;
      String name;
      String address;

      void updateAddress(String newAddress) {
          this.address = newAddress;
      }

      int getAge() {
          return age;
      }
  }
  ```
- **Creating an Object**:
  ```java
  Student english = new Student(); // Instantiates a Student object
  ```

---

## **3. Four Pillars of OOPs**
### **1. Data Abstraction**
- **Definition**: Hiding internal implementation and exposing only essential features.
- **Achieved via**:
  - **Abstract classes** (partial abstraction).
  - **Interfaces** (full abstraction).
- **Example**:
  - **Car Brake System**: User presses the brake pedal, but the internal mechanism (hydraulics, sensors) is hidden.
  - **Cellphone**: User interacts with buttons/screen, but internal circuitry is abstracted.
- **Advantages**:
  - Improves **security** (users cannot access internal logic).
  - Simplifies **complexity**.

**Demo (Interface Example)**:
```java
interface Car {
    void applyBrake();
    void incSpeed();
}

class Suzuki implements Car {
    public void applyBrake() {
        // Hidden implementation (e.g., hydraulic system)
        System.out.println("Car stopped");
    }
}
```
- User calls `applyBrake()` without knowing how it works internally.

---

### **2. Encapsulation (Data Hiding)**
- **Definition**: Bundling data (variables) and methods (functions) into a single unit (class) and restricting direct access to data.
- **Steps**:
  1. Declare variables as `private`.
  2. Provide `public` getter/setter methods to access/modify them.
- **Advantages**:
  - **Security**: Prevents unauthorized access.
  - **Flexibility**: Allows controlled modifications.
  - **Loose Coupling**: Reduces dependency between components.

**Demo**:
```java
class Dog {
    private String color;

    // Getter
    String getColor() {
        return this.color;
    }

    // Setter
    void setColor(String color) {
        this.color = color;
    }
}
```
**Usage**:
```java
Dog lab = new Dog();
lab.setColor("black");
System.out.println(lab.getColor()); // Output: black
```

---

### **3. Inheritance**
- **Definition**: A mechanism where a child class inherits properties and methods from a parent class.
- **Keyword**: `extends`.
- **Types**:
  1. **Single Inheritance**: One child class inherits from one parent.
  2. **Multilevel Inheritance**: Chain of inheritance (A → B → C).
  3. **Hierarchical Inheritance**: Multiple children inherit from one parent.
  4. **Multiple Inheritance**: One child inherits from multiple parents (**not supported in Java** due to the **diamond problem**).  
     - **Workaround**: Use **interfaces** (`implements`).

**Demo**:
```java
class Vehicle {
    boolean engine;
    boolean getEngine() {
        return engine;
    }
}

class Car extends Vehicle {
    String type;
    String getCarType() {
        return type;
    }
}
```
**Usage**:
```java
Car swift = new Car();
swift.getEngine(); // Works (inherited from Vehicle)
Vehicle vehicle = new Vehicle();
vehicle.getCarType(); // Error (parent cannot access child methods)
```

---

### **4. Polymorphism**
- **Definition**: "Many forms" – the ability of a method to behave differently based on the context.
- **Types**:
  1. **Compile-Time (Static) Polymorphism**: Achieved via **method overloading**.
     - Same method name, different parameters.
  2. **Run-Time (Dynamic) Polymorphism**: Achieved via **method overriding**.
     - Same method signature in parent and child classes.

**Demo (Method Overloading)**:
```java
class Sum {
    int doSum(int a, int b) {
        return a + b;
    }
    int doSum(int a, int b, int c) {
        return a + b + c;
    }
}
```
**Demo (Method Overriding)**:
```java
class A {
    int getEngine() {
        return 1;
    }
}

class B extends A {
    @Override
    int getEngine() {
        return 2;
    }
}
```
**Usage**:
```java
B obj = new B();
obj.getEngine(); // Returns 2 (overridden method)
```

---

## **4. Relationships in OOP**
### **1. "Is-A" Relationship (Inheritance)**
- Represents **inheritance** (e.g., "Dog **is an** Animal").
- Achieved using `extends`.
- Example:
  ```java
  class Animal {}
  class Dog extends Animal {} // Dog is an Animal
  ```

### **2. "Has-A" Relationship (Association)**
- Represents **object composition** (one object contains another).
- Types:
  1. **Aggregation**: Weak relationship (objects can exist independently).
     - Example: "School **has** Students" (school can exist without students).
  2. **Composition**: Strong relationship (child object cannot exist without parent).
     - Example: "Car **has** Engine" (engine cannot exist without car).

---

## **Summary of Key Concepts**
| **Concept** | **Definition** | **Example** |
|-------------|---------------|-------------|
| **Class** | Blueprint for objects | `class Car { ... }` |
| **Object** | Instance of a class | `Car myCar = new Car();` |
| **Abstraction** | Hiding internal details | Interface `applyBrake()` |
| **Encapsulation** | Data hiding with getters/setters | `private String color;` |
| **Inheritance** | Child class inherits from parent | `class Car extends Vehicle` |
| **Polymorphism** | Same method, different behaviors | Method overloading/overriding |

---

## **Conclusion**
OOPs concepts in Java provide a structured approach to software design, promoting **reusability**, **modularity**, and **security**. Mastering these principles is essential for writing efficient and maintainable Java code.