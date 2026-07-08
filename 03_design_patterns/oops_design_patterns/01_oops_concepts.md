**1. What is OOPS ?**
- Language in which objects are first class citizens 
- Uses real world analogy like- inheritance, polymorphism, abstraction etc
- Manipulating these objects to get results is the goal of Object Oriented Programming.

---

**2. OOP Concepts ?**
- Inheritance
	- Inheriting the properties of parents 
- Abstraction 
    - Hides implementation details and exposes only essential features.
    - Example: A driver uses a car without knowing how the engine works.

```java
// Abstract class
abstract class Car {
    abstract void startEngine(); // only defines WHAT to do
}

// Concrete class
class Tesla extends Car {
    @Override
    void startEngine() {
        System.out.println("Tesla engine starts silently...");
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Tesla();
        myCar.startEngine(); // Driver doesn’t care HOW it works
    }
}

```

- Encapsulation
    - Wrapping data (variables) and methods into a single unit (class).
    - Protects data using access modifiers (private, public).
    - Example: private salary field accessed via getter/setter.
- Polymorphism
    - Ability of an object to take many forms.
    - Compile-time polymorphism → Method overloading.
    - Runtime polymorphism → Method overriding.

---

**3. Abstraction vs. Encapsulation ?**
- Encapsulation → How functionality is achieved (implementation level).
- Abstraction → What functionality is provided (design level).

---

**4.Association, Aggregations, Compositions**

- Association
  - Relationship between two independent classes via objects.
  - Can be one-to-one, one-to-many, many-to-one, many-to-many.
- Aggregation
  - “Has-a” relationship where the child can exist independently.
  - Example: Employee belongs to an Organization but can exist without it.

```java
public class Organization {
    private List<Person> employees;
}

public class Person {
    private String name;
}
  
```
- Composition
  - Strong “part-of” relationship where the child cannot exist without the parent.
  - Example: A Car has an Engine; if the Car is destroyed, the Engine ceases to exist.

```java
public class Body {
    private final Hand hand;  
    public Body() {
        hand = new Hand();
    }
}
class Hand {
    private String whichHand;
}

```
  
**5. UML Notations of Association, Aggregations, Compositions**
- Associations ------------->
- Aggregation  ------------<>
- Composition  ------------<> // Diamond is filled

**6. Why do you think OOPS brought evolution?**
- Shifted programming from procedural to object-based design.
- Improved modularity, reusability, and scalability.
- Enabled modeling of complex real-world systems more naturally.

Shift from Procedural to Object-Based Design

```java
// Procedural style
int length = 5;
int breadth = 10;

int area(int l, int b) {
    return l * b;
}

System.out.println(area(length, breadth));

```
Object-Oriented (data + behavior together)

```java
// Object-oriented style
class Rectangle {
    int length;
    int breadth;

    Rectangle(int l, int b) {
        length = l;
        breadth = b;
    }

    int area() {
        return length * breadth;
    }
}

public class Main {
    public static void main(String[] args) {
        Rectangle rect = new Rectangle(5, 10);
        System.out.println(rect.area()); // cleaner, modular
    }
}

```

Notice how procedural programming separates data and functions, while object-oriented programming binds them together, making code more modular and reusable.

**7. Cohesion**
- High Cohesion → Each class focuses on a single responsibility.
- Loose Coupling → Classes are independent, reducing dependency.
- Together, they make systems easier to maintain and extend.