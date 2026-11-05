# ⚡ Chapter 9 — Node.js `events` Module

In this chapter, we will learn how Node.js handles events using the built-in `events` module.

We will cover `EventEmitter`, creating custom events, `.on()`, `.emit()`, `.once()`, `.removeListener()`, and event-driven architecture with practical examples.

## 🔑 Requires Before Starting

Before starting Chapter 9, make sure you understand these topics:

1. JavaScript Functions — Creating and calling functions.
2. Arrow Functions — Writing functions using `() => {}`.
3. Objects — Creating and accessing object properties.
4. Node.js Basics — Running JavaScript files using `node app.js`.
5. Modules — Importing built-in modules using `require()`.
6. Callbacks — Passing a function as an argument to another function.

Previous chapters required:

- Chapter 5 — Node.js Modules
- Chapter 6 — Node.js `path` Module
- Chapter 7 — Node.js `fs` Module
- Chapter 8 — Node.js `os` Module

# 1️⃣ Introduction to Events Module

## 1.1 What is an Event?

An event is an action or occurrence that happens in an application.

For example:

- A user registers an account.
- A customer places an order.
- A file finishes downloading.
- A payment is completed.
- A server receives a request.

Whenever something happens in an application, we can call it an event.

### Real-world example

Imagine a doorbell.

[Doorbell cartoon Vector Images & Graphics for Commercial Use | VectorStock](https://images.openai.com/static-rsc-4/LIrEOvA3i1n_1D3C2gi8n-8MSdylhonoKBTrPZzl0uCJAhD8lUExHwMHO2fQKzrJT-5A7tojLhRlHrYbP-d3Sl0MhuV8rN0H0iQ0TJ08oZK-f8nqzC3dgP0U-r9ur4KX-xslJK6pjDfdg5t3xN9dUpkW3H0kQpk1IMXJv3bPUPQ?purpose=inline)

1. A person presses the doorbell.
2. The doorbell detects the action.
3. The bell produces a sound.

Here:

| Real-world action   | Node.js concept            |
| ------------------- | -------------------------- |
| Pressing doorbell   | Event occurs               |
| Doorbell waiting    | Event listener             |
| Pressing the button | Emit event                 |
| Bell ringing        | Callback function executes |

## 1.2 What is the Node.js Events Module?

The Node.js `events` module is a built-in module that allows us to create, listen for, and trigger events.

It helps different parts of an application respond when something happens.

Syntax:

```
const EventEmitter = require("events");
```

No separate npm installation is required because `events` is a built-in Node.js module.

## 1.3 Why Do We Need the Events Module?

Imagine an online shopping application.

When a customer places an order, we may need to:

1. Create the order.
2. Send a confirmation email.
3. Update product stock.
4. Send a notification.

Without events, we might put all these operations directly inside one function.

Using events, we can separate these operations into different listeners.

This makes our code easier to organize and maintain.

# 2️⃣ What is EventEmitter?

## 2.1 Definition

`EventEmitter` is a class provided by the Node.js `events` module.

It allows us to create custom events and execute functions when those events occur.

Basic syntax:

```
const EventEmitter = require("events");

// Create EventEmitter object
const event = new EventEmitter();
```

### Understand the code

| Code                 | Explanation                     |
| -------------------- | ------------------------------- |
| `require("events")`  | Imports the events module       |
| `EventEmitter`       | Receives the EventEmitter class |
| `new EventEmitter()` | Creates a new event object      |
| `event`              | Our EventEmitter object         |

## 2.2 What is an Event Listener?

An event listener is a function that waits for a particular event.

When that event is triggered, the listener function executes.

Example:

```
const EventEmitter = require("events");

const event = new EventEmitter();

// Register an event listener
event.on("welcome", () => {
    console.log("Welcome to Node.js");
});
```

Output:

```
No output
```

Why?

Because we registered the listener but did not trigger the event.

Remember: `on()` registers a listener. It does not trigger it.

# 3️⃣ `.on()` Method

## 3.1 What is `.on()`?

The `.on()` method is used to listen for an event.

When the specified event occurs, the registered callback function executes.

Syntax:

```
event.on("eventName", callbackFunction);
```

### Example

```
const EventEmitter = require("events");

const event = new EventEmitter();

// Listen for welcome event
event.on("welcome", () => {
    console.log("Hello Ramesh!");
});
```

At this stage, the listener is registered but has not executed.

## 3.2 Important Points

- `.on()` registers an event listener.
- We can register multiple listeners.
- The listener waits until its event is triggered.
- The same listener can execute multiple times when the event is emitted multiple times.

# 4️⃣ `.emit()` Method

## 4.1 What is `.emit()`?

The `.emit()` method is used to trigger an event.

When we trigger an event, its registered listeners execute.

Syntax:

```
event.emit("eventName");
```

### Example

```
const EventEmitter = require("events");

const event = new EventEmitter();

// Register listener
event.on("welcome", () => {
    console.log("Hello Ramesh!");
});

// Trigger event
event.emit("welcome");
```

Output:

```
Hello Ramesh!
```

## 4.2 Dry Run

| Step | Code                 | Explanation          |
| ---- | -------------------- | -------------------- |
| 1    | `new EventEmitter()` | Creates event object |
| 2    | `event.on()`         | Registers listener   |
| 3    | `event.emit()`       | Triggers event       |
| 4    | `console.log()`      | Prints message       |

### Visual Flow

Create EventEmitter

Register Listener — `on()`

Trigger Event — `emit()`

Callback Function Executes

Remember:

- `on()` → Listen for an event.
- `emit()` → Trigger an event.

# 5️⃣ Passing Data Through Events

We can pass values when triggering an event.

The listener receives those values as function arguments.

Syntax:

```
event.on("eventName", (data) => {
    // Use received data
});

event.emit("eventName", data);
```

### Example

```
const EventEmitter = require("events");

const event = new EventEmitter();

// Listen for userCreated event
event.on("userCreated", (name, age) => {

    console.log("User Name:", name);

    console.log("User Age:", age);

});

// Trigger event and pass data
event.emit("userCreated", "Ramesh", 25);
```

Output:

```
User Name: Ramesh
User Age: 25
```

### Dry Run

```
event.emit("userCreated", "Ramesh", 25);
```

The values are passed in this order:

| `emit()` value | Listener parameter |
| -------------- | ------------------ |
| `"Ramesh"`     | `name`             |
| `25`           | `age`              |

The listener receives the values and prints them.

### Passing an Object

We can also pass an entire object.

```
const EventEmitter = require("events");

const event = new EventEmitter();

event.on("productCreated", (product) => {

    console.log("Product:", product.name);

    console.log("Price:", product.price);

});

event.emit("productCreated", {
    name: "Laptop",
    price: 50000
});
```

Output:

```
Product: Laptop
Price: 50000
```

This approach is useful when an event needs to carry multiple related values.

# 6️⃣ `.once()` Method

## 6.1 What is `.once()`?

The `.once()` method registers an event listener that executes only one time.

Even if we trigger the same event multiple times, the listener executes only once.

Syntax:

```
event.once("eventName", callbackFunction);
```

### Example

```
const EventEmitter = require("events");

const event = new EventEmitter();

// Register listener only once
event.once("login", () => {

    console.log("User logged in!");

});

// Trigger event three times
event.emit("login");

event.emit("login");

event.emit("login");
```

Output:

```
User logged in!
```

### Dry Run

| Step | Action                  | Result              |
| ---- | ----------------------- | ------------------- |
| 1    | Register using `once()` | Listener registered |
| 2    | First `emit()`          | Listener executes   |
| 3    | Second `emit()`         | No execution        |
| 4    | Third `emit()`          | No execution        |

## 6.2 Difference Between `on()` and `once()`

| `on()`                       | `once()`                                          |
| ---------------------------- | ------------------------------------------------- |
| Registers a regular listener | Registers a one-time listener                     |
| Can execute multiple times   | Executes only once                                |
| Listener remains registered  | Listener is automatically removed after execution |
| Used for repeated events     | Used for one-time events                          |

Real-world example: A welcome notification that should be shown only once.

# 7️⃣ `.removeListener()` and `.off()` Methods

## 7.1 What is `.removeListener()`?

Sometimes we register an event listener but later want to remove it.

The `removeListener()` method removes a specific listener from an event.

Syntax:

```
event.removeListener("eventName", callbackFunction);
```

Node.js also provides `.off()`, which is an alias for removing an event listener.

### Example

```
const EventEmitter = require("events");

const event = new EventEmitter();

// Create listener function
function welcome() {

    console.log("Welcome to Node.js");

}

// Register listener
event.on("greet", welcome);

// Trigger event
event.emit("greet");

// Remove listener
event.removeListener("greet", welcome);

// Trigger again
event.emit("greet");
```

Output:

```
Welcome to Node.js
```

Why only one output?

Because we removed the listener before the second `emit()`.

### Using `.off()`

```
event.off("greet", welcome);
```

This performs the same listener-removal operation.

Important: Pass the same function reference that you registered with `on()`.

# 8️⃣ Multiple Listeners for One Event

We can register multiple listeners for the same event.

When the event is triggered, all registered listeners execute.

### Example

```
const EventEmitter = require("events");

const event = new EventEmitter();

// First listener
event.on("orderPlaced", () => {

    console.log("Order created successfully");

});

// Second listener
event.on("orderPlaced", () => {

    console.log("Sending confirmation email");

});

// Third listener
event.on("orderPlaced", () => {

    console.log("Updating product stock");

});

// Trigger event
event.emit("orderPlaced");
```

Output:

```
Order created successfully
Sending confirmation email
Updating product stock
```

### Visual Flow

`orderPlaced` Event

Create Order

Send Email

Update Stock

All three listeners execute when `orderPlaced` is emitted.

Important: EventEmitter listeners execute synchronously by default, in their registration order. Using events does not automatically make the listener functions asynchronous.

# 9️⃣ Custom Events

## 9.1 What are Custom Events?

Custom events are events that we create ourselves according to our application requirements.

For example:

- `userRegistered`
- `userLoggedIn`
- `userLoggedOut`
- `orderPlaced`
- `paymentCompleted`
- `productCreated`

Node.js allows us to create any meaningful event name.

### Example

```
const EventEmitter = require("events");

const event = new EventEmitter();

// Custom event
event.on("paymentCompleted", () => {

    console.log("Payment completed successfully");

});

// Trigger custom event
event.emit("paymentCompleted");
```

Output:

```
Payment completed successfully
```

We created our own event called `paymentCompleted`.

# 🔟 Event-Driven Architecture

## 10.1 What is Event-Driven Architecture?

Event-driven architecture is a programming approach where different parts of an application communicate through events.

One part of the application emits an event, and other parts listen and respond to it.

### Real-world example — Online Shopping Application

When a customer places an order:

1. Order is created.
2. Confirmation email is sent.
3. Product stock is updated.
4. Notification is generated.

These actions can respond to the same event.

Customer places order

`orderPlaced` event

Email

Send confirmation

Inventory

Update stock

Notification

Notify customer

### Why is it useful?

- Separates different responsibilities.
- Makes code easier to maintain.
- Allows multiple listeners for one event.
- Helps organize large applications.

Important: Node.js EventEmitter is useful for events within a Node.js process. It is not, by itself, a distributed messaging system for communication between separate servers.

# 1️⃣1️⃣ Error Event

Node.js EventEmitter provides a special event named `error`.

We can use it to handle errors emitted by an EventEmitter.

### Example

```
const EventEmitter = require("events");

const event = new EventEmitter();

// Listen for error event
event.on("error", (error) => {

    console.log("Error:", error.message);

});

// Trigger error event
event.emit("error", new Error("Something went wrong"));
```

Output:

```
Error: Something went wrong
```

Important: If an EventEmitter emits an `error` event without a registered `error` listener, Node.js throws the error. It may terminate the application if the error is not handled.

# 1️⃣2️⃣ Practical Example — User Registration

Now let's build a simple practical example.

Requirement: When a new user registers, display the user's details.

### Project Structure

```
events-practice/
│
└── app.js
```

### `app.js`

```
// Import EventEmitter
const EventEmitter = require("events");

// Create EventEmitter object
const event = new EventEmitter();

// Listen for user registration event
event.on("userRegistered", (user) => {

    console.log("User registered successfully!");

    console.log("Name:", user.name);

    console.log("Email:", user.email);

});

// Create registration function
function registerUser(name, email) {

    // Create user object
    const user = {
        name: name,
        email: email
    };

    // Trigger registration event
    event.emit("userRegistered", user);

}

// Call registration function
registerUser("Ramesh", "ramesh@gmail.com");
```

### Output

```
User registered successfully!
Name: Ramesh
Email: ramesh@gmail.com
```

### Dry Run

| Step | Code                 | Explanation                 |
| ---- | -------------------- | --------------------------- |
| 1    | `require("events")`  | Imports EventEmitter        |
| 2    | `new EventEmitter()` | Creates event object        |
| 3    | `event.on()`         | Registers listener          |
| 4    | `registerUser()`     | Calls registration function |
| 5    | `const user = {}`    | Creates user object         |
| 6    | `event.emit()`       | Triggers event              |
| 7    | Listener executes    | Displays user details       |

### Understand the Complete Flow

```
registerUser()
      |
      v
Create user object
      |
      v
event.emit("userRegistered", user)
      |
      v
event.on("userRegistered", ...)
      |
      v
Display user details
```

# 1️⃣3️⃣ Common Mistakes

| Mistake                         | Explanation                                  | Correct approach                               |
| ------------------------------- | -------------------------------------------- | ---------------------------------------------- |
| Forgetting `new EventEmitter()` | No event object is created                   | Create an instance                             |
| Using different event names     | Listener will not receive the intended event | Use matching names                             |
| Forgetting `emit()`             | Listener is registered but not triggered     | Trigger the event                              |
| Using `once()` repeatedly       | Listener runs only once                      | Use `on()` when repeated execution is required |
| Removing the wrong function     | Listener may not be removed                  | Use the same function reference                |
| Ignoring `error` events         | An unhandled error can terminate the process | Handle errors appropriately                    |

# 1️⃣4️⃣ Best Practices

1. Use meaningful event names such as `userCreated` and `orderPlaced`.
2. Keep each listener responsible for a specific task.
3. Remove listeners when they are no longer required.
4. Handle special `error` events carefully.
5. Avoid registering duplicate listeners unintentionally.
6. Remember that EventEmitter listeners execute synchronously by default.
7. Do not use EventEmitter as a replacement for a message broker when separate services need to communicate.

# 1️⃣5️⃣ Interview Questions

## Beginner Level

1\. What is the Node.js events module?

It is a built-in Node.js module used to create, listen for, and trigger events.

2\. What is EventEmitter?

EventEmitter is a class that allows us to manage events in Node.js.

3\. What is the purpose of `on()`?

It registers a function to listen for a particular event.

4\. What is the purpose of `emit()`?

It triggers an event and executes its registered listeners.

5\. What is the purpose of `once()`?

It registers a listener that executes only one time.

## Intermediate Level

6\. Can multiple listeners listen to the same event?

Yes. We can register multiple listeners for the same event.

7\. Can we pass data through events?

Yes. We can pass arguments using `emit()` and receive them in the listener function.

8\. How do you remove an event listener?

We can use `off()` or `removeListener()` with the event name and the original listener function.

9\. What is a custom event?

A custom event is an event created by the developer according to application requirements.

10\. What is event-driven architecture?

It is an architecture where different parts of an application communicate by producing and responding to events.

## Advanced Level

11\. Are EventEmitter listeners synchronous or asynchronous by default?

They are synchronous by default. They execute in the order they were registered.

12\. What happens when an `error` event has no listener?

Node.js throws the error, which can terminate the application if it is not handled.

13\. What is the difference between callbacks and events?

A callback is a function passed to another function. An event is an occurrence that can trigger one or more registered listeners.

14\. What is the difference between `on()` and `once()`?

`on()` keeps listening for repeated events, while `once()` removes its listener after the first execution.

15\. Is EventEmitter used for communication between separate Node.js servers?

Not directly. EventEmitter handles events inside a process. Separate services commonly use message brokers or messaging systems.

# 1️⃣6️⃣ Practice Problems

Try these programs in VS Code.

Practice 1 — Welcome Event

Create an event called `welcome`.

- Register a listener.
- Print `Welcome to Node.js`.
- Trigger the event.

Practice 2 — Student Event

Create an event called `studentCreated`.

- Pass student name.
- Pass student age.
- Display both values.

Practice 3 — Login Event

- Create a `login` event.
- Use `once()`.
- Trigger the event three times.
- Observe the output.

Practice 4 — Remove Listener

- Create a listener function.
- Register it using `on()`.
- Trigger the event.
- Remove the listener using `off()`.
- Trigger the event again.

Practice 5 — Multiple Listeners

Create an event called `orderPlaced`.

Register three listeners:

1. Create order message.
2. Send email message.
3. Update stock message.

# 1️⃣7️⃣ Mini Challenge — Order Management System

Your task

Requirement: When a customer places an order, three actions should happen.

1. Print `Order created successfully`.
2. Print `Sending confirmation email`.
3. Print `Updating product stock`.

### Starting Code

```
const EventEmitter = require("events");

const event = new EventEmitter();

// Step 1: Register first listener


// Step 2: Register second listener


// Step 3: Register third listener


// Step 4: Trigger orderPlaced event
```

### Logic-Building Steps

| Step | What should you do?                       |
| ---- | ----------------------------------------- |
| 1    | Create an EventEmitter object             |
| 2    | Register three listeners using `on()`     |
| 3    | Use the same event name for all listeners |
| 4    | Trigger the event using `emit()`          |
| 5    | Check the output                          |

Try it yourself before asking for the solution.

# 1️⃣8️⃣ Chapter Summary

| Topic                     | Explanation                              |
| ------------------------- | ---------------------------------------- |
| Event                     | An action or occurrence                  |
| `events`                  | Built-in Node.js module                  |
| `EventEmitter`            | Class used to manage events              |
| `on()`                    | Registers an event listener              |
| `emit()`                  | Triggers an event                        |
| `once()`                  | Executes listener only once              |
| `off()`                   | Removes an event listener                |
| `removeListener()`        | Removes a specific listener              |
| Custom Events             | Events created by developers             |
| Event-Driven Architecture | Application communication through events |

# 1️⃣9️⃣ Quick Revision

Remember these important methods:

| Method             | Remember                 |
| ------------------ | ------------------------ |
| `on()`             | Listen                   |
| `emit()`           | Trigger                  |
| `once()`           | One time                 |
| `off()`            | Remove                   |
| `removeListener()` | Remove specific listener |

Important code pattern:

```
const EventEmitter = require("events");

const event = new EventEmitter();

event.on("hello", () => {
    console.log("Hello!");
});

event.emit("hello");
```

# 🛑 Chapter 9 Complete

Completed

### Your Node.js learning progress

- ✅ Chapter 1 — Introduction to Node.js
- ✅ Chapter 2 — Installation and Setup
- ✅ Chapter 3 — Node.js Project Structure
- ✅ Chapter 4 — NPM
- ✅ Chapter 5 — Modules
- ✅ Chapter 6 — `path` Module
- ✅ Chapter 7 — `fs` Module
- ✅ Chapter 8 — `os` Module
- ✅ Chapter 9 — `events` Module

### ➡️ Next: Chapter 10 — Node.js `url` Module

In the next chapter, we will learn:

1. What is a URL?
2. What is the `url` module?
3. Importing the URL module.
4. Creating URL objects.
5. `URL` class.
6. `URLSearchParams`.
7. URL properties.
8. Reading query parameters.
9. Modifying query parameters.
10. Practical examples.

Type `NEXT` when you are ready.&#x20;