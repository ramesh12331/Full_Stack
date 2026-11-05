# 🎯 Chapter 10 — Node.js Events Module

![Node.js](https://img.shields.io/badge/Node.js-Events%20Module-339933?style=for-the-badge&logo=node.js&logoColor=white)
![Level](https://img.shields.io/badge/Level-Beginner%20to%20Intermediate-blue?style=for-the-badge)

> Learn event-driven programming in Node.js using the built-in `EventEmitter` class.

---

## 📚 Table of Contents

- [1. Event-Driven Programming](#1--event-driven-programming)
- [2. EventEmitter](#2--eventemitter)
- [3. The `.on()` Method](#3--the-on-method)
- [4. The `.emit()` Method](#4--the-emit-method)
- [5. The `.once()` Method](#5--the-once-method)
- [6. The `.off()` Method](#6--the-off-method)
- [7. Custom Events](#7--custom-events)
- [8. Passing Data with Events](#8--passing-data-with-events)
- [9. Event-Driven Architecture](#9--event-driven-architecture)
- [10. Practical Example](#10--practical-example)
- [11. Important EventEmitter APIs](#11--important-eventemitter-apis)
- [12. Practice Exercises](#12--practice-exercises)
- [13. Interview Questions](#13--interview-questions)
- [14. Chapter Summary](#14--chapter-summary)

---

## 1. 🔄 Event-Driven Programming

**Event-driven programming** is a programming approach in which the flow of a program is controlled by events and the code that responds to those events.

An **event** is an action or occurrence that a program can detect.

### 🌍 Real-world examples

- A user clicks a button.
- A file finishes loading.
- A server receives a request.
- A database connection is established.
- A timer completes.

### 🛎️ Doorbell example

1. A visitor presses the doorbell button.
2. The doorbell produces a sound.
3. Someone inside hears the sound and responds.

| Real world | Programming |
|---|---|
| Pressing the doorbell | Emitting an event |
| Doorbell sound | Event notification |
| Person responding | Event listener / handler |

**Key idea:** A listener waits for an event. When that event is emitted, its callback function executes.

---

## 2. 📦 EventEmitter

Node.js provides a built-in `events` module. Its `EventEmitter` class lets us create, emit, and listen for custom events.

No package installation is required.

### Import EventEmitter

**CommonJS:**

```js
const EventEmitter = require("events");
```

**ES Modules:**

```js
import { EventEmitter } from "node:events";
```

### Create an EventEmitter instance

```js
const EventEmitter = require("events");

// Create an EventEmitter object
const emitter = new EventEmitter();

console.log("EventEmitter is ready!");
```

**Output:**

```text
EventEmitter is ready!
```

The `emitter` object can register listeners and emit events.

---

## 3. 👂 The `.on()` Method

The `.on()` method registers a listener for an event. Its callback runs whenever that event is emitted.

### Syntax

```js
emitter.on(eventName, callback);
```

### Example

Create `on-example.js`:

```js
const EventEmitter = require("events");

const emitter = new EventEmitter();

// Register a listener for the "greet" event
emitter.on("greet", () => {
    console.log("Hello! Welcome to Node.js Events.");
});

// Emit the event
emitter.emit("greet");
```

**Output:**

```text
Hello! Welcome to Node.js Events.
```

### 🔍 Execution flow

1. `new EventEmitter()` creates an event emitter.
2. `on("greet", callback)` registers a listener.
3. `emit("greet")` emits the event.
4. The registered callback executes.

**Remember:** Register the listener before emitting the event if you want it to receive that emission.

---

## 4. 📢 The `.emit()` Method

The `.emit()` method triggers an event. It calls the listeners currently registered for that event.

### Syntax

```js
emitter.emit(eventName, ...arguments);
```

### Example

```js
const EventEmitter = require("events");

const emitter = new EventEmitter();

emitter.on("welcome", () => {
    console.log("Welcome event received!");
});

// Trigger the event
const wasHandled = emitter.emit("welcome");

console.log("Was the event handled?", wasHandled);
```

**Output:**

```text
Welcome event received!
Was the event handled? true
```

`emit()` returns `true` if at least one listener was called, and `false` if no listener was registered for that event.

### Multiple listeners for the same event

```js
const EventEmitter = require("events");

const emitter = new EventEmitter();

emitter.on("message", () => {
    console.log("Listener 1 executed");
});

emitter.on("message", () => {
    console.log("Listener 2 executed");
});

emitter.emit("message");
```

**Output:**

```text
Listener 1 executed
Listener 2 executed
```

Listeners are normally called synchronously in registration order.

---

## 5. ☝️ The `.once()` Method

The `.once()` method registers a listener that runs only **one time** for that event. After it runs, it is automatically removed.

### Syntax

```js
emitter.once(eventName, callback);
```

### Example

```js
const EventEmitter = require("events");

const emitter = new EventEmitter();

// This listener executes only once
emitter.once("login", () => {
    console.log("User logged in!");
});

// Emit the same event three times
emitter.emit("login");
emitter.emit("login");
emitter.emit("login");
```

**Output:**

```text
User logged in!
```

### 💡 When is `.once()` useful?

- One-time initialization.
- First successful connection notification.
- Handling a one-time setup event.
- Running an action only on the first occurrence.

---

## 6. 🚫 The `.off()` Method

The `.off()` method removes a previously registered listener. It is an alias for `.removeListener()`.

To remove a listener, pass the **same function reference** that was registered.

### Syntax

```js
emitter.off(eventName, listener);
```

### Example

```js
const EventEmitter = require("events");

const emitter = new EventEmitter();

// Define a named listener
function greet() {
    console.log("Hello from the listener!");
}

// Register the listener
emitter.on("greet", greet);

// First emission: listener runs
emitter.emit("greet");

// Remove the exact listener function
emitter.off("greet", greet);

// Second emission: listener does not run
emitter.emit("greet");

console.log("Listener removed.");
```

**Output:**

```text
Hello from the listener!
Listener removed.
```

### ⚠️ Important: function reference

This will not remove the original listener:

```js
emitter.off("greet", () => {
    console.log("Hello from the listener!");
});
```

The arrow function above is a new function object. It is not the same function reference that was registered.

---

## 7. 🛠️ Custom Events

A **custom event** is an event name that you define for your application.

Examples: `userRegistered`, `orderPlaced`, `paymentCompleted`, `fileUploaded`, `notificationSent`.

### Example: User Registration Event

```js
const EventEmitter = require("events");

const emitter = new EventEmitter();

// Listen for a custom event
emitter.on("userRegistered", () => {
    console.log("A new user has registered!");
});

// Trigger the custom event
emitter.emit("userRegistered");
```

**Output:**

```text
A new user has registered!
```

---

## 8. 📩 Passing Data with Events

You can pass arguments to listeners through `emit()`. The listener callback receives those arguments.

### Example: Pass user information

```js
const EventEmitter = require("events");

const emitter = new EventEmitter();

// Receive data in the listener
emitter.on("userRegistered", (name, email) => {
    console.log("User Name:", name);
    console.log("User Email:", email);
});

// Pass values while emitting the event
emitter.emit("userRegistered", "Ramesh", "ramesh@example.com");
```

**Output:**

```text
User Name: Ramesh
User Email: ramesh@example.com
```

### Passing an object

```js
const EventEmitter = require("events");

const emitter = new EventEmitter();

emitter.on("orderPlaced", (order) => {
    console.log("Order ID:", order.id);
    console.log("Product:", order.product);
    console.log("Amount:", order.amount);
});

emitter.emit("orderPlaced", {
    id: 101,
    product: "Laptop",
    amount: 50000
});
```

**Output:**

```text
Order ID: 101
Product: Laptop
Amount: 50000
```

---

## 9. 🏗️ Event-Driven Architecture

**Event-driven architecture (EDA)** is a design approach in which application components communicate by producing and responding to events.

Instead of one component directly controlling every other component, a component can announce that something happened. Other components can listen and react.

### 🛒 E-commerce order example

When a customer places an order:

1. The order service creates an order.
2. It emits an `orderPlaced` event.
3. The notification handler sends a confirmation.
4. The inventory handler updates stock.
5. The analytics handler records the order.

### Event flow

```text
             Customer places order
                       |
                       v
                 Order Service
                       |
                       v
              Emit "orderPlaced"
                       |
          +------------+------------+
          |            |            |
          v            v            v
     Notification  Inventory    Analytics
       Handler      Handler      Handler
          |            |            |
          v            v            v
      Send email   Update stock  Record sale
```

### Node.js demonstration

```js
const EventEmitter = require("events");

const orderEmitter = new EventEmitter();

// Notification handler
orderEmitter.on("orderPlaced", (order) => {
    console.log(`Notification: Order ${order.id} confirmed.`);
});

// Inventory handler
orderEmitter.on("orderPlaced", (order) => {
    console.log(`Inventory: Updating stock for ${order.product}.`);
});

// Analytics handler
orderEmitter.on("orderPlaced", (order) => {
    console.log(`Analytics: Recorded order amount ${order.amount}.`);
});

// Order service emits the event
const order = {
    id: 501,
    product: "Laptop",
    amount: 50000
};

orderEmitter.emit("orderPlaced", order);
```

**Output:**

```text
Notification: Order 501 confirmed.
Inventory: Updating stock for Laptop.
Analytics: Recorded order amount 50000.
```

### ✅ Benefits

- Components can be loosely coupled.
- Multiple listeners can respond to one event.
- New event handlers can be added without changing the event producer.
- Application workflows can be easier to organize.

### ⚠️ Important distinction

Node.js `EventEmitter` is an **in-process** event mechanism. It is not automatically a distributed message broker. For communication between separate services or machines, systems may use tools such as RabbitMQ, Apache Kafka, or cloud messaging services.

---

## 10. 💻 Practical Example — User Activity Event Manager

Create a file named `user-events.js`.

```js
// Import Node.js EventEmitter
const EventEmitter = require("events");

// Create an event emitter instance
const userEvents = new EventEmitter();

// Listener 1: User login
function handleLogin(username) {
    console.log(`✅ ${username} logged in successfully.`);
}

// Listener 2: User logout
function handleLogout(username) {
    console.log(`👋 ${username} logged out.`);
}

// Register listeners
userEvents.on("login", handleLogin);
userEvents.on("logout", handleLogout);

// Register a one-time welcome listener
userEvents.once("firstLogin", (username) => {
    console.log(`🎉 Welcome for the first time, ${username}!`);
});

// Emit events
userEvents.emit("firstLogin", "Ramesh");
userEvents.emit("firstLogin", "Ramesh");

userEvents.emit("login", "Ramesh");
userEvents.emit("logout", "Ramesh");

// Remove login listener
userEvents.off("login", handleLogin);

// This login event has no listener now
userEvents.emit("login", "Ramesh");

console.log("Event demonstration completed.");
```

**Expected Output:**

```text
🎉 Welcome for the first time, Ramesh!
✅ Ramesh logged in successfully.
👋 Ramesh logged out.
Event demonstration completed.
```

### ▶️ Run the program

```bash
node user-events.js
```

No external package installation is necessary.

---

## 11. 🧠 Important EventEmitter APIs

| API | Purpose |
|---|---|
| `.on()` | Registers a listener |
| `.emit()` | Triggers an event |
| `.once()` | Registers a one-time listener |
| `.off()` | Removes a specific listener |
| `.removeListener()` | Removes a specific listener; alias of `.off()` |
| `.removeAllListeners()` | Removes all listeners, or all listeners for one event |
| `.listenerCount(eventName)` | Returns the number of listeners for an event |
| `.eventNames()` | Returns event names with registered listeners |
| `.setMaxListeners(n)` | Sets the maximum listener warning threshold |

### ⚠️ The special `error` event

If an `EventEmitter` emits the special `error` event and no `error` listener is registered, Node.js throws the error and the process may exit.

```js
const EventEmitter = require("events");

const emitter = new EventEmitter();

// Register an error listener
emitter.on("error", (error) => {
    console.error("Handled error:", error.message);
});

// Emit an error event
emitter.emit("error", new Error("Something went wrong"));
```

**Output:**

```text
Handled error: Something went wrong
```

---

## 12. 🏋️ Practice Exercises

### 🟢 Beginner Level

1. Import the `events` module.
2. Create an `EventEmitter` instance.
3. Register a `greet` event using `.on()`.
4. Trigger the event using `.emit()`.
5. Register two listeners for the same event.

### 🟡 Intermediate Level

1. Create a custom `studentRegistered` event.
2. Pass a student's name and course through `.emit()`.
3. Use `.once()` for a first-time welcome message.
4. Register a listener and remove it with `.off()`.
5. Compare the output before and after removing the listener.

### 🔴 Mini Project — Order Event Manager

Build a small order event manager with these requirements:

- Create an `EventEmitter` instance.
- Register an `orderPlaced` event.
- Pass order ID, product name, and amount.
- Add separate listeners for notification, inventory, and analytics.
- Register a one-time `firstOrder` event.
- Remove one listener using `.off()`.
- Print clear messages to follow the event flow.

---

## 13. 🎤 Interview Questions

1. What is event-driven programming?
2. What is an event in Node.js?
3. What is the `events` module?
4. What is `EventEmitter`?
5. What is the purpose of `.on()`?
6. What is the purpose of `.emit()`?
7. What is the difference between `.on()` and `.once()`?
8. How do you remove an event listener?
9. Why should you use a named function when removing a listener?
10. Can multiple listeners listen to the same event?
11. Can you pass arguments through `.emit()`?
12. What is event-driven architecture?
13. Is EventEmitter a distributed messaging system?
14. What happens when an `error` event is emitted without an error listener?

---

## 14. ✅ Chapter Summary

In this chapter, you learned:

- 🔄 Event-driven programming and its basic idea.
- 📦 The built-in Node.js `events` module.
- 👂 How to register listeners with `.on()`.
- 📢 How to trigger events with `.emit()`.
- ☝️ How to register one-time listeners with `.once()`.
- 🚫 How to remove listeners with `.off()`.
- 🛠️ How to create custom events.
- 📩 How to pass data through events.
- 🏗️ How event-driven architecture organizes application components.

### ⚡ Quick Revision

```js
const EventEmitter = require("events");
const emitter = new EventEmitter();

function greet(name) {
    console.log(`Hello, ${name}!`);
}

emitter.on("greet", greet);       // Listen
emitter.emit("greet", "Ramesh");  // Trigger
emitter.once("welcome", greet);   // Listen only once
emitter.off("greet", greet);      // Remove listener
```

---

**🎯 Next Chapter:** Chapter 11 — Node.js URL Module

Keep practising each example in VS Code before moving to the next chapter!
