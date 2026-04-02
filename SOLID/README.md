# SOLID Principles – Interview Guide

A complete guide to understand, explain, and answer interview questions about SOLID principles with examples in TypeScript.

---

# 📌 What is SOLID?

SOLID is a set of 5 design principles that help you write:
- Clean code
- Maintainable systems
- Scalable architecture

They are mainly used in Object-Oriented Programming (OOP).

---

# 🧩 The 5 Principles

## 1. Single Responsibility Principle (SRP)

### 💡 Definition
A class should have only **one reason to change**.

### ❌ Bad Example
```ts
class UserService {
  saveUser() {}
  sendEmail() {}
}
```

### ✅ Good Example
```ts
class UserService {
  saveUser() {}
}

class EmailService {
  sendEmail() {}
}
```

### 🎯 Interview Answer
> SRP means each class should do only one job to make code easier to maintain and test.

---

## 2. Open/Closed Principle (OCP)

### 💡 Definition
Software should be:
- Open for extension
- Closed for modification

### ❌ Bad Example
```ts
class Discount {
  calculate(type: string) {
    if (type === "A") return 10;
    if (type === "B") return 20;
  }
}
```

### ✅ Good Example
```ts
interface DiscountStrategy {
  calculate(): number;
}

class DiscountA implements DiscountStrategy {
  calculate() { return 10; }
}

class DiscountB implements DiscountStrategy {
  calculate() { return 20; }
}
```

### 🎯 Interview Answer
> OCP allows adding new features without modifying existing code.

---

## 3. Liskov Substitution Principle (LSP)

### 💡 Definition
Subclasses should be replaceable with their base classes without breaking functionality.

### ❌ Bad Example
```ts
class Bird {
  fly() {}
}

class Penguin extends Bird {
  fly() {
    throw new Error("Cannot fly");
  }
}
```

### ✅ Good Example
```ts
interface Bird {}

interface FlyingBird {
  fly(): void;
}
```

### 🎯 Interview Answer
> LSP ensures inheritance is used correctly without breaking behavior.

---

## 4. Interface Segregation Principle (ISP)

### 💡 Definition
Clients should not be forced to depend on methods they do not use.

### ❌ Bad Example
```ts
interface Worker {
  work(): void;
  eat(): void;
}
```

### ✅ Good Example
```ts
interface Workable {
  work(): void;
}

interface Eatable {
  eat(): void;
}
```

### 🎯 Interview Answer
> ISP encourages smaller, focused interfaces.

---

## 5. Dependency Inversion Principle (DIP)

### 💡 Definition
High-level modules should not depend on low-level modules.
Both should depend on abstractions.

### ❌ Bad Example
```ts
class MySQLDatabase {
  connect() {}
}

class App {
  private db = new MySQLDatabase();
}
```

### ✅ Good Example
```ts
interface Database {
  connect(): void;
}

class MySQLDatabase implements Database {
  connect() {}
}

class App {
  constructor(private db: Database) {}
}
```

### 🎯 Interview Answer
> DIP reduces coupling by depending on interfaces instead of implementations.

---

# 🧠 Common Interview Questions

## 1. What is SOLID?
**Answer:**
A set of five principles used to design maintainable and scalable object-oriented systems.

---

## 2. Why is SOLID important?
**Answer:**
- Improves code readability
- Makes testing easier
- Reduces bugs
- Supports scalability

---

## 3. Difference between SRP and ISP?
**Answer:**
- SRP → concerns classes
- ISP → concerns interfaces

---

## 4. Which principle is most important?
**Answer:**
DIP is often considered the most important because it reduces coupling and improves flexibility.

---

## 5. Real-world example of SOLID?
**Answer:**
- Payment systems (multiple payment methods)
- Notification systems (Email, SMS)

---

# 🔥 Advanced Interview Tips

## ✅ When to use SOLID
- Large-scale applications
- Systems expected to grow

## ❌ When NOT to overuse
- Small projects
- Simple scripts

---

# 🚀 Pro Tips for Interviews

- Always give **examples**
- Mention **benefits (testability, flexibility)**
- Connect with **real-world scenarios**
- Use **TypeScript interfaces** to demonstrate understanding

---

# 📌 Summary

| Principle | Key Idea |
|----------|--------|
| SRP | One responsibility |
| OCP | Extend without modifying |
| LSP | Safe inheritance |
| ISP | Small interfaces |
| DIP | Depend on abstractions |

---

# 💬 Final Tip

If you understand SOLID deeply, you are not just writing code — you are designing systems.

