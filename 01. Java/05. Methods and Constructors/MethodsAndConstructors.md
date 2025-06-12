# Methods and Constructors

## Methods in Java

### Definition and Purpose
- A method is a collection of instructions that performs a specific task
- Methods enable code reusability and organization
- They encapsulate functionality that can be called multiple times
- Methods improve code readability and maintainability

### Method Declaration Syntax
```java
[access_specifier] [return_type] method_name([parameters]) [throws exceptions] {
    // method body
    return [value]; // if return type is not void
}
```

### Components of a Method
1. **Access Specifiers** (4 types):
   - `public`: Accessible from any class in any package
   - `private`: Accessible only within the same class
   - `protected`: Accessible within the same package or by subclasses in different packages
   - `default` (package-private): Accessible only within the same package (no modifier specified)

2. **Return Type**:
   - Specifies the data type of the value returned by the method
   - Use `void` if the method doesn't return anything
   - Can be primitive types (int, double, etc.) or reference types (objects)

3. **Method Name**:
   - Should be a verb or action-oriented
   - Follow camelCase convention (start with lowercase, capitalize subsequent words)
   - Should be meaningful and descriptive of the method's purpose

4. **Parameters**:
   - Variables passed to the method for its operation
   - Can be zero or more parameters
   - Each parameter must have a type and name
   - Parameters are separated by commas

5. **Method Body**:
   - Contains the actual implementation
   - Enclosed in curly braces {}
   - Can include local variables, control statements, and other method calls
   - Must return a value of the specified type (unless void)

### Example Method
```java
public class Calculation {
    public int sum(int val1, int val2) {
        int total = val1 + val2; // Instruction 1
        System.out.println("addition of val1 and val2 is: " + total); // Instruction 2
        return total; // Instruction 3
    }
    
    public int getPriceOfPen() {
        int capPrice = 2;
        int penBodyPrice = 5;
        int totalPenPrice = sum(capPrice, penBodyPrice);
        return totalPenPrice;
    }
}
```

### Types of Methods

1. **System-Defined Methods**:
   - Predefined methods in Java libraries
   - Examples: `Math.sqrt()`, `System.out.println()`

2. **User-Defined Methods**:
   - Created by programmers for specific application needs
   - Example: The `sum()` method in the Calculation class above

3. **Overloaded Methods**:
   - Multiple methods with the same name but different parameters
   - Differentiated by parameter types, number of parameters, or order
   - Return type is not considered for overloading
   - Example:
     ```java
     public class Invoice {
         void getInvoice() {
             System.out.println("inside invoice method");
         }
         
         void getInvoice(String z) { /* ... */ }
         
         int getInvoice(int a) { /* ... */ }
         
         void getInvoice(int a, int b) { /* ... */ }
     }
     ```

4. **Overridden Methods**:
   - Methods in child classes that have the same signature as parent class methods
   - Used for runtime polymorphism

5. **Static Methods**:
   - Associated with the class rather than instances
   - Called using class name (ClassName.methodName())
   - Cannot access non-static variables/methods directly
   - Cannot be overridden
   - Best for utility methods that don't modify object state
   - Example: Factory design pattern methods

6. **Final Methods**:
   - Cannot be overridden by subclasses
   - Used when method implementation should not change

7. **Abstract Methods**:
   - Declared in abstract classes without implementation
   - Implementation provided by concrete subclasses
   - Must be overridden by first concrete subclass

### Variable Arguments (Varargs)
- Allows methods to accept variable number of arguments
- Only one varargs parameter per method
- Must be the last parameter
- Syntax: `type... variableName`
- Example:
  ```java
  public class Calculation {
      public int sum(int a, int... variable) {
          int output = a;
          for(int var : variable) {
              output = output + var;
          }
          return output;
      }
  }
  
  // Usage:
  calculationObj.sum(3); // a=3, variable=[]
  calculationObj.sum(3, 8, 9, 10); // a=3, variable=[8,9,10]
  calculationObj.sum(3, 8, 9, 10, 3, 3, 2, 2, 2, 2, 2, 2);
  ```

## Constructors in Java

### Definition and Purpose
- Special methods used to initialize objects
- Called when an object is created using `new` keyword
- Primary purpose is to initialize instance variables
- Constructors enable object creation with specific initial states

### Key Characteristics
1. **Name**: Must exactly match the class name
2. **No Return Type**: Not even void (implicitly returns the class instance)
3. **Cannot Be**:
   - `static`: Because they initialize instance variables
   - `final`: Since constructors cannot be inherited/overridden
   - `abstract`: Because they must have concrete implementation
   - `synchronized`: Not applicable to constructors

### Why Constructors Have Special Rules
- **Same Name as Class**: Makes it easy to identify as a constructor (no return type)
- **No Return Type**: Implicitly returns the class instance
- **Cannot Be Final**: Constructors aren't inherited, so final is meaningless
- **Cannot Be Abstract**: Must have concrete implementation
- **Cannot Be Static**: Need to initialize instance variables

### Types of Constructors

1. **Default Constructor**:
   - Provided by Java if no constructor is defined
   - Takes no arguments
   - Initializes instance variables with default values (0, null, false, etc.)

2. **No-Argument Constructor**:
   - User-defined constructor with no parameters
   - Similar to default constructor but can include custom initialization
   - Example:
     ```java
     public class MyClass {
         public MyClass() {
             // initialization code
         }
     }
     ```

3. **Parameterized Constructor**:
   - Takes parameters to initialize instance variables
   - Allows object creation with specific initial values
   - Example:
     ```java
     public class Student {
         String name;
         int age;
         
         public Student(String name, int age) {
             this.name = name;
             this.age = age;
         }
     }
     ```

4. **Constructor Overloading**:
   - Multiple constructors with different parameter lists
   - Provides flexibility in object initialization
   - Example:
     ```java
     public class Rectangle {
         int width, height;
         
         public Rectangle() { // No-arg
             width = height = 1;
         }
         
         public Rectangle(int size) { // Square
             width = height = size;
         }
         
         public Rectangle(int w, int h) { // Rectangle
             width = w;
             height = h;
         }
     }
     ```

5. **Private Constructor**:
   - Prevents instantiation from outside the class
   - Used in singleton design pattern
   - Example:
     ```java
     public class Singleton {
         private static Singleton instance;
         
         private Singleton() { /* ... */ }
         
         public static Singleton getInstance() {
             if(instance == null) {
                 instance = new Singleton();
             }
             return instance;
         }
     }
     ```

### Constructor Chaining
- Calling one constructor from another
- Achieved using `this()` (same class) or `super()` (parent class)
- Must be the first statement in the constructor

1. **Using this()**:
   ```java
   public class Calculation {
       String name;
       int empID;
       
       Calculation() {
           this(10); // Calls parameterized constructor
       }
       
       Calculation(int empID) {
           this("default", empID); // Calls another constructor
       }
       
       Calculation(String name, int empID) {
           this.name = name;
           this.empID = empID;
       }
   }
   ```

2. **Using super()**:
   - Child class constructor always calls parent class constructor first
   - Implicitly calls super() if not explicitly specified
   - Must be first statement in child constructor
   - Example:
     ```java
     class Parent {
         Parent(int x) { /* ... */ }
     }
     
     class Child extends Parent {
         Child() {
             super(10); // Must explicitly call parameterized parent constructor
             // child initialization
         }
     }
     ```

### Important Notes
- If parent class has only parameterized constructors, child must explicitly call one using super()
- Constructor chaining helps avoid code duplication
- Default constructor is not provided if any constructor is defined
- Interfaces cannot have constructors (since they can't be instantiated)

### Best Practices
- Keep constructors simple (avoid complex logic)
- Use constructor overloading judiciously
- Consider using factory methods for complex object creation
- Document constructor behavior clearly
- Initialize all essential fields in constructors