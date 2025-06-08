# 📘 POODR Chapter 4 – Creating Flexible Interfaces

## 🧠 TLDR

This chapter emphasizes designing interfaces that reveal intent and minimize unnecessary dependencies. Interfaces aren’t about exposing all functionality — they’re about hiding implementation and focusing on what an object does, not how it does it.

## 💡 Key Concepts

- 🤝 Depend on what an object does, not how it works
- 💬 Trust messages over methods
- 🪞 Public interfaces reflect intent, private ones reflect implementation
- 🎭 Use interfaces to isolate behavior, reduce coupling, and clarify responsibilities
- 🙈 The Law of Demeter (LoD) is a design guideline for reducing coupling and improving code maintainability. It suggests that an object should only interact with:
  1. **Itself** – Call its own methods.
  2. **Its direct collaborators** – Call methods on objects it directly owns or has been passed.
  3. **Objects it creates** – Call methods on objects it instantiates.

## 🧪 Code Pattern

```typescript
interface Trip {
    prepare(): void;
}

class Mechanic {
    prepareTrip(): void {
    console.log('Tune the bike');
    }
}

class TripCoordinator {
    prepareTrip(): void {
    console.log('Arrange schedule');
    }
}

class TripPreparer {
    constructor(private services: Trip[]) {}

    prepareAll() {
        this.services.forEach(service => service.prepare());
    }
}
✨ Use abstract messages like prepare() to build flexible, message-driven design.
```

## 🧪 Mini Challenge

🎯 Rewrite a “manager” class so it no longer calls .someThing().otherThing().value.
✅ Use Demeter’s rule: “Only talk to immediate collaborators.”

🔁 Refactor This

```typescript
// ❌ Before
class Trip {
  mechanic: Mechanic;

  prepare() {
    this.mechanic.tools.clean();
  }
}

// ✅ After
class Mechanic {
  prepareTrip() {
    this.cleanTools();
  }
}

class Trip {
  constructor(private preparer: Mechanic) {}

  prepare() {
    this.preparer.prepareTrip();
  }
}
```

## 🤔 Reflection

This chapter reframed “interface” as communication, not just method names. Public messages = contract. Private methods = implementation detail.

## 🔖 Sticker Wisdom

> “Ask for what you want, not how to get it.”

> "Object oriented application is made up of classes but defined by messages"

> "Instead of deciding on a class and then figuring out its responsibilities, you are now deciding on a message and figuring out where to send it.
