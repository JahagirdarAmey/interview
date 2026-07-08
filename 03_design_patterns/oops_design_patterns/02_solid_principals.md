# SOLID Principles

### 1. Single Responsibility Principle (SRP)
- A class should have only one reason to change — one responsibility.

```java
// ❌ Bad: Handles both employee data and salary calculation
class Employee {
    String name;
    double salary;

    void calculateSalary() { /* logic */ }
    void saveToDatabase() { /* logic */ }
}

// ✅ Good: Split responsibilities
class Employee {
    String name;
    double salary;
}

class SalaryCalculator {
    void calculateSalary(Employee emp) { /* logic */ }
}

class EmployeeRepository {
    void save(Employee emp) { /* logic */ }
}
```

### 2. Open/Closed Principle (OCP)
- Classes should be open for extension but closed for modification.

```java
// Base class
abstract class Shape {
    abstract double area();
}

// Extended classes
class Circle extends Shape {
    double radius;
    Circle(double r) { radius = r; }
    double area() { return Math.PI * radius * radius; }
}

class Rectangle extends Shape {
    double length, breadth;
    Rectangle(double l, double b) { length = l; breadth = b; }
    double area() { return length * breadth; }
}

```
Adding new shapes doesn’t require modifying existing code.

### 3. Liskov Substitution Principle (LSP)
- Objects of a superclass should be replaceable with objects of its subclasses without breaking functionality.

```java
class Bird {
    void fly() { System.out.println("Flying..."); }
}

class Sparrow extends Bird { } // ✅ Valid substitution

class Ostrich extends Bird {
    @Override
    void fly() { throw new UnsupportedOperationException("Ostrich can't fly!"); } // ❌ Violates LSP
}

```

Ostrich shouldn’t inherit fly() if it can’t fly. Better design: separate FlyingBird and NonFlyingBird.

### 4. Interface Segregation Principle (ISP)
- Clients shouldn’t be forced to depend on methods they don’t use.

```java
// ❌ Bad: One big interface
interface Worker {
    void work();
    void eat();
}

// ✅ Good: Split interfaces
interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

class Robot implements Workable {
    public void work() { System.out.println("Robot working..."); }
}

class Human implements Workable, Eatable {
    public void work() { System.out.println("Human working..."); }
    public void eat() { System.out.println("Human eating..."); }
}

```

### 5. Dependency Inversion Principle (DIP)
- High-level modules shouldn’t depend on low-level modules; both should depend on abstractions.

```java
// Bad Example (Violation of DIP)

// Low-level module
class EmailService {
    void sendEmail(String message) {
        System.out.println("Email sent: " + message);
    }
}

// High-level module depends directly on EmailService
class Notification {
    private EmailService emailService = new EmailService();

    void notifyUser(String msg) {
        emailService.sendEmail(msg); // tightly coupled
    }
}

public class Main {
    public static void main(String[] args) {
        Notification notification = new Notification();
        notification.notifyUser("Hello DIP!");
    }
}

```
Problem: If tomorrow you want to send SMS or Push notifications, you must modify Notification class. This breaks the Open/Closed Principle and violates DIP.

```java
// Good Example (Applying DIP)
// Abstraction
interface MessageService {
    void sendMessage(String msg);
}

// Low-level modules
class EmailService implements MessageService {
    public void sendMessage(String msg) {
        System.out.println("Email sent: " + msg);
    }
}

class SMSService implements MessageService {
    public void sendMessage(String msg) {
        System.out.println("SMS sent: " + msg);
    }
}

// High-level module depends on abstraction
class Notification {
    private MessageService service;

    Notification(MessageService service) {
        this.service = service;
    }

    void notifyUser(String msg) {
        service.sendMessage(msg);
    }
}

public class Main {
    public static void main(String[] args) {
        MessageService email = new EmailService();
        MessageService sms = new SMSService();

        Notification notification1 = new Notification(email);
        notification1.notifyUser("Hello via Email!");

        Notification notification2 = new Notification(sms);
        notification2.notifyUser("Hello via SMS!");
    }
}

```