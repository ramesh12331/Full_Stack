# 📘 Chapter 10 — Node.js Events Module



Beginner to Advanced

Node.js

One Chapter at a Time



In this chapter, we will learn how Node.js handles events using the built-in `EventEmitter` class.

Topics covered:

1. Event-driven programming
2. EventEmitter
3. `.on()`
4. `.emit()`
5. `.once()`
6. `.off()`
7. Custom events
8. Event-driven architecture

## 1. What is it? 🤔

Event-driven programming is a programming approach where the execution of code depends on events.

An event is an action or occurrence that happens in a program.

Examples:

- A user clicks a button.
- A user logs into an application.
- A file finishes uploading.
- A payment is completed.
- A server receives a request.

In Node.js, we use the built-in `events` module to create and handle events.

The main class is called EventEmitter.

Simple definition:

> EventEmitter allows us to create events, listen for events, and execute callback functions when events occur.

## 2. Why do we need it? 🎯

Imagine you are developing an e-commerce application.

When a customer places an order, several actions must happen:

- Send an order confirmation email.
- Update product stock.
- Save order information.
- Send a notification.
- Update sales analytics.

Without an event-based approach, the order functionality might need to directly manage all these operations.

This can make the code tightly coupled and difficult to maintain.

With EventEmitter:

- The order system emits an `orderPlaced` event.
- Different listeners respond to that event.
- Each listener performs its own task.

Problem solved: Different parts of an application can respond to the same event without the event producer needing to manage every listener.

## 3. Real-world analogy 🛎️

Think about a doorbell.

[hand pressing on ringing bell near building entrance](https://images.openai.com/static-rsc-4/T7M21sdA7BmM-GsEPuV5RZ0MNVwRrVrpacP-fPVqIwKsMPiiTXfMLoSBU-zOPlDnTcagIzZIiI-XeO7OjJgScW4MF31uPG-woETOgYuoQT_Pk_frScYQO5oDZRH7sJJ1hOmelcNRVYrGg65rair9V1Mbb3RIPrOYma_M3M1IANj3VXPWDs83Zpnq9GoBLScQ?purpose=inline)

How does it work?

1. A visitor presses the doorbell.
2. The doorbell produces a sound.
3. People inside hear the sound.
4. Someone responds by opening the door.

Programming comparison:

| Doorbell                | Node.js                    |
| ----------------------- | -------------------------- |
| Doorbell button pressed | Event emitted              |
| Doorbell sound          | Event notification         |
| Person waiting          | Event listener             |
| Person responds         | Callback function executes |

Remember:

- `.on()` → Wait for an event.
- `.emit()` → Trigger an event.
- Callback → Execute when the event occurs.

## 4. Architecture / Flow 🏗️

Let's understand the basic EventEmitter flow.

1\. Create EventEmitter

new EventEmitter()

2\. Register Listener

emitter.on("eventName", callback)

3\. Emit Event

emitter.emit("eventName")

4\. Execute Callback

Listener callback runs

Flow: Create → Register → Emit → Execute.

## 5. Syntax 📝

### Step 1: Import EventEmitter

```
const EventEmitter = require("events");
```

### Step 2: Create an instance

```
const emitter = new EventEmitter();
```

### Step 3: Register an event listener

```
emitter.on("greet", () => {
    console.log("Hello!");
});
```

### Step 4: Emit the event

```
emitter.emit("greet");
```

Important: The `events` module is built into Node.js. You do not need to install it using npm.

## 6. Basic Example 💻

Create a file:

`events.js`

```
// Step 1: Import EventEmitter
const EventEmitter = require("events");

// Step 2: Create EventEmitter instance
const emitter = new EventEmitter();

// Step 3: Register an event listener
emitter.on("greet", () => {
    console.log("Hello Ramesh!");
});

// Step 4: Trigger the event
emitter.emit("greet");
```

## 7. Dry Run 🔍

Let's execute the program step by step.

| Step | Code                    | What happens?             |
| ---- | ----------------------- | ------------------------- |
| 1    | `require("events")`     | Imports EventEmitter      |
| 2    | `new EventEmitter()`    | Creates an emitter object |
| 3    | `on("greet", callback)` | Registers a listener      |
| 4    | `emit("greet")`         | Triggers the event        |
| 5    | Callback executes       | Prints the message        |

Understand this carefully:

When JavaScript reaches:

```
emitter.on("greet", () => {
    console.log("Hello Ramesh!");
});
```

The callback is registered. It does not execute immediately.

When JavaScript reaches:

```
emitter.emit("greet");
```

The registered callback executes.

## 8. Output 🖥️

```
Hello Ramesh!
```

Run in VS Code:

```
node events.js
```

## 9. Line-by-line explanation 📖

```
const EventEmitter = require("events");
```

Imports Node.js's built-in events module.

```
const emitter = new EventEmitter();
```

Creates an object that can manage events and listeners.

```
emitter.on("greet", () => {
    console.log("Hello Ramesh!");
});
```

Registers a callback function for the event named `greet`.

```
emitter.emit("greet");
```

Triggers the `greet` event and executes its registered listener.

Key difference:

- `on()` registers.
- `emit()` triggers.

## 10. Practical examples 🚀

Now let's understand each important EventEmitter method.

### A. `.on()` — Listen to an event

Definition: Registers a listener that executes whenever the specified event is emitted.

Syntax:

```
emitter.on("eventName", callback);
```

Example:

```
const EventEmitter = require("events");

const emitter = new EventEmitter();

// Register listener
emitter.on("login", () => {
    console.log("User logged in successfully!");
});

// Emit event
emitter.emit("login");
emitter.emit("login");
emitter.emit("login");
```

Output:

```
User logged in successfully!
User logged in successfully!
User logged in successfully!
```

Explanation: Every time `login` is emitted, the listener executes.

### B. `.emit()` — Trigger an event

Definition: Triggers an event and calls its registered listeners.

Syntax:

```
emitter.emit("eventName");
```

Example:

```
const EventEmitter = require("events");

const emitter = new EventEmitter();

emitter.on("payment", () => {
    console.log("Payment completed!");
});

// Trigger payment event
const result = emitter.emit("payment");

console.log("Event handled:", result);
```

Output:

```
Payment completed!
Event handled: true
```

`emit()` returns:

- `true` if at least one listener was called.
- `false` if no listener was registered.

### C. `.once()` — Execute only one time

Definition: Registers a listener that executes only once, then removes itself.

Syntax:

```
emitter.once("eventName", callback);
```

Example:

```
const EventEmitter = require("events");

const emitter = new EventEmitter();

emitter.once("welcome", () => {
    console.log("Welcome to our application!");
});

// Emit event multiple times
emitter.emit("welcome");
emitter.emit("welcome");
emitter.emit("welcome");
```

Output:

```
Welcome to our application!
```

Why only once?

After the first execution, Node.js automatically removes that listener.

### D. `.off()` — Remove an event listener

Definition: Removes a previously registered event listener.

Syntax:

```
emitter.off("eventName", listenerFunction);
```

Example:

```
const EventEmitter = require("events");

const emitter = new EventEmitter();

// Create a named function
function greet() {
    console.log("Hello!");
}

// Register listener
emitter.on("greet", greet);

// First event
emitter.emit("greet");

// Remove listener
emitter.off("greet", greet);

// Second event
emitter.emit("greet");

console.log("Listener removed!");
```

Output:

```
Hello!
Listener removed!
```

Notice that the second event does not print `Hello!`.

Important: `.off()` needs the same function reference that you originally registered.

### E. Custom Events 🛠️

Definition: Custom events are event names that we define according to our application requirements.

Examples:

- `userRegistered`
- `orderPlaced`
- `paymentCompleted`
- `fileUploaded`
- `messageReceived`

Example:

```
const EventEmitter = require("events");

const emitter = new EventEmitter();

// Register custom event
emitter.on("userRegistered", () => {
    console.log("New user registered!");
});

// Trigger custom event
emitter.emit("userRegistered");
```

Output:

```
New user registered!
```

### F. Passing data through custom events 📩

We can also pass data through `.emit()`.

```
const EventEmitter = require("events");

const emitter = new EventEmitter();

// Listen and receive data
emitter.on("userRegistered", (user) => {
    console.log("User ID:", user.id);
    console.log("Name:", user.name);
    console.log("Email:", user.email);
});

// Emit event with an object
emitter.emit("userRegistered", {
    id: 101,
    name: "Ramesh",
    email: "ramesh@example.com"
});
```

Output:

```
User ID: 101
Name: Ramesh
Email: ramesh@example.com
```

### G. Event-driven architecture 🏗️

Let's take an e-commerce application.

When a customer places an order, multiple components may need to respond.

[System Design in 2026: The Architecture Patterns Worth Drawing | Chamuka DrawIt](https://images.openai.com/static-rsc-4/cmAc_FbnBNP7B6wwf6d9AXR07Y8x2bbJg66W7zjUroTynXVACJ3si2cucfUz-N2ZUXuYLsN-ngv4IJM9jBrxGqbRxptAg0JTHEuy8gwixB_ufCTukX5tHf_msjbhG2TJ5XmUfWL3gVhh-vJyRu5T8ChaznHh8Veb39vpVX6Zcsw?purpose=inline)

[chamuka.ai](https://www.chamuka.ai/blog/system-design-2026?utm_source=chatgpt.com)

Architecture flow:

```
             Customer
                 |
                 v
           Order Service
                 |
                 v
       Emit "orderPlaced"
                 |
       +---------+---------+
       |         |         |
       v         v         v
   Notification Inventory Analytics
      Service    Service   Service
       |         |         |
       v         v         v
   Send Email Update Stock Record Sale
```

Example:

```
const EventEmitter = require("events");

const orderEmitter = new EventEmitter();

// Notification listener
orderEmitter.on("orderPlaced", (order) => {
    console.log(`Email sent for order ${order.id}`);
});

// Inventory listener
orderEmitter.on("orderPlaced", (order) => {
    console.log(`Stock updated for ${order.product}`);
});

// Analytics listener
orderEmitter.on("orderPlaced", (order) => {
    console.log(`Sales recorded: ${order.amount}`);
});

// Order data
const order = {
    id: 101,
    product: "Laptop",
    amount: 50000
};

// Emit order event
orderEmitter.emit("orderPlaced", order);
```

Output:

```
Email sent for order 101
Stock updated for Laptop
Sales recorded: 50000
```

Professional understanding: Node.js EventEmitter handles events inside the same Node.js process. For communication between separate applications or servers, systems commonly use message brokers such as RabbitMQ or Apache Kafka.

## 11. Common mistakes ⚠️

### Mistake 1: Emitting before registering

Wrong

```
emitter.emit("greet");

emitter.on("greet", () => {
    console.log("Hello!");
});
```

The listener misses the earlier event.

Correct

```
emitter.on("greet", () => {
    console.log("Hello!");
});

emitter.emit("greet");
```

### Mistake 2: Expecting `.once()` to run repeatedly

```
emitter.once("login", callback);

emitter.emit("login");
emitter.emit("login");
```

The listener runs only for the first emission.

Use `.on()` if the listener should execute every time.

### Mistake 3: Removing a different function reference

Wrong

```
emitter.on("greet", () => console.log("Hello"));

emitter.off("greet", () => console.log("Hello"));
```

These are two different function objects.

Correct

```
function greet() {
    console.log("Hello");
}

emitter.on("greet", greet);
emitter.off("greet", greet);
```

### Mistake 4: Forgetting the special error event

An emitted `error` event without a registered error listener throws an error.

Correct approach:

```
emitter.on("error", (error) => {
    console.error("Handled error:", error.message);
});
```

## 12. Best practices 🏆

1. Use meaningful event names such as `userRegistered` and `orderPlaced`.
2. Register listeners before emitting events.
3. Use `.once()` for one-time actions.
4. Use `.off()` when a listener is no longer needed.
5. Prefer named functions when you need to remove listeners.
6. Keep event handlers focused on one responsibility.
7. Handle the special `error` event where appropriate.
8. Avoid registering duplicate listeners unintentionally.
9. Avoid putting too much business logic inside one listener.
10. Remember that EventEmitter is synchronous by default; a long-running listener can delay other listeners.

## 13. Interview questions 🎤

### 🟢 Beginner

1\. What is event-driven programming?

It is a programming approach where code executes in response to events.

2\. What is EventEmitter?

It is a class provided by Node.js's built-in `events` module for creating and handling events.

3\. What is `.on()`?

It registers an event listener.

4\. What is `.emit()`?

It triggers an event.

5\. Is the events module built into Node.js?

Yes. No separate installation is required.

### 🟡 Intermediate

6\. Difference between `.on()` and `.once()`?

`.on()` executes on every matching emission. `.once()` executes only once.

7\. What is `.off()`?

It removes a previously registered listener.

8\. Can multiple listeners listen to the same event?

Yes. All registered listeners are normally called in registration order.

9\. Can we pass data through `.emit()`?

Yes. We can pass strings, numbers, objects, and other arguments.

10\. What does `.emit()` return?

A Boolean indicating whether at least one listener was called.

### 🔴 Advanced

11\. What is event-driven architecture?

An architecture where components communicate by producing and responding to events.

12\. Is EventEmitter asynchronous?

EventEmitter listeners are called synchronously by default. A listener can schedule asynchronous work, but that does not make the initial event dispatch asynchronous.

13\. What happens when an error event has no listener?

Node.js throws the error; the process may exit if it is not handled.

14\. What is the difference between EventEmitter and Kafka?

EventEmitter is an in-process event mechanism. Kafka is a distributed event-streaming platform that allows communication across applications and machines.

## 14. Practice problems 🏋️

Try these in VS Code.

Beginner

1. Create an EventEmitter instance.
2. Register a `greet` event.
3. Emit the `greet` event three times.
4. Create two listeners for the same event.
5. Create a `login` event using `.once()`.

Intermediate

6. Create a `studentRegistered` event and pass student details.
7. Remove a listener using `.off()`.
8. Create a `paymentCompleted` custom event.
9. Use `.emit()` and check its Boolean return value.
10. Register listeners for `orderPlaced`.

Advanced

11. Create an order system with notification, inventory, and analytics listeners.
12. Use `.once()` for the first order.
13. Remove the analytics listener after a specified operation.
14. Add an error listener and emit an error event.

## 15. Mini challenge 🚀

Your independent task

### Build a Student Registration Event Manager

Create a file named `student-events.js`.

Requirements:

1. Create an EventEmitter instance.
2. Register a custom event called `studentRegistered`.
3. Pass student ID, name, and course through `.emit()`.
4. Add three listeners:
   - Print a registration confirmation.
   - Print course information.
   - Print a welcome message.
5. Use `.once()` for a first-time welcome event.
6. Remove one listener using `.off()`.
7. Emit the event again and observe the output.

Expected output format:

```
Student registered successfully!
Student: Ramesh
Course: Node.js
Welcome to the course!
```

Try to write the code independently before looking at earlier examples.

## 16. Chapter summary ✅

| Topic                     | What you learned                      |
| ------------------------- | ------------------------------------- |
| Event-driven programming  | Code responds to events               |
| EventEmitter              | Creates and manages events            |
| `.on()`                   | Registers a listener                  |
| `.emit()`                 | Triggers an event                     |
| `.once()`                 | Executes a listener once              |
| `.off()`                  | Removes a listener                    |
| Custom events             | Application-defined events            |
| Event-driven architecture | Components communicate through events |

Main concept: EventEmitter allows different parts of a Node.js application to respond to events without directly depending on each other.

## 17. Quick revision ⚡

```
const EventEmitter = require("events");

// Create emitter
const emitter = new EventEmitter();

// Named listener
function greet(name) {
    console.log(`Hello ${name}!`);
}

// Register listener
emitter.on("greet", greet);

// Trigger event
emitter.emit("greet", "Ramesh");

// Register one-time listener
emitter.once("welcome", () => {
    console.log("Welcome!");
});

// Trigger one-time event
emitter.emit("welcome");

// Remove listener
emitter.off("greet", greet);
```

### Remember these four methods

| Method    | Meaning         |
| --------- | --------------- |
| `.on()`   | Listen          |
| `.emit()` | Trigger         |
| `.once()` | Listen once     |
| `.off()`  | Remove listener |

Chapter 10 lesson complete

STOP — Practise this chapter and solve the mini challenge.

Type NEXT when you are ready for Chapter 11 — Node.js URL Module