# 📘 POODR Chapter 3 – Managing Dependencies

## 🧠 TLDR

This chapter is about how to stop your classes from being too nosy. The fewer assumptions your class makes about the world around it, the easier it is to change. Dependencies should be explicit, isolated, and invertible. Don’t hardcode your collaborators — inject them, abstract them, and flip the direction of control.

## 💡 Key Concepts

- 🔗 Reduce tight coupling between classes
- 🧩 Depend on interfaces, not concrete implementations
- 💉 Inject dependencies instead of creating them inside the class
- 🧪 Loosely coupled classes are easier to test
- 🔁 Reverse dependency direction when it hurts

## 🧪 Code Pattern

```typescript
// ❌ Tightly coupled
class Report {
    private printer = new PDFPrinter(); // hardcoded dependency

    print() {
    this.printer.printReport();
    }
}

// ✅ Inject dependency via interface
interface Printer {
printReport(): void;
}

class Report {
    constructor(private printer: Printer) {}

    print() {
    this.printer.printReport();
    }
}
Now Report doesn’t care how the report gets printed — just that it does.
```

## 🧪 Mini Challenge

🎯 Build a NotificationService that can send messages via:

- 📧 Email
- 💬 Slack
- 📱 SMS

Requirements:

- Use interfaces for transports
- Inject the transport strategy without hardcoding any of them
- Bonus: Add a fake transport for test environments.

## 🔁 Refactor This

```typescript
// ❌ Before: tight coupling, not testable
class InvoiceService {
  emailSender = new SendGridClient();

  sendInvoice(data: InvoiceData) {
    this.emailSender.send(data);
  }
}

// ✅ After: interface-based + injected dependency
interface MessageSender {
  send(data: InvoiceData): void;
}

class InvoiceService {
  constructor(private sender: MessageSender) {}

  sendInvoice(data: InvoiceData) {
    this.sender.send(data);
  }
}
```

## 🤔 Reflection

Interesting way of looking at dependencies, other object has a behaviour that you need and you are collaborating with them to complete tasks.

For any desired behavior, an object either knows it personally, inherits it, or knows another object who knows it.

It's not the class of the object that’s important, it’s the message you plan to send to it.

## 🔖 Sticker Wisdom

> "Your class becomes less useful when it knows too much about other objects; if it knew less, it could do more."

> "Pretend for a moment that your classes are people. If you were to give them advice about how to behave, you would tell them to depend on things that change less often than you do."
