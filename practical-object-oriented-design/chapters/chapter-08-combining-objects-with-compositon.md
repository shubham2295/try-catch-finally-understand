# 📘 POODR Chapter 8 – Combining Objects with Composition

## 🧠 TLDR

Inheritance isn’t the only way to share behavior — and often it’s the wrong one. This chapter explores composition: building objects out of other objects. It’s flexible, testable, and avoids the rigidity of class hierarchies.

## 💡 Key Concepts

- ⚙️ Composition means “has-a” vs inheritance’s “is-a”
- 🛠️ Delegation allows objects to collaborate
- 🧩 Create objects from smaller parts that each do one job well
- 🧪 Composition is preferred by default when flexibility is key

## 🧪 Code Pattern

```typescript
class Wheel {
  constructor(private rim: number, private tire: number) {}

  diameter(): number {
    return this.rim + this.tire * 2;
  }
}

class Gear {
  constructor(
    private chainring: number,
    private cog: number,
    private wheel: Wheel
  ) {}

  gearInches(): number {
    return (this.chainring / this.cog) * this.wheel.diameter();
  }
}

//Gear uses Wheel, but doesn't inherit from it. This is true delegation via composition.
```

## 🧪 Mini Challenge

- 🎯 Refactor a class with multiple responsibilities into a main object + collaborators
- 🧩 Ask: Can each collaborator be reused independently?
- ✅ Optional: use compose() to experiment with behavior assembly

## 🔁 Refactor This

```typescript
// ❌ Before: one class does everything
class Bike {
  ride() {}
  tune() {}
  report() {}
}

// ✅ After: composed object
class Bike {
  constructor(private mechanic: Mechanic, private tracker: RideTracker) {}

  ride() {
    this.tracker.track();
  }

  maintain() {
    this.mechanic.tune();
  }
}
```

## 🤔 Reflection / Real Talk

Composition, inheritance, and behavior sharing via modules are all tools — not ideologies. Each approach has its strengths and tradeoffs, and mastering them requires experimentation and practice, not dogma. While composed objects are often simple and modular, their combinations can create complex systems that aren’t always easy to reason about.

Design skill comes from making and learning from mistakes, not avoiding them. The key is to stay flexible, detach from past decisions, and refactor without fear.

## 🔖 Sticker Wisdom

> “Aggregation is exactly like composition except that the contained object has an independent life.”

> "Inheritance for the cost of arranging objects in a hierarchy, you get message delegation for free."

> "Prefer composition over inheritance — every time you can.”
