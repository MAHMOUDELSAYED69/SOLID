![image](https://github.com/user-attachments/assets/a374c352-5801-48f2-b569-8b2c40e72f9b)

# SOLID Principles in Dart

This repository demonstrates the application of SOLID principles in Dart, focusing on object-oriented programming practices. The SOLID principles are a set of design guidelines that aim to make software designs more understandable, flexible, and maintainable.

## Table of Contents

- [Introduction](#introduction)
- [Single Responsibility Principle (SRP)](#single-responsibility-principle-srp)
- [Open/Closed Principle (OCP)](#openclosed-principle-ocp)
- [Liskov Substitution Principle (LSP)](#liskov-substitution-principle-lsp)
- [Interface Segregation Principle (ISP)](#interface-segregation-principle-isp)
- [Dependency Inversion Principle (DIP)](#dependency-inversion-principle-dip)
- [Conclusion](#conclusion)

## Introduction

SOLID is an acronym that stands for five design principles intended to improve software design and reduce the risk of software rot. The principles are:

1. **S**ingle Responsibility Principle (SRP)
2. **O**pen/Closed Principle (OCP)
3. **L**iskov Substitution Principle (LSP)
4. **I**nterface Segregation Principle (ISP)
5. **D**ependency Inversion Principle (DIP)

By following these principles, developers can create systems that are easier to manage, scale, and understand.

## Single Responsibility Principle (SRP)

The **Single Responsibility Principle** states that a class should have only one reason to change, meaning it should have only one job or responsibility. This principle promotes the idea that a class should encapsulate only one part of the functionality provided by the software.

### Benefits of SRP
- **Improved maintainability:** Changes in requirements can be implemented in a single class without affecting others.
- **Enhanced readability:** Smaller classes with focused responsibilities are easier to understand.
- **Easier testing:** Classes with single responsibilities are easier to test in isolation.

### Bad Example (Violating SRP)

```dart
class User {
  void save() {
    // Save user to database
  }
  
  void sendEmail() {
    // Send email to user
  }
}
```

### Good Example (Following SRP)

```dart
class User {
  void save() {
    // Save user to database
  }
}

class EmailService {
  void sendEmail() {
    // Send email to user
  }
}
```

## Open/Closed Principle (OCP)

The **Open/Closed Principle** states that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. This principle encourages developers to write code that can be extended with new features without changing existing code.

### Benefits of OCP
- **Reduced risk of bugs:** Existing code remains unchanged, minimizing the chance of introducing new bugs.
- **Easier to add new features:** New functionality can be added through inheritance or composition.

### Bad Example (Violating OCP)

```dart
class Shape {
  String type;
  
  double calculateArea() {
    throw "Unsupported operation";
  }
}
```

### Good Example (Following OCP)

```dart
abstract class Shape {
  double calculateArea();
}

class Circle extends Shape {
  double radius;
  
  @override
  double calculateArea() {
    return 3.14 * radius * radius;
  }
}

class Rectangle extends Shape {
  double width;
  double height;
  
  @override
  double calculateArea() {
    return width * height;
  }
}
```

## Liskov Substitution Principle (LSP)

The **Liskov Substitution Principle** states that objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program. This principle ensures that a subclass can stand in for its superclass without issues.

### Benefits of LSP
- **Improved code reusability:** Subtypes can be used interchangeably with their base types.
- **Enhanced maintainability:** Following LSP leads to a more predictable codebase.

### Bad Example (Violating LSP)

```dart
class Rectangle {
  double width;
  double height;
}

class Square extends Rectangle {
  @override
  set width(double value) {
    super.width = value;
    super.height = value;
  }
  
  @override
  set height(double value) {
    super.width = value;
    super.height = value;
  }
}
```

### Good Example (Following LSP)

```dart
abstract class Shape {
  double area();
}

class Rectangle implements Shape {
  double width;
  double height;
  
  @override
  double area() {
    return width * height;
  }
}

class Square implements Shape {
  double side;
  
  @override
  double area() {
    return side * side;
  }
}
```

## Interface Segregation Principle (ISP)

The **Interface Segregation Principle** states that no client should be forced to depend on methods it does not use. This principle encourages developers to create smaller, more specific interfaces rather than large, general-purpose ones.

### Benefits of ISP
- **Reduced dependencies:** Clients only depend on what they use, leading to fewer changes.
- **Enhanced flexibility:** Specific interfaces can be changed without affecting other parts of the code.

### Bad Example (Violating ISP)

```dart
abstract class Worker {
  void work();
  void eat();
}

class Engineer implements Worker {
  @override
  void work() {
    // Engineer specific work
  }
  
  @override
  void eat() {
    // Engineer specific eating habits
  }
}
```

### Good Example (Following ISP)

```dart
abstract class Worker {
  void work();
}

abstract class Eater {
  void eat();
}

class Engineer implements Worker, Eater {
  @override
  void work() {
    // Engineer specific work
  }
  
  @override
  void eat() {
    // Engineer specific eating habits
  }
}
```

## Dependency Inversion Principle (DIP)

The **Dependency Inversion Principle** states that high-level modules should not depend on low-level modules, but both should depend on abstractions. This principle promotes the use of interfaces or abstract classes to decouple dependencies.

### Benefits of DIP
- **Increased flexibility:** High-level modules can be changed independently of low-level modules.
- **Improved testability:** Dependencies can be mocked or stubbed in unit tests.

### Bad Example (Violating DIP)

```dart
class UserService {
  final Database database;
  
  UserService() {
    this.database = Database();
  }
  
  void saveUser(User user) {
    database.save(user);
  }
}

class Database {
  void save(User user) {
    // Save user to database
  }
}
```

### Good Example (Following DIP)

```dart
abstract class UserRepository {
  void save(User user);
}

class DatabaseRepository implements UserRepository {
  @override
  void save(User user) {
    // Save user to database
  }
}

class UserService {
  final UserRepository userRepository;
  
  UserService(this.userRepository);
  
  void saveUser(User user) {
    userRepository.save(user);
  }
}
```

## Conclusion

By adhering to SOLID principles, Dart developers can create more flexible, maintainable, and scalable applications. Each principle contributes to code that is easier to understand, extend, and refactor. Implementing these principles not only enhances the quality of the software but also improves collaboration and reduces the cost of changes in the long run.

