# 📘 POODR Chapter 2 – Designing Classes with a Single Responsibility

## 🧠 TLDR
This chapter is all about the Single Responsibility Principle (SRP). A class should do one thing and do it well. When a class takes on too many roles, it becomes rigid and hard to change. SRP makes code easier to reuse, understand, and evolve.

## 💡 Key Concepts
- ✔️ Good design passes the TRUE(Transparent, Resusable, Usable, Exemplary) test
- 🧼 A class should represent a single concept or responsibility
- 🧩 Break large classes into smaller collaborators
- 📦 Don’t confuse grouping by data vs grouping by behavior
- 💥 Adding responsibilities = coupling = painful change
- ✅ The more focused the class, the easier it is to test

## 🧪 Code Pattern
```typescript
// SRP in action: Gear calculates gearing, Wheel calculates diameter. One job per class.
class Gear {
  constructor(
    private chainring: number,
    private cog: number,
    private wheel: Wheel
  ) {}

  ratio(): number {
    return this.chainring / this.cog;
  }

  gearInches(): number {
    return this.ratio() * this.wheel.diameter();
  }
}

class Wheel {
  constructor(private rim: number, private tire: number) {}

  diameter(): number {
    return this.rim + 2 * this.tire;
  }
}
```

## 🧪 Mini Challenge
- 🎯 Take a class in your current TypeScript project
- 🔍 Ask: “What’s your job?”
- ✅ If it does 2+ things, break it into smaller, focused classes

🔁 Refactor This
```typescript
// ❌ Before: mixed concerns
class Gear {
  constructor(
    private chainring: number,
    private cog: number,
    private rim: number,
    private tire: number
  ) {}

  diameter(): number {
    return this.rim + this.tire * 2;
  }

  gearInches(): number {
    return this.chainring / this.cog * this.diameter();
  }
}

// ✅ After: SRP FTW
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
```

## 🤔 Reflection
Just because it's related doesn't mean it belongs together. SRP isn't about minimalism — it’s about clarity.

## 🔖 Sticker Wisdom
“A class should do the smallest possible useful thing.”
