# 📘 Chapter 12 — Node.js Event Loop



PART 3 — Asynchronous Node.js

Beginner to Advanced



In this chapter, you will understand how Node.js executes synchronous and asynchronous code.

We will learn the Call Stack, Event Loop, Callback Queue, Timers, I/O callbacks, Microtasks, Promises, `process.nextTick()`, `setTimeout()`, and `setImmediate()`.

## 🔑 Requires Before Starting

Before starting, you should understand:

1. JavaScript functions — How functions are created and called.
2. Synchronous code — Code that executes one statement at a time.
3. Asynchronous code — Code that can continue without waiting for an operation to finish.
4. Callbacks — Functions passed to another function.
5. Promises — Basic understanding of `.then()` and `.catch()`.
6. Timers — Basic understanding of `setTimeout()`.

If you have completed Chapter 11, you are ready!

### 🎮 Interactive chapter guide

Tap an icon to see a quick introduction to that learning activity.

&#x20;Read

&#x20;Code

&#x20;Dry run

&#x20;Quiz

📖 Read: Understand each Event Loop concept with simple definitions and diagrams.

## 1. What is it?

### 1.1 What is the Event Loop?

The Event Loop is a mechanism in Node.js that coordinates the execution of asynchronous callbacks.

It helps Node.js decide when to execute callbacks after the current JavaScript work has finished and the relevant operation is ready.

In simple words:

- JavaScript executes code using the Call Stack.
- Asynchronous operations are handled using Node.js runtime facilities and the operating system.
- When operations complete, their callbacks become eligible to run.
- The Event Loop helps schedule those callbacks.

### 1.2 What is the Call Stack?

The Call Stack keeps track of functions that are currently executing.

Example:

```
function first() {
    console.log("First function");
}

function second() {
    first();
    console.log("Second function");
}

second();
```

Output:

```
First function
Second function
```

When `second()` calls `first()`, the `first()` function is placed on top of the Call Stack.

After `first()` finishes, it is removed from the stack and `second()` continues.

### 1.3 What is the Callback Queue?

The Callback Queue is a common name for queues that hold callbacks waiting to be processed.

In Node.js, callbacks are handled through different Event Loop phases and queues. It is not just one simple queue.

For example:

```
setTimeout(() => {
    console.log("Timer callback");
}, 1000);
```

The timer callback becomes eligible after its delay. It does not interrupt the currently executing JavaScript code.

### 1.4 What is a Microtask?

A microtask is a high-priority scheduled task that runs after the current JavaScript operation completes, before the Event Loop continues to the next phase.

Examples:

- Promise `.then()` callbacks.
- Promise `.catch()` callbacks.
- Promise `.finally()` callbacks.

Node.js also has a special `process.nextTick()` queue, which is processed before the Promise microtask queue in the usual CommonJS execution context.

### 1.5 What is Node.js Runtime?

The Node.js runtime provides features that allow JavaScript to work outside a browser.

It includes:

- JavaScript engine (V8).
- Node.js APIs.
- Event Loop.
- libuv.
- File System APIs.
- Networking APIs.
- Timers.

## 2. Why do we need it?

Imagine your backend application receives three requests:

1. User A requests student information.
2. User B requests a product list.
3. User C uploads a file.

Some operations take time because they depend on file reading, database access, or network communication.

If Node.js waited synchronously for every I/O operation, it could not efficiently process other JavaScript work while waiting.

The Event Loop helps Node.js coordinate asynchronous operations.

### Without asynchronous handling

```
Request A
   |
Wait for database
   |
Complete Request A
   |
Request B
   |
Wait for database
   |
Complete Request B
```

### With asynchronous handling

```
Request A ── Start database operation
                 |
Request B ── Start another operation
                 |
Request C ── Start file operation
                 |
          Operations complete
                 |
        Handle their callbacks
```

Why is it important?

- Helps Node.js handle many I/O operations efficiently.
- Prevents waiting for I/O from blocking the JavaScript thread.
- Coordinates callbacks and Promise handlers.
- Supports responsive backend applications.

## 3. Real-world analogy

Imagine a receptionist in an office. 🏢

The receptionist has one desk and receives different requests.

1. A visitor asks for a document.
2. The receptionist asks another employee to prepare it.
3. While waiting, the receptionist accepts another visitor's request.
4. When the document is ready, the receptionist handles the completed request.

Visitor requests

JavaScript function call

Receptionist

Call Stack executes JavaScript

Wait for document

Async operation

Help another visitor

Other JavaScript work

Document is ready

Callback becomes eligible to execute

In this analogy:

| Real-world example                     | Node.js concept               |
| -------------------------------------- | ----------------------------- |
| Receptionist                           | JavaScript execution          |
| Work desk                              | Call Stack                    |
| Other employee preparing document      | Asynchronous operation        |
| Completed document notification        | Callback ready                |
| Receptionist handles completed request | Event Loop schedules callback |

## 4. Architecture / flow

### 4.1 Main Node.js Event Loop architecture

JavaScript Code

Your Node.js program

Call Stack

Executes synchronous JavaScript

Node.js Runtime / libuv / OS

Supports timers and asynchronous I/O

Completed operations and eligible callbacks

Event Loop

Coordinates callback execution

Callback executes on Call Stack

### 4.2 Important Event Loop phases

Node.js Event Loop has several phases.

| Phase             | Purpose                                                        |
| ----------------- | -------------------------------------------------------------- |
| Timers            | Executes eligible `setTimeout()` and `setInterval()` callbacks |
| Pending callbacks | Executes certain deferred system-level I/O callbacks           |
| Idle, prepare     | Internal libuv operations                                      |
| Poll              | Retrieves and processes I/O events                             |
| Check             | Executes `setImmediate()` callbacks                            |
| Close callbacks   | Executes certain close-event callbacks                         |

Simplified phase order:

```
       ┌──────────────────────┐
       │        Timers        │
       └──────────┬───────────┘
                  ↓
       ┌──────────────────────┐
       │   Pending Callbacks  │
       └──────────┬───────────┘
                  ↓
       ┌──────────────────────┐
       │     Idle / Prepare   │
       └──────────┬───────────┘
                  ↓
       ┌──────────────────────┐
       │        Poll          │
       └──────────┬───────────┘
                  ↓
       ┌──────────────────────┐
       │        Check         │
       └──────────┬───────────┘
                  ↓
       ┌──────────────────────┐
       │    Close Callbacks   │
       └──────────┬───────────┘
                  │
                  └── Repeat
```

Important: This diagram shows the main phases, not every internal scheduling detail. `process.nextTick()` and Promise microtasks are handled between JavaScript operations and Event Loop phase work.

### 4.3 Call Stack example

```
function one() {
    console.log("One");
}

function two() {
    console.log("Two");
    one();
}

two();
```

Call Stack:

```
       two()
         |
         v
       one()
         |
         v
    console.log()
         |
         v
      Returns
```

The Call Stack works using the LIFO principle:

LIFO = Last In, First Out.

The last function added to the stack is the first one removed.

## 5. Syntax

Let's understand the important Node.js Event Loop functions.

### 5.1 `setTimeout()`

Schedules a callback to run after a specified minimum delay.

Syntax:

```
setTimeout(callback, delay);
```

Example:

```
setTimeout(() => {
    console.log("Timer completed");
}, 2000);
```

Meaning:

- `callback` — Function to execute.
- `2000` — Delay in milliseconds (approximately 2 seconds).

### 5.2 `setImmediate()`

Schedules a callback to execute in the Check phase of the Event Loop.

Syntax:

```
setImmediate(callback);
```

Example:

```
setImmediate(() => {
    console.log("Immediate callback");
});
```

### 5.3 `process.nextTick()`

Schedules a callback in Node.js's special next-tick queue.

Syntax:

```
process.nextTick(callback);
```

Example:

```
process.nextTick(() => {
    console.log("Next tick callback");
});
```

It runs after the current JavaScript operation completes, before the Event Loop continues to its next phase in the usual CommonJS execution context.

### 5.4 Promise microtasks

Promise handlers such as `.then()` are scheduled as microtasks.

```
Promise.resolve().then(() => {
    console.log("Promise callback");
});
```

### 5.5 Callback syntax

```
setTimeout(() => {
    console.log("Timer callback");
}, 1000);
```

### Quick comparison

| Function             | Purpose                                |
| -------------------- | -------------------------------------- |
| `setTimeout()`       | Schedule a timer callback              |
| `setImmediate()`     | Schedule a callback in the Check phase |
| `process.nextTick()` | Schedule a next-tick callback          |
| `Promise.then()`     | Schedule a Promise microtask           |

## 6. Basic example

### Example 1 — Understanding the Call Stack

File: `callStack.js`

```
function first() {
    console.log("First function");
}

function second() {
    console.log("Second function");

    // Call first function
    first();

    console.log("Second function completed");
}

// Start execution
console.log("Start");

second();

console.log("End");
```

Expected output:

```
Start
Second function
First function
Second function completed
End
```

### Example 2 — Understanding `setTimeout()`

File: `timer.js`

```
console.log("Start");

setTimeout(() => {
    console.log("Timer callback");
}, 1000);

console.log("End");
```

Expected output:

```
Start
End
Timer callback
```

### Example 3 — Understanding `setImmediate()`

File: `immediate.js`

```
console.log("Start");

setImmediate(() => {
    console.log("Immediate callback");
});

console.log("End");
```

Expected output:

```
Start
End
Immediate callback
```

### Example 4 — Understanding `process.nextTick()`

File: `nextTick.js`

```
console.log("Start");

process.nextTick(() => {
    console.log("Next tick callback");
});

console.log("End");
```

Expected output:

```
Start
End
Next tick callback
```

### Example 5 — Understanding Promise microtasks

File: `promise.js`

```
console.log("Start");

Promise.resolve().then(() => {
    console.log("Promise callback");
});

console.log("End");
```

Expected output:

```
Start
End
Promise callback
```

## 7. Dry run

This is the most important section of this chapter. Learn the execution order carefully.

### Dry run 1 — Synchronous code and timer

```
console.log("A");

setTimeout(() => {
    console.log("B");
}, 1000);

console.log("C");
```

Step-by-step:

| Step | Operation                  | Result           |
| ---- | -------------------------- | ---------------- |
| 1    | Execute `console.log("A")` | Print A          |
| 2    | Call `setTimeout()`        | Schedule timer   |
| 3    | Execute `console.log("C")` | Print C          |
| 4    | Timer becomes eligible     | Callback can run |
| 5    | Execute timer callback     | Print B          |

Output:

```
A
C
B
```

### Dry run 2 — Call Stack and Promise

```
console.log("A");

Promise.resolve().then(() => {
    console.log("B");
});

console.log("C");
```

Step-by-step:

1. Print A.
2. Schedule Promise callback as a microtask.
3. Print C.
4. Current synchronous JavaScript finishes.
5. Execute Promise microtask and print B.

Output:

```
A
C
B
```

### Dry run 3 — `process.nextTick()` and Promise

```
console.log("A");

process.nextTick(() => {
    console.log("B");
});

Promise.resolve().then(() => {
    console.log("C");
});

console.log("D");
```

Execution order in a CommonJS file:

1. Print A.
2. Schedule next-tick callback B.
3. Schedule Promise microtask C.
4. Print D.
5. Run next-tick callback B.
6. Run Promise microtask C.

Output:

```
A
D
B
C
```

Important: In the usual CommonJS context, Node.js processes the next-tick queue before Promise microtasks after the current JavaScript operation. ESM module evaluation can have different ordering in some examples, so we are using CommonJS for these exercises.

### Dry run 4 — Multiple asynchronous operations

```
console.log("Start");

setTimeout(() => {
    console.log("Timer");
}, 0);

Promise.resolve().then(() => {
    console.log("Promise");
});

process.nextTick(() => {
    console.log("NextTick");
});

console.log("End");
```

Let's dry run:

| Step | Operation                 | Output   |
| ---- | ------------------------- | -------- |
| 1    | Print Start               | Start    |
| 2    | Schedule timer            | —        |
| 3    | Schedule Promise          | —        |
| 4    | Schedule nextTick         | —        |
| 5    | Print End                 | End      |
| 6    | Process nextTick          | NextTick |
| 7    | Process Promise microtask | Promise  |
| 8    | Process eligible timer    | Timer    |

Expected output:

```
Start
End
NextTick
Promise
Timer
```

### Dry run 5 — `setTimeout()` vs `setImmediate()` at top level

```
setTimeout(() => {
    console.log("Timeout");
}, 0);

setImmediate(() => {
    console.log("Immediate");
});
```

Important interview concept

Do not assume a fixed output order here.

At the top level, the order between these two callbacks can vary depending on timing and the Node.js environment.

You may see:

```
Timeout
Immediate
```

or:

```
Immediate
Timeout
```

Both can be valid.

### Dry run 6 — `setImmediate()` inside an I/O callback

File: `ioOrder.js`

```
const fs = require("fs");

fs.readFile(__filename, () => {

    setTimeout(() => {
        console.log("Timeout");
    }, 0);

    setImmediate(() => {
        console.log("Immediate");
    });

});
```

Expected output:

```
Immediate
Timeout
```

Why?

- The file-reading callback executes as an I/O callback.
- `setImmediate()` schedules work for the Check phase.
- The timer callback becomes eligible for the Timers phase.
- In this I/O callback example, the Check phase runs before the next timer callback.

Remember: This is a useful way to understand the difference between `setTimeout()` and `setImmediate()`.

## 8. Output

### 🎯 Interactive output prediction quiz

Try to predict each output before revealing the answer.

Test your understanding

5 questions

Question 1

console.log("A");\
console.log("B");\
console.log("C");

&#x20;Reveal answer

Question 2

console.log("A");\
setTimeout(() => console.log("B"), 0);\
console.log("C");

&#x20;Reveal answer

Question 3

console.log("A");\
Promise.resolve().then(() => console.log("B"));\
console.log("C");

&#x20;Reveal answer

Question 4

console.log("A");\
process.nextTick(() => console.log("B"));\
Promise.resolve().then(() => console.log("C"));\
console.log("D");

&#x20;Reveal answer

Question 5

setTimeout(() => console.log("Timeout"), 0);\
setImmediate(() => console.log("Immediate"));

&#x20;Reveal answer

## 9. Line-by-line explanation

Let's understand one important example containing all the major scheduling concepts.

File: `eventLoop.js`

```
// 1. Synchronous statement
console.log("1. Start");

// 2. Schedule timer callback
setTimeout(() => {
    console.log("5. Timer");
}, 0);

// 3. Schedule Promise microtask
Promise.resolve().then(() => {
    console.log("4. Promise");
});

// 4. Schedule nextTick callback
process.nextTick(() => {
    console.log("3. NextTick");
});

// 5. Synchronous statement
console.log("2. End");
```

Expected output:

```
1. Start
2. End
3. NextTick
4. Promise
5. Timer
```

### Explanation

Line 1:

```
console.log("1. Start");
```

This is synchronous code. It executes immediately.

Line 2:

```
setTimeout(() => {
    console.log("5. Timer");
}, 0);
```

Schedules a timer callback. It does not execute immediately.

Line 3:

```
Promise.resolve().then(() => {
    console.log("4. Promise");
});
```

Creates an already-fulfilled Promise and schedules its `.then()` handler as a microtask.

Line 4:

```
process.nextTick(() => {
    console.log("3. NextTick");
});
```

Schedules a callback in Node.js's next-tick queue.

Line 5:

```
console.log("2. End");
```

This synchronous statement executes before the scheduled callbacks.

### Final execution order

```
Synchronous code
       |
       v
    Start
       |
       v
     End
       |
       v
NextTick queue
       |
       v
 Promise microtasks
       |
       v
  Timer callback
```

This example uses CommonJS and demonstrates the usual Node.js scheduling order.

## 10. Practical example

### Project: Student Management System

Let's build a small example that uses:

- File System module.
- Asynchronous file reading.
- `process.nextTick()`.
- Promise microtasks.
- `setTimeout()`.
- `setImmediate()`.

Folder structure:

```
student-app/
│
├── app.js
└── students.txt
```

students.txt

```
Ramesh
Rahul
Suresh
Priya
```

File: `app.js`

```
const fs = require("fs");

console.log("1. Student application started");

// Read student data asynchronously
fs.readFile("students.txt", "utf-8", (err, data) => {

    if (err) {
        console.log("File error:", err.message);
        return;
    }

    console.log("5. Student data loaded");

    // Schedule a timer
    setTimeout(() => {
        console.log("8. Timer callback");
    }, 0);

    // Schedule immediate callback
    setImmediate(() => {
        console.log("7. Immediate callback");
    });

    // Schedule Promise microtask
    Promise.resolve().then(() => {
        console.log("6. Promise callback");
    });
});

// Schedule nextTick callback
process.nextTick(() => {
    console.log("3. NextTick callback");
});

// Schedule another Promise
Promise.resolve().then(() => {
    console.log("4. Promise outside file callback");
});

console.log("2. Application is running");
```

### Expected output

The first four lines are:

```
1. Student application started
2. Application is running
3. NextTick callback
4. Promise outside file callback
```

After the file-reading operation completes, the remaining output is:

```
5. Student data loaded
6. Promise callback
7. Immediate callback
8. Timer callback
```

### Why does this happen?

1. Synchronous statements execute first.
2. The file-reading operation starts.
3. The `nextTick` callback is scheduled.
4. The outside Promise handler is scheduled.
5. Synchronous JavaScript finishes.
6. Node.js processes the next-tick and Promise callbacks.
7. The file-reading callback executes when the file operation completes.
8. Inside that callback, the Promise microtask is processed after the current callback finishes.
9. The Check phase executes the `setImmediate()` callback before the next timer callback in this I/O example.

Note: The actual time taken by file reading depends on your system. The example assumes the file exists and is read successfully.

## 11. Common mistakes

### Mistake 1 — Thinking `setTimeout(0)` means immediate execution

Wrong understanding

```
console.log("Start");

setTimeout(() => {
    console.log("Timer");
}, 0);

console.log("End");
```

Some beginners expect:

```
Start
Timer
End
```

Correct output

```
Start
End
Timer
```

Reason: The synchronous JavaScript must finish before the timer callback can execute.

### Mistake 2 — Confusing `process.nextTick()` with `setImmediate()`

They are not the same.

| `process.nextTick()`                                      | `setImmediate()`                                 |
| --------------------------------------------------------- | ------------------------------------------------ |
| Uses next-tick queue                                      | Uses Check phase                                 |
| Runs before Promise microtasks in usual CommonJS examples | Runs in a later Event Loop phase                 |
| Can delay Event Loop progress if continuously scheduled   | Allows the Event Loop to progress between phases |

### Mistake 3 — Assuming Promise callbacks run before nextTick callbacks

Wrong order for this CommonJS example

```
Promise.resolve().then(() => {
    console.log("Promise");
});

process.nextTick(() => {
    console.log("NextTick");
});
```

Correct output

```
NextTick
Promise
```

### Mistake 4 — Assuming `setTimeout()` always executes before `setImmediate()`

At the top level, there is no guaranteed fixed order between them.

Do not write code that depends on one always running first.

### Mistake 5 — Thinking the Event Loop executes multiple JavaScript callbacks simultaneously

The JavaScript callbacks on the main thread execute one at a time.

Asynchronous I/O can progress outside the JavaScript execution stack, but that does not mean two main-thread JavaScript callbacks run simultaneously.

### Mistake 6 — Continuously scheduling `process.nextTick()`

Example:

```
function repeat() {
    process.nextTick(repeat);
}

repeat();
```

This continuously fills the next-tick queue and can prevent the Event Loop from progressing.

Avoid recursive next-tick scheduling unless you have a specific reason.

## 12. Best practices

1. Avoid blocking the Event Loop. Do not perform heavy synchronous operations during normal server request processing.
2. Use asynchronous I/O APIs. Prefer asynchronous file and network operations.
3. Understand microtask ordering. Know the difference between `process.nextTick()` and Promise callbacks.
4. Do not depend on top-level timer ordering. `setTimeout(0)` and `setImmediate()` do not have a guaranteed order in every situation.
5. Avoid unnecessary `process.nextTick()` usage. Excessive use can delay other Event Loop work.
6. Use `setImmediate()` when scheduling work for the Check phase is appropriate.
7. Use Promises and async/await for readable asynchronous code.
8. Handle asynchronous errors. Use appropriate error handling for callbacks and Promises.
9. Move CPU-heavy work off the main thread. Consider Worker Threads for suitable CPU-intensive tasks.
10. Test actual execution order. Run examples in your Node.js environment instead of assuming every asynchronous operation behaves identically.

## 13. Interview questions

### 🟢 Beginner level

Q1. What is the Event Loop in Node.js?

The Event Loop coordinates asynchronous callback execution after the current JavaScript operation completes.

Q2. What is the Call Stack?

The Call Stack tracks functions that are currently executing. It follows the LIFO principle.

Q3. What is a Callback Queue?

It is a general term for queues holding callbacks waiting to be executed. Node.js uses multiple Event Loop phases and scheduling queues.

Q4. What is a microtask?

A microtask is a scheduled task, such as a Promise `.then()` handler, that runs after the current JavaScript operation.

Q5. What is `process.nextTick()`?

It schedules a callback in Node.js's special next-tick queue.

### 🟡 Intermediate level

Q6. What are the main Event Loop phases?

- Timers.
- Pending callbacks.
- Idle and prepare.
- Poll.
- Check.
- Close callbacks.

Q7. What is the difference between `setTimeout()` and `setImmediate()`?

`setTimeout()` schedules a timer callback, while `setImmediate()` schedules a callback for the Check phase.

Q8. What is the difference between Promise microtasks and `process.nextTick()`?

In the usual CommonJS execution context, next-tick callbacks are processed before Promise microtasks.

Q9. What is the Poll phase?

The Poll phase handles I/O events and callbacks. It can also wait for I/O events when appropriate.

Q10. What is the Check phase?

The Check phase executes callbacks scheduled using `setImmediate()`.

### 🔴 Advanced level

Q11. What happens if the Call Stack is busy?

Other JavaScript callbacks cannot execute on the main thread until the current JavaScript execution finishes.

Q12. Can the Event Loop execute callbacks simultaneously?

No. JavaScript callbacks on the main thread execute one at a time.

Q13. What happens if `process.nextTick()` is called recursively?

It can continuously fill the next-tick queue and delay other Event Loop phases.

Q14. What is libuv?

libuv is a library that provides Node.js with its Event Loop and asynchronous I/O support.

Q15. Why is the Event Loop important in backend development?

It helps Node.js handle asynchronous operations efficiently without blocking the main JavaScript thread while waiting for I/O.

Q16. Is `setTimeout(fn, 0)` guaranteed to run before `setImmediate(fn)`?

No. Their top-level ordering is not guaranteed.

Q17. What is the difference between asynchronous and parallel execution?

Asynchronous execution allows code to continue without waiting. Parallel execution means multiple operations actually run at the same time.

## 14. Practice problems

Try these exercises in VS Code.

Exercise 1 — Call Stack

Write three functions:

- `first()`
- `second()`
- `third()`

Call them inside each other and predict the output.

Exercise 2 — Timer

Use `setTimeout()` with a delay of 0.

Expected output:

```
Start
End
Timer
```

Exercise 3 — Promise microtask

Create a Promise using `Promise.resolve()` and use `.then()` to print a message.

Predict the output along with two synchronous `console.log()` statements.

Exercise 4 — NextTick

Use:

- `console.log()`
- `process.nextTick()`
- `Promise.resolve().then()`

Predict the execution order in a CommonJS file.

Exercise 5 — Timer vs Immediate

Create both `setTimeout()` and `setImmediate()` at the top level.

Run the code multiple times and observe whether the order is consistent.

Exercise 6 — I/O callback

Use `fs.readFile()` and schedule both `setTimeout()` and `setImmediate()` inside its callback.

Observe the output order.

## 15. Mini challenge 🏆

Independent coding challenge

### Build an Event Loop Output Prediction Program

Write the following code in a file named `challenge.js`.

```
console.log("1. Start");

setTimeout(() => {
    console.log("2. Timeout");
}, 0);

Promise.resolve().then(() => {
    console.log("3. Promise");
});

process.nextTick(() => {
    console.log("4. NextTick");
});

setImmediate(() => {
    console.log("5. Immediate");
});

console.log("6. End");
```

### Your task

Before running the code:

1. Identify the synchronous statements.
2. Identify the timer callback.
3. Identify the Promise microtask.
4. Identify the next-tick callback.
5. Identify the immediate callback.
6. Predict the output.

Hint: In a CommonJS file, the first four output positions are predictable, but the relative order of the top-level timer and immediate callbacks is not guaranteed.

### Check your answer

&#x20;Reveal explanation

## 16. Chapter summary

| Topic                | What you learned                                 |
| -------------------- | ------------------------------------------------ |
| Event Loop           | Coordinates asynchronous callback execution      |
| Call Stack           | Tracks currently executing functions             |
| Node.js Runtime      | Provides Node.js execution environment and APIs  |
| Callback Queue       | General term for queues holding callbacks        |
| Timers               | Handles timer callbacks                          |
| I/O callbacks        | Handles completed I/O operations                 |
| Microtasks           | Handles Promise callbacks                        |
| Promise Queue        | Queue for Promise microtasks                     |
| `process.nextTick()` | Schedules next-tick callbacks                    |
| `setTimeout()`       | Schedules timer callbacks                        |
| `setImmediate()`     | Schedules Check-phase callbacks                  |
| libuv                | Provides Event Loop and asynchronous I/O support |

### Important execution order

For a typical CommonJS example:

```
1. Synchronous JavaScript
          ↓
2. process.nextTick()
          ↓
3. Promise microtasks
          ↓
4. Event Loop phases
          ↓
5. Eligible callbacks execute
```

Remember: The exact scheduling depends on the context and the type of asynchronous operation.

## 17. Quick revision

## 📚 Chapter 12 — Quick Revision

1\. Call Stack

Executes JavaScript functions.

2\. Event Loop

Coordinates asynchronous callback execution.

3\. Microtasks

Promise handlers execute as microtasks.

4\. NextTick

`process.nextTick()` schedules callbacks in Node.js's next-tick queue.

5\. Timers

`setTimeout()` schedules timer callbacks.

6\. Check phase

`setImmediate()` schedules callbacks for this phase.

Important methods

| Method               | Remember                  |
| -------------------- | ------------------------- |
| `process.nextTick()` | Next-tick queue           |
| `Promise.then()`     | Promise microtask         |
| `setTimeout()`       | Timer phase               |
| `setImmediate()`     | Check phase               |
| `fs.readFile()`      | Asynchronous file reading |

One final example to remember

```
console.log("A");

process.nextTick(() => {
    console.log("B");
});

Promise.resolve().then(() => {
    console.log("C");
});

setTimeout(() => {
    console.log("D");
}, 0);

console.log("E");
```

Expected output in CommonJS:

```
A
E
B
C
D
```

Chapter 12 completed

Your learning checklist

My revision progress

0/8

I understand the Call Stack

I understand the Event Loop

I understand Event Loop phases

I understand Microtasks and Promise callbacks

I understand process.nextTick()

I understand setTimeout()

I understand setImmediate()

I can predict asynchronous output

Practice the output-prediction questions before moving forward. I'll wait for your `NEXT` before starting Chapter 13 — Callbacks.