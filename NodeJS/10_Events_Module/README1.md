# 📘 Chapter 10 — Node.js Events Module



PART 2 — Node.js Core Modules

Beginner to Advanced



In this chapter, we will learn how Node.js handles events and how different parts of an application communicate with each other using the Events Module.

## 🔑 Requires Before Starting

Before starting this chapter, you should understand:

1. JavaScript functions — How to create and call functions.
2. Arrow functions — How to write `() => {}`.
3. Objects — How to create and access object properties.
4. Node.js modules — How to import built-in modules using `require()`.
5. Basic JavaScript execution — How code executes line by line.

Example:

```
// Normal function
function greet() {
    console.log("Hello!");
}

// Calling the function
greet();
```

Expected output:

```
Hello!
```

## 1. What is it?

### What is an Event?

An event is an action or occurrence that happens in a program.

For example:

- A user registers.
- A user logs in.
- A button is clicked.
- A file is uploaded.
- An order is placed.
- A payment is completed.

When an event happens, we can execute a particular function.

### What is the Node.js Events Module?

Node.js provides a built-in module called `events`.

It allows us to create, listen to, and handle custom events in our applications.

We use a class called EventEmitter to work with events.

Example:

```
const EventEmitter = require("events");

// Create EventEmitter object
const event = new EventEmitter();

// Listen for an event
event.on("greet", () => {
    console.log("Hello! Welcome to Node.js");
});

// Trigger the event
event.emit("greet");
```

Expected output:

```
Hello! Welcome to Node.js
```

Here:

- `EventEmitter` — Class used to manage events.
- `event` — Object created from EventEmitter.
- `.on()` — Listens for an event.
- `.emit()` — Triggers an event.

## 2. Why do we need it?

Imagine you are building an online shopping application.

When a customer places an order, several actions must happen:

1. Save the order in the database.
2. Send an email to the customer.
3. Send a notification to the admin.
4. Update the order statistics.

Without event-driven programming, you might write all these operations inside one large function.

```
function placeOrder() {
    console.log("Order saved");

    console.log("Email sent");

    console.log("Admin notified");

    console.log("Statistics updated");
}
```

This can become difficult to maintain as your application grows.

Using events, we can separate these responsibilities.

```
function placeOrder() {
    console.log("Order placed");

    orderEvents.emit("orderPlaced");
}
```

Different listeners can respond to the same event.

```
orderEvents.on("orderPlaced", () => {
    console.log("Sending email...");
});

orderEvents.on("orderPlaced", () => {
    console.log("Notifying admin...");
});

orderEvents.on("orderPlaced", () => {
    console.log("Updating statistics...");
});
```

Main advantages:

- Separates different responsibilities.
- Makes code easier to maintain.
- Allows multiple functions to respond to one event.
- Reduces direct dependencies between different parts of an application.

## 3. Real-world analogy

Imagine a school bell. 🔔

When the bell rings:

- Students enter the classroom.
- Teachers start teaching.
- The office updates attendance.

The bell does not directly control every person's action.

It simply announces that an event has happened.

School bell example

Bell rings

Event: bellRings

Students

Enter class

Teachers

Start teaching

Office

Update records

In Node.js:

- Bell ringing = `.emit()`
- People listening = `.on()`
- Actions performed = Callback functions

## 4. Architecture / Flow

Let's understand how Node.js event handling works.

1\. Create EventEmitter

Create an event manager

2\. Register Listener

Use .on() to listen

3\. Trigger Event

Use .emit()

4\. Execute Listener

Registered callback function runs

Important: In this basic EventEmitter example, listeners execute synchronously in the order they were registered when `.emit()` is called.

## 5. Syntax

### Step 1: Import the Events Module

```
const EventEmitter = require("events");
```

### Step 2: Create an EventEmitter object

```
const event = new EventEmitter();
```

### Step 3: Register an event listener

```
event.on("eventName", () => {
    console.log("Event received");
});
```

### Step 4: Trigger the event

```
event.emit("eventName");
```

### Important EventEmitter methods

| Method              | Purpose                                |
| ------------------- | -------------------------------------- |
| `.on()`             | Register a listener                    |
| `.emit()`           | Trigger an event                       |
| `.once()`           | Execute listener only once             |
| `.off()`            | Remove a listener                      |
| `.removeListener()` | Remove a listener (alternative method) |
| `.listenerCount()`  | Count listeners for an event           |

## 6. Basic example

Let's create our first Node.js event program.

File: `app.js`

```
// Import events module
const EventEmitter = require("events");

// Create EventEmitter object
const event = new EventEmitter();

// Register listener
event.on("greet", () => {
    console.log("Hello Ramesh!");
});

// Trigger event
event.emit("greet");
```

Run in the VS Code terminal:

```
node app.js
```

## 7. Dry run

Let's execute the code step by step.

Code:

```
const EventEmitter = require("events");

const event = new EventEmitter();

event.on("greet", () => {
    console.log("Hello Ramesh!");
});

event.emit("greet");
```

| Step | Statement                | What happens?           |
| ---- | ------------------------ | ----------------------- |
| 1    | `require("events")`      | Imports Events Module   |
| 2    | `new EventEmitter()`     | Creates an event object |
| 3    | `event.on("greet", ...)` | Registers a listener    |
| 4    | `event.emit("greet")`    | Triggers the event      |
| 5    | `console.log()`          | Prints the message      |

Remember this flow:

```
Import Module
     ↓
Create Object
     ↓
Register Listener (.on)
     ↓
Trigger Event (.emit)
     ↓
Execute Callback
```

## 8. Output

When you execute:

```
node app.js
```

Expected output:

```
Hello Ramesh!
```

Why?

Because we registered a listener for the `greet` event and then triggered that event.

## 9. Line-by-line explanation

Let's understand every important line.

Line 1:

```
const EventEmitter = require("events");
```

- `require()` imports a module.
- `"events"` is a built-in Node.js module.
- `EventEmitter` is the class exported by that module.

Line 2:

```
const event = new EventEmitter();
```

- `new` creates an object.
- `event` is our EventEmitter object.
- We use this object to manage events.

Line 3:

```
event.on("greet", () => {
    console.log("Hello Ramesh!");
});
```

- `.on()` registers a listener.
- `"greet"` is the event name.
- `() => {}` is the callback function.
- The callback runs when the event is emitted.

Line 4:

```
event.emit("greet");
```

- `.emit()` triggers an event.
- The event name must match the listener's event name.
- The registered callback executes.

## 10. Practical example

### Example 1: Understanding `.on()`

`.on()` registers a listener that can execute every time the same event is triggered.

File: `on.js`

```
const EventEmitter = require("events");

const event = new EventEmitter();

// Register listener
event.on("login", () => {
    console.log("User logged in");
});

// Trigger the event three times
event.emit("login");
event.emit("login");
event.emit("login");
```

Output:

```
User logged in
User logged in
User logged in
```

Remember: `.on()` continues listening until the listener is removed or the EventEmitter is no longer used.

### Example 2: Understanding `.emit()`

`.emit()` triggers the event and can also pass data to listeners.

```
const EventEmitter = require("events");

const event = new EventEmitter();

// Register listener and receive data
event.on("user", (name) => {
    console.log(`Welcome ${name}`);
});

// Emit event with data
event.emit("user", "Ramesh");
event.emit("user", "Rahul");
```

Output:

```
Welcome Ramesh
Welcome Rahul
```

You can pass multiple arguments:

```
event.on("student", (name, age) => {
    console.log(`Name: ${name}`);
    console.log(`Age: ${age}`);
});

event.emit("student", "Ramesh", 25);
```

Output:

```
Name: Ramesh
Age: 25
```

### Example 3: Understanding `.once()`

`.once()` registers a listener that executes only one time.

```
const EventEmitter = require("events");

const event = new EventEmitter();

// Register one-time listener
event.once("welcome", () => {
    console.log("Welcome to Node.js!");
});

// Trigger three times
event.emit("welcome");
event.emit("welcome");
event.emit("welcome");
```

Output:

```
Welcome to Node.js!
```

Why only once?

Because `.once()` automatically removes its listener after the first execution.

### Example 4: Understanding `.off()`

`.off()` removes a previously registered event listener.

Important: You must use the same function reference that you used while registering the listener.

```
const EventEmitter = require("events");

const event = new EventEmitter();

// Create callback function
const welcome = () => {
    console.log("Welcome user");
};

// Register listener
event.on("login", welcome);

// Trigger event
event.emit("login");

// Remove listener
event.off("login", welcome);

// Trigger again
event.emit("login");
```

Output:

```
Welcome user
```

Dry run:

1. Register `welcome` as the login listener.
2. First `.emit()` executes `welcome`.
3. `.off()` removes the listener.
4. Second `.emit()` has no listener to execute.

### Example 5: Custom events

A custom event is an event name that we create according to our application requirements.

Examples:

- `userRegistered`
- `orderPlaced`
- `paymentCompleted`
- `fileUploaded`
- `userDeleted`

Let's create a custom event.

File: `customEvent.js`

```
const EventEmitter = require("events");

const event = new EventEmitter();

// Listen for custom event
event.on("orderPlaced", (orderId) => {
    console.log(`Order ${orderId} placed successfully`);
});

// Trigger custom event
event.emit("orderPlaced", 101);
```

Output:

```
Order 101 placed successfully
```

### Example 6: Event-driven architecture

Let's create a small user registration application.

When a user registers:

1. Display registration success.
2. Send a welcome email (simulated).
3. Notify the admin (simulated).

File: `userRegistration.js`

```
// Import Events Module
const EventEmitter = require("events");

// Create EventEmitter object
const userEvents = new EventEmitter();

// Listener 1: Send welcome email
userEvents.on("userRegistered", (user) => {
    console.log(`Welcome email sent to ${user.email}`);
});

// Listener 2: Notify admin
userEvents.on("userRegistered", (user) => {
    console.log(`Admin notified about ${user.name}`);
});

// Listener 3: Display notification
userEvents.on("userRegistered", (user) => {
    console.log("Registration notification created");
});

// Registration function
function registerUser(name, email) {

    // Create user object
    const user = {
        name: name,
        email: email
    };

    console.log("User registered successfully");

    // Trigger custom event
    userEvents.emit("userRegistered", user);
}

// Call registration function
registerUser("Ramesh", "ramesh@gmail.com");
```

Expected output:

```
User registered successfully
Welcome email sent to ramesh@gmail.com
Admin notified about Ramesh
Registration notification created
```

Understanding the architecture

registerUser()

User registration happens

emit("userRegistered", user)

Event is triggered with user data

Email

Send welcome email

Admin

Notify admin

Notification

Create notification

This is a simple example of event-driven architecture.

In a real application, email sending and notifications would use actual services. The example above only prints messages.

## 11. Common mistakes

### Mistake 1: Using different event names

Wrong

```
event.on("login", () => {
    console.log("User logged in");
});

event.emit("logout");
```

Output:

```
// No output
```

Why? The listener is registered for `login`, but we triggered `logout`.

Correct

```
event.on("login", () => {
    console.log("User logged in");
});

event.emit("login");
```

### Mistake 2: Calling `.off()` with a different function

Wrong

```
event.on("login", () => {
    console.log("User logged in");
});

event.off("login", () => {
    console.log("User logged in");
});
```

Why? These are two different function objects.

Correct

```
const login = () => {
    console.log("User logged in");
};

event.on("login", login);

event.off("login", login);
```

### Mistake 3: Expecting `.once()` to execute multiple times

```
event.once("welcome", () => {
    console.log("Welcome");
});

event.emit("welcome");
event.emit("welcome");
```

Output:

```
Welcome
```

Remember: `.once()` executes only once.

### Mistake 4: Emitting an error event without a listener

In Node.js, the event named `error` has special behavior.

```
event.emit("error", new Error("Something went wrong"));
```

If an `error` event is emitted without a registered `error` listener, Node.js throws the error.

A safer example:

```
event.on("error", (err) => {
    console.log("Error handled:", err.message);
});

event.emit("error", new Error("Database failed"));
```

Output:

```
Error handled: Database failed
```

## 12. Best practices

When using EventEmitter in professional Node.js applications:

1. Use meaningful event names.

   Good: `userRegistered`, `orderPlaced`, `paymentCompleted`.
2. Use reusable callback functions.

   This makes removing listeners easier.
3. Remove unnecessary listeners.

   Use `.off()` when a listener is no longer needed.
4. Handle errors carefully.

   Register an `error` listener when your event flow can emit errors.
5. Avoid too many listeners on one event.

   Node.js gives a warning when an EventEmitter exceeds its default maximum of 10 listeners for one event. This is a warning, not a hard limit.
6. Keep event responsibilities separate.

   Email handling, notifications, and logging should have separate responsibilities.
7. Do not confuse events with asynchronous execution.

   Normal EventEmitter listeners execute synchronously. If a listener performs asynchronous work, handle its Promise or callback appropriately.
8. Use events where they improve code organization.

   Not every function call needs an event.

## 13. Interview questions

### 🟢 Beginner level

Q1. What is an event in Node.js?

An event is an action or occurrence that happens in an application, such as user login, order placement, or file upload.

Q2. What is the Events Module?

It is a built-in Node.js module used to create and manage events.

Q3. What is EventEmitter?

EventEmitter is a class provided by the Events Module. It allows us to register listeners and trigger events.

Q4. What is `.on()`?

`.on()` registers a listener for an event.

Q5. What is `.emit()`?

`.emit()` triggers an event and executes its registered listeners.

### 🟡 Intermediate level

Q6. What is the difference between `.on()` and `.once()`?

| `.on()`                     | `.once()`                           |
| --------------------------- | ----------------------------------- |
| Can execute multiple times  | Executes only once                  |
| Listener remains registered | Listener is removed after execution |
| Used for repeated events    | Used for one-time events            |

Q7. What is `.off()`?

`.off()` removes a registered event listener. It requires the original function reference.

Q8. Can we pass data through events?

Yes. We can pass arguments through `.emit()`.

```
event.emit("user", "Ramesh", 25);
```

Q9. Can multiple listeners listen to the same event?

Yes. All registered listeners for that event are executed when it is emitted.

Q10. What is a custom event?

A custom event is an event created by the developer according to application requirements.

### 🔴 Advanced level

Q11. What is event-driven architecture?

It is an architecture in which different parts of an application communicate by producing and responding to events.

Q12. Are EventEmitter listeners asynchronous?

No. Normal EventEmitter listeners execute synchronously in registration order. A listener can start asynchronous work, but that does not make the event dispatch itself asynchronous.

Q13. What happens if we emit an event without registering a listener?

Usually nothing happens. The event is emitted, but there is no listener to execute. The special `error` event is an exception.

Q14. What is the difference between events and callbacks?

A callback is a function passed to another function. EventEmitter provides a system where listeners register for named events and execute when those events are emitted.

Q15. What is a memory leak warning in EventEmitter?

It can appear when too many listeners are registered for one event. It may indicate that listeners are not being removed correctly.

## 14. Practice problems

Try these exercises yourself.

Exercise 1 — Welcome Event

Create an event named `welcome`.

Requirements:

- Register a listener.
- Print `Welcome to Node.js`.
- Trigger the event.

Exercise 2 — Login Event

Create a login event.

Requirements:

- Pass a username through `.emit()`.
- Display the username inside the listener.

Example output:

```
Ramesh logged in successfully
```

Exercise 3 — Once Event

Create an event named `payment`.

Requirements:

- Use `.once()`.
- Trigger the event three times.
- Print `Payment completed` only once.

Exercise 4 — Remove Listener

Requirements:

- Create a callback function.
- Register it using `.on()`.
- Trigger the event.
- Remove the listener using `.off()`.
- Trigger the event again.

Exercise 5 — Multiple Listeners

Create an event named `orderPlaced`.

Requirements:

- First listener: print `Order saved`.
- Second listener: print `Email sent`.
- Third listener: print `Admin notified`.
- Trigger the event once.

## 15. Mini challenge 🏆

Independent coding challenge

### Build a User Registration Event System

Requirement:

Create a Node.js program using EventEmitter.

When a user registers, perform these operations:

1. Display user registration success.
2. Display welcome email sent.
3. Display admin notification.
4. Display user registration log.

Input:

```
registerUser("Ramesh", "ramesh@gmail.com");
```

Expected output:

```
User registered successfully

Welcome email sent to ramesh@gmail.com

Admin notified about Ramesh

User registration logged
```

### Your task

Try writing the code yourself before looking at the solution.

Hints:

- Import `events`.
- Create an EventEmitter object.
- Register three or four listeners.
- Create a `registerUser()` function.
- Trigger a custom event from that function.
- Pass the user object through `.emit()`.

## 16. Chapter summary

| Topic                     | What you learned                         |
| ------------------------- | ---------------------------------------- |
| Event                     | An action or occurrence in a program     |
| Events Module             | Built-in Node.js module                  |
| EventEmitter              | Class used to manage events              |
| `.on()`                   | Register an event listener               |
| `.emit()`                 | Trigger an event                         |
| `.once()`                 | Execute listener only once               |
| `.off()`                  | Remove an event listener                 |
| Custom events             | Developer-created events                 |
| Event-driven architecture | Application components respond to events |

Main concept:

```
EventEmitter
     |
     |-- .on()       → Listen
     |
     |-- .emit()     → Trigger
     |
     |-- .once()     → Listen once
     |
     |-- .off()      → Remove listener
```

## 17. Quick revision

Remember these five important methods

| Method             | Easy meaning    |
| ------------------ | --------------- |
| `.on()`            | Listen          |
| `.emit()`          | Trigger         |
| `.once()`          | Listen once     |
| `.off()`           | Remove          |
| `.listenerCount()` | Count listeners |

Basic syntax to remember:

```
const EventEmitter = require("events");

const event = new EventEmitter();

event.on("hello", () => {
    console.log("Hello Node.js");
});

event.emit("hello");
```

Chapter 10 completed

Important: `.on()` registers a listener; `.emit()` triggers it. Normal listeners execute synchronously.

Practice the examples and exercises before moving forward. I'll wait for your `NEXT` before starting Chapter 11 — Synchronous vs Asynchronous.