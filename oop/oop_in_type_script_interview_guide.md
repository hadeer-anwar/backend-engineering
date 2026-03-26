# OOP in TypeScript – Interview Questions Guide (Junior → Senior)

This README is a structured, in-depth guide to Object-Oriented Programming (OOP) in TypeScript, designed to help you prepare for interviews from **Junior to Senior level**.

---

# 📚 Table of Contents
1. Basics of OOP
2. TypeScript & OOP Fundamentals
3. Core OOP Principles
4. Intermediate Concepts
5. Advanced Concepts
6. System Design & Real Scenarios
7. Coding Challenges

---

# 🟢 1. Junior Level

## 🔹 Basic Questions

### 1. What is OOP?
**Answer:**
OOP (Object-Oriented Programming) is a programming paradigm based on objects, which contain data (properties) and behavior (methods).

---

### 2. What are the main principles of OOP?
- Encapsulation
- Inheritance
- Polymorphism
- Abstraction

---

### 3. What is a class in TypeScript?
```ts
class User {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  greet() {
    return `Hello ${this.name}`;
  }
}
```

---

### 4. What is an object?
Instance of a class.

```ts
const user = new User("Hadeer");
```

---

### 5. Access Modifiers
- public
- private
- protected

```ts
class Example {
  public a = 1;
  private b = 2;
  protected c = 3;
}
```

---

## 🔹 Important Follow-ups
- Difference between `type` and `interface`
- When to use class vs object literal

---

# 🟡 2. Mid-Level

## 🔹 Encapsulation

### What is it?
Hiding internal state and exposing controlled access.

```ts
class BankAccount {
  private balance: number = 0;

  deposit(amount: number) {
    this.balance += amount;
  }

  getBalance() {
    return this.balance;
  }
}
```

---

## 🔹 Inheritance

```ts
class Animal {
  move() {
    console.log("Moving");
  }
}

class Dog extends Animal {
  bark() {
    console.log("Bark");
  }
}
```

---

## 🔹 Polymorphism

```ts
class Shape {
  area(): number {
    return 0;
  }
}

class Circle extends Shape {
  area() {
    return Math.PI * 2 * 2;
  }
}
```

---

## 🔹 Abstraction

```ts
abstract class Payment {
  abstract pay(amount: number): void;
}

class CardPayment extends Payment {
  pay(amount: number) {
    console.log("Paid with card", amount);
  }
}
```

---

## 🔹 Interface vs Abstract Class

| Feature | Interface | Abstract Class |
|--------|----------|----------------|
| Implementation | ❌ | ✅ |
| Multiple inheritance | ✅ | ❌ |
| Use case | Contracts | Base logic |

---

## 🔹 Constructor Shortcuts

```ts
class User {
  constructor(public name: string, private age: number) {}
}
```

---

# 🔴 3. Senior Level

## 🔹 SOLID Principles

### 1. Single Responsibility
Each class should have one responsibility.

### 2. Open/Closed
Open for extension, closed for modification.

### 3. Liskov Substitution
Subclasses should replace base classes safely.

### 4. Interface Segregation
Avoid large interfaces.

### 5. Dependency Inversion
Depend on abstractions, not concrete classes.

---

## 🔹 Dependency Injection

```ts
class EmailService {
  send() {}
}

class UserService {
  constructor(private emailService: EmailService) {}
}
```

---

## 🔹 Composition vs Inheritance

Prefer composition:

```ts
class Engine {
  start() {}
}

class Car {
  constructor(private engine: Engine) {}
}
```

---

## 🔹 Design Patterns

### Singleton
```ts
class Config {
  private static instance: Config;

  private constructor() {}

  static getInstance() {
    if (!Config.instance) {
      Config.instance = new Config();
    }
    return Config.instance;
  }
}
```

---

### Factory
```ts
class UserFactory {
  static create(type: string) {
    if (type === "admin") return new Admin();
    return new Customer();
  }
}
```

---

### Strategy
```ts
interface PaymentStrategy {
  pay(amount: number): void;
}
```

---

## 🔹 Advanced TypeScript OOP

### Generics
```ts
class Repository<T> {
  private items: T[] = [];

  add(item: T) {
    this.items.push(item);
  }
}
```

---

### Mixins
```ts
type Constructor = new (...args: any[]) => {};

function Timestamped<TBase extends Constructor>(Base: TBase) {
  return class extends Base {
    createdAt = new Date();
  };
}
```

---

### Decorators (Important for NestJS)
```ts
function Log(target: any, key: string) {
  console.log(key);
}
```

---

# 🧠 4. System Design Questions

### 1. Design a School System
- Users (Student, Teacher, Admin)
- Courses
- Enrollment

👉 Focus on:
- Inheritance vs composition
- Role-based design
- Modular structure

---

### 2. Booking System
- Appointment
- Service
- Provider

👉 Focus on:
- Encapsulation
- Validation
- Scalability

---

### 3. Payment System
- Multiple payment methods

👉 Use:
- Strategy Pattern

---

# 💻 5. Coding Challenges

### 1. Implement a Logger with Singleton

### 2. Create a Generic Repository

### 3. Build Role-Based Access System

---

# 🎯 Tips for Interviews

- Always explain WHY, not just WHAT
- Prefer composition over inheritance
- Mention SOLID principles
- Show real-world examples
- Relate answers to systems (like SaaS or school system)

---

# 🚀 Final Advice

If you're aiming for senior level:
- Think in **architecture**, not just classes
- Focus on **scalability and maintainability**
- Connect OOP with **real backend systems (NestJS, Express)**

---

# 🎤 6. Real Interview Q&A Simulation

## 🟢 Junior Simulation

### Q1: What is the difference between class and interface?
**Answer:**
A class is used to create objects and can include implementation, while an interface defines a contract (shape) without implementation.

**Follow-up:** When would you use interface?
→ When defining DTOs, APIs, or enforcing structure across multiple classes.

---

### Q2: What is encapsulation?
**Answer:**
Encapsulation is restricting direct access to data and exposing it through methods.

**Example:**
```ts
class User {
  private password: string;

  setPassword(p: string) {
    this.password = p;
  }
}
```

---

## 🟡 Mid-Level Simulation

### Q3: Inheritance vs Composition?
**Answer:**
Inheritance creates tight coupling, while composition is more flexible and maintainable.

**Good Answer Tip:**
“I prefer composition because it reduces coupling and improves testability.”

---

### Q4: How do you apply OOP in a real backend system?
**Answer:**
- Use classes for services and entities
- Use interfaces for contracts
- Apply dependency injection

**Example (Service Layer):**
```ts
class AppointmentService {
  constructor(private repo: AppointmentRepo) {}
}
```

---

### Q5: What is polymorphism in TypeScript?
**Answer:**
Same method name, different behavior depending on the object.

---

## 🔴 Senior Simulation

### Q6: How do you design a scalable system using OOP?
**Strong Answer:**
- Follow SOLID principles
- Use dependency injection
- Separate concerns (controllers, services, repositories)
- Prefer composition over inheritance

---

### Q7: Explain Dependency Inversion with real example
**Answer:**
High-level modules should not depend on low-level modules.

```ts
interface EmailService {
  send(): void;
}

class GmailService implements EmailService {
  send() {}
}

class UserService {
  constructor(private emailService: EmailService) {}
}
```

---

### Q8: How would you design a multi-tenant SaaS system?
**Answer (Very Important for YOU 🔥):**
- Tenant isolation (DB or schema per tenant)
- Shared logic via services
- Role-based access
- Config-based features (plans/subscriptions)

---

### Q9: How do you avoid fat classes?
**Answer:**
- Apply Single Responsibility Principle
- Split logic into smaller services
- Use composition

---

## 💡 Bonus: Behavioral + Technical Mix

### Q10: Tell me about a challenge using OOP
**Strong Answer Structure:**
- Problem
- Your design decision
- Why OOP helped
- Result

---

# 🎯 How to Practice This

- Practice answering out loud
- Record yourself
- Focus on clarity + structure
- Always give real examples

---

Good luck 🚀

