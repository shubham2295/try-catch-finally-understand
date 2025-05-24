# 📘 POODR Chapter 5 – Reducing Costs with Duck Typing

## 🧠 TLDR

This chapter is about polymorphism without inheritance — aka "if it walks like a duck..." You don’t need to share a class or interface to share behavior. What matters is that objects respond to the right messages. Duck typing enables flexible, interchangeable objects — and fewer rigid hierarchies.

## 💡 Key Concepts

- 🦆 Polymorphism ≠ inheritance — it’s about shared behavior
- 💬 Message-based design allows for loose coupling
- 🔍 Depend on the message, not the type
- 🤝 Don’t ask "what are you?" — ask "can you respond to this?"

## 🧪 Code Pattern

```typescript
interface TripParticipant {
  prepareTrip(): void;
}

class Mechanic {
  prepareTrip() {
    console.log("Tune the bikes");
  }
}

class TripCoordinator {
  prepareTrip() {
    console.log("Arrange logistics");
  }
}

class Trip {
  constructor(private participants: TripParticipant[]) {}

  prepare() {
    this.participants.forEach((p) => p.prepareTrip());
  }
}
// The Trip class doesn't care what a participant is, only that it responds to prepareTrip().
```

## 🧪 Mini Challenge

- 🎯 Find 2+ classes in your codebase that respond to similar messages
- 🔄 Replace conditional logic (if (obj.type === 'X')) with polymorphism
- 💡 Bonus: use a duck-type type guard to validate unknown input

## 🔁 Refactor This

```typescript
// ❌ Before: conditionals everywhere
class Trip {
  prepare(participant: any) {
    if (participant instanceof Mechanic) {
      participant.prepareTrip();
    } else if (participant instanceof TripCoordinator) {
      participant.prepareTrip();
    }
  }
}

// ✅ After: rely on shared behavior
class Trip {
  constructor(private participants: TripParticipant[]) {}

  prepare() {
    this.participants.forEach((p) => p.prepareTrip());
  }
}
```

## 🤔 Reflection

Interfaces are often seen as essential for ensuring safety, but this chapter highlights that message-based design can provide even greater safety and flexibility. It shifts the focus from type safety to design intent, emphasizing the importance of trusting objects to respond to the right messages.

## 🔖 Sticker Wisdom

"The ability to tolerate ambiguity about the class of an object is the hallmark of a confident designer"
"Flexible applications are built on objects that operate on trust; it is your job to make your objects trustworthy"
