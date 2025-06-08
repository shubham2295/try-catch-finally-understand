# 📘 POODR Chapter 6 – Acquiring Behavior through Inheritance

## 🧠 TLDR

Inheritance can help you share behavior and reduce duplication, but only when used wisely. This chapter explores when inheritance is appropriate — and warns against blindly relying on it. Favor behavioral similarity over structural convenience.

## 💡 Key Concepts

🧬 Inheritance means "is-a" but also "acts-like"
🔁 Overuse leads to rigid, tangled class hierarchies
🧠 Prefer composition when behavior varies
🧪 Use abstract base classes to enforce shared interfaces

## 🧪 Code Pattern

```typescript
abstract class Bicycle {
  constructor(protected size: string) {}

  abstract defaultTireSize(): string;

  specs(): string {
    return `Size: ${this.size}, Tire: ${this.defaultTireSize()}`;
  }
}

class RoadBike extends Bicycle {
  defaultTireSize(): string {
    return "23C";
  }
}

//Behavior is reused via inheritance, but only when it makes semantic sense.
```

## 🧪 Mini Challenge

🎯 Find two classes with overlapping behavior
🔍 Does one conceptually “inherit” from the other, or should they compose?
🧪 Bonus: Write a shared abstract class and extend both

## 🔁 Refactor This

```typescript
// ❌ Before: duplicate logic
class RoadBike {
  constructor(private size: string) {}

  specs() {
    return `Size: ${this.size}, Tire: 23C`;
  }
}

class MountainBike {
  constructor(private size: string) {}

  specs() {
    return `Size: ${this.size}, Tire: 2.1"`;
  }
}

// ✅ After: share via inheritance
abstract class Bicycle {
  constructor(protected size: string) {}
  abstract defaultTireSize(): string;
  specs() {
    return `Size: ${this.size}, Tire: ${this.defaultTireSize()}`;
  }
}
```

## 🤔 Reflection

When a concrete class almost fits the needs, it's tempting to just tweak it—but that can lead to messy code. Inheritance is a better fit for related types that share behavior but vary in specific ways. It allows message delegation to a parent class, making reuse clean. Patterns like template method demand clear responsibility from subclasses, ensuring they fully implement required behavior.

## 🔖 Sticker Wisdom

> "Creating a hierarchy has costs; the best way to minimize these costs is to maximize your chance of getting the abstraction right before allowing subclasses to depend on it."

> "The general rule for refactoring into a new inheritance hierarchy is to arrange code so that you can promote abstractions rather than demote concretions."
