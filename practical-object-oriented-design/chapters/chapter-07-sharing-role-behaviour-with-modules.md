# 📘 POODR Chapter 7 – Sharing Role Behavior with Modules

## 🧠 TLDR

This chapter introduces the idea of roles — shared behavior that doesn't require a class hierarchy. When multiple unrelated classes need the same functionality, use modules (or mixins) to share behavior without implying inheritance. Think “acts like,” not “is a.”

## 💡 Key Concepts

- 👯‍♂️ Different objects can play the same role
- 🧩 Use modules to compose behavior
- ❌ Inheritance implies type — modules imply capability
- 🎭 Roles make polymorphism flexible without coupling

## 🧪 Code Pattern

```typescript
// Role: Schedulable
interface Schedulable {
  isAvailable(time: Date): boolean;
}

class Mechanic implements Schedulable {
  isAvailable(time: Date): boolean {
    return true; // simplified
  }
}

class TripCoordinator implements Schedulable {
  isAvailable(time: Date): boolean {
    return false; // simplified
  }
}

// These classes share behavior via a contract, not inheritance. They “act schedulable,” but aren’t of the same type.
```

## 🧪 Mini Challenge

- 🎯 Think of 2+ classes that do similar things but aren't related
- ✅ Extract that behavior into a shared role interface
- 🔁 Optional: Add a factory that builds “role-players”

### 🔁 Refactor This

```typescript
// ❌ Before: Duplicate behavior across unrelated classes
class Mechanic {
  available(): boolean {
    return true;
  }
}

class Guide {
  available(): boolean {
    return true;
  }
}

// ✅ After: share a role contract
interface Schedulable {
  isAvailable(time: Date): boolean;
}
```

## 🤔 Reflection / Real Talk

Mixins or interfaces — serve as a way to share behavior across objects that play a common role. When an object includes behavior from elsewhere, it’s not just gaining methods — it’s entering into a design contract. That contract is governed by the Liskov Substitution Principle: if you act like something, you better be something.

Modules follow similar patterns as inheritance and should be designed with template methods and hook methods in mind, giving flexibility to the objects that include them. Rather than force subclasses or includers to know about super or implementation details, good modules make inclusion seamless. Shared behavior implies a shared responsibility — and that behavior must be predictable and intentional.

## 🔖 Sticker Wisdom

> “Every hierarchy can be thought of a pyramid that has both depth and breadth. An object’s depth is the number of superclasses between it and the top. Its breadth is the number of its direct subclasses.”
