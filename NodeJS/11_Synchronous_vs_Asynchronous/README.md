# 📘 Chapter 11 — Synchronous vs Asynchronous in Node.js



PART 3 — Asynchronous Node.js

Beginner to Advanced



In this chapter, you will learn how Node.js executes code, how it handles time-consuming operations, and why asynchronous programming is important for backend development.

## 🔑 Requires Before Starting

Before starting, you should understand:

1. JavaScript functions — How to create and call functions.
2. Variables — `const`, `let`, and basic data types.
3. Callbacks — Basic understanding of passing a function to another function.
4. Node.js basics — How to run JavaScript files using `node filename.js`.
5. Console output — How to understand `console.log()` execution order.

Example:

```
function greet() {
    console.log("Hello");
}

console.log("Start");

greet();

console.log("End");
```

Output:

```
Start
Hello
End
```

JavaScript executes these statements one after another. This is the basic idea of synchronous execution.

## 1. What is it?

In Node.js, we commonly execute code in two ways:

1. Synchronous programming
2. Asynchronous programming

### 1.1 What is synchronous programming?

Synchronous programming means executing code one statement at a time, in order.

The next statement waits until the current statement finishes.

Example:

```
console.log("Task 1");

console.log("Task 2");

console.log("Task 3");
```

Output:

```
Task 1
Task 2
Task 3
```

Execution flow:

```
Task 1 → Task 2 → Task 3
```

### 1.2 What is asynchronous programming?

Asynchronous programming allows Node.js to start an operation and continue executing other code without waiting for that operation to finish.

When the operation completes, its callback or Promise handler can run.

Example:

```
console.log("Task 1");

setTimeout(() => {
    console.log("Task 2");
}, 2000);

console.log("Task 3");
```

Output:

```
Task 1
Task 3
Task 2
```

Why?

- Task 1 executes first.
- `setTimeout()` schedules a callback.
- JavaScript continues to Task 3.
- After approximately 2 seconds, Task 2 executes.

Important: `setTimeout()` does not pause the entire program for two seconds.

### 1.3 Important terminology

| Term         | Simple meaning                                                           |
| ------------ | ------------------------------------------------------------------------ |
| Synchronous  | Execute one operation and wait for it to finish                          |
| Asynchronous | Start an operation and continue without waiting                          |
| Blocking     | Prevent further execution on the same thread until an operation finishes |
| Non-blocking | Allow further execution while an operation is in progress                |
| Callback     | A function passed to another function                                    |
| Promise      | An object representing a future result                                   |
| async/await  | Syntax for working with Promises more clearly                            |

## 2. Why do we need it?

Imagine you are developing a backend application.

A user sends a request to download a large file.

While the file is being read, another user sends a request to view their profile.

If the server performs every operation synchronously, the file-reading operation can block the JavaScript thread. Other JavaScript work must wait.

This can make the application slow.

Asynchronous programming helps Node.js handle operations such as:

- Reading files.
- Writing files.
- Database queries.
- API requests.
- Network communication.
- Uploading and downloading files.

### Example: Synchronous problem

```
const fs = require("fs");

console.log("Application started");

// Synchronous file reading
const data = fs.readFileSync("sample.txt", "utf-8");

console.log(data);

console.log("Application finished");
```

Execution order:

```
Application started
File content
Application finished
```

The program waits until `readFileSync()` finishes reading the file.

### Example: Asynchronous solution

```
const fs = require("fs");

console.log("Application started");

// Asynchronous file reading
fs.readFile("sample.txt", "utf-8", (err, data) => {

    if (err) {
        console.log("Error:", err.message);
        return;
    }

    console.log(data);
});

console.log("Application finished");
```

Possible output:

```
Application started
Application finished
File content
```

The program continues while the file is being read.

Main benefit: Node.js can handle other work instead of keeping the JavaScript thread blocked while waiting for I/O operations.

## 3. Real-world analogy

Imagine you visit a restaurant. 🍽️

### Synchronous restaurant

1. You order food.
2. You stand near the kitchen and wait.
3. You cannot do anything else until your food is ready.
4. After receiving your food, you continue.

Synchronous approach

Place order

Wait for food

Cannot proceed with the next task

Receive food

Continue

### Asynchronous restaurant

1. You place an order.
2. The restaurant starts preparing your food.
3. You sit down and do other things.
4. When food is ready, the restaurant informs you.

Asynchronous approach

Place order

Kitchen prepares food

Work happens in the background

You do other work

No need to wait doing nothing

Food ready notification

In this analogy:

- Placing the order = Starting an asynchronous operation.
- Preparing food = Operation in progress.
- Doing other work = Continuing JavaScript execution.
- Food ready notification = Callback or Promise completion.

## 4. Architecture / flow

### 4.1 Synchronous execution flow

```
       Start
         |
         v
      Task 1
         |
         v
      Task 2
         |
         v
      Task 3
         |
         v
       End
```

Each task must finish before the next task begins.

### 4.2 Asynchronous execution flow

```
          Start
            |
            v
        Task 1
            |
            v
    Start async operation
            |
            v
      Continue JavaScript
            |
            v
        Execute Task 3
            |
            v
  Async operation completes
            |
            v
    Execute callback/handler
            |
            v
           End
```

The exact scheduling depends on the operation type and the Node.js event loop.

### 4.3 How Node.js handles asynchronous work

Node.js uses several parts to manage asynchronous operations:

| Component             | Responsibility                                          |
| --------------------- | ------------------------------------------------------- |
| JavaScript call stack | Executes JavaScript functions                           |
| Node.js runtime       | Provides Node-specific APIs                             |
| Operating system      | Handles many I/O operations                             |
| libuv                 | Helps manage asynchronous I/O and event-loop operations |
| Event loop            | Coordinates when eligible callbacks execute             |

We will study these components deeply in Chapter 12 — Event Loop.

## 5. Syntax

### 5.1 Synchronous syntax

```
const result = operation();

console.log(result);
```

The next statement waits for `operation()` to return.

### 5.2 Asynchronous callback syntax

```
operation((error, result) => {

    if (error) {
        console.log(error);
        return;
    }

    console.log(result);

});
```

The callback runs when the operation completes.

### 5.3 Promise syntax

```
operation()
    .then((result) => {
        console.log(result);
    })
    .catch((error) => {
        console.log(error);
    });
```

### 5.4 async/await syntax

```
async function getData() {

    try {
        const result = await operation();

        console.log(result);

    } catch (error) {
        console.log(error);
    }
}
```

We will study callbacks, Promises, and async/await in more detail in Chapters 13 and 14.

## 6. Basic example

### Example 1 — Synchronous JavaScript

File: `sync.js`

```
// Task 1
console.log("Task 1 started");

// Task 2
console.log("Task 2 started");

// Task 3
console.log("Task 3 started");

console.log("All tasks completed");
```

Run:

```
node sync.js
```

### Example 2 — Asynchronous JavaScript

File: `async.js`

```
// Task 1
console.log("Task 1 started");

// Task 2: Schedule callback after 2 seconds
setTimeout(() => {
    console.log("Task 2 completed");
}, 2000);

// Task 3
console.log("Task 3 started");

console.log("All synchronous tasks completed");
```

Run:

```
node async.js
```

Notice that Task 3 executes before Task 2.

### Example 3 — Blocking vs non-blocking file reading

Create a file named `sample.txt`:

```
Welcome to Node.js asynchronous programming.
```

Blocking example:

```
const fs = require("fs");

console.log("Start");

const data = fs.readFileSync("sample.txt", "utf-8");

console.log(data);

console.log("End");
```

Non-blocking example:

```
const fs = require("fs");

console.log("Start");

fs.readFile("sample.txt", "utf-8", (err, data) => {

    if (err) {
        console.log(err.message);
        return;
    }

    console.log(data);
});

console.log("End");
```

Both programs read the same file, but their execution order is different.

## 7. Dry run

Let's understand the most important concept through dry runs.

### Dry run 1 — Synchronous code

```
console.log("A");

console.log("B");

console.log("C");
```

| Step | Statement          | Output |
| ---- | ------------------ | ------ |
| 1    | `console.log("A")` | A      |
| 2    | `console.log("B")` | B      |
| 3    | `console.log("C")` | C      |

Final output:

```
A
B
C
```

### Dry run 2 — Asynchronous code

```
console.log("A");

setTimeout(() => {
    console.log("B");
}, 2000);

console.log("C");
```

Step-by-step:

| Step | Operation               | Result                    |
| ---- | ----------------------- | ------------------------- |
| 1    | Print A                 | A                         |
| 2    | Call `setTimeout()`     | Schedule callback         |
| 3    | Print C                 | C                         |
| 4    | Timer reaches its delay | Callback becomes eligible |
| 5    | Execute callback        | B                         |

Final output:

```
A
C
B
```

The 2000 milliseconds means approximately 2 seconds, not an exact guarantee that the callback runs at precisely that time.

### Dry run 3 — Asynchronous file reading

```
const fs = require("fs");

console.log("A");

fs.readFile("sample.txt", "utf-8", (err, data) => {
    console.log("B");
});

console.log("C");
```

Execution:

1. Print `A`.
2. Start file reading.
3. Register the callback.
4. Continue executing JavaScript.
5. Print `C`.
6. After file reading completes, execute the callback and print `B`.

Expected output:

```
A
C
B
```

The exact completion time depends on file I/O and system conditions.

### Dry run 4 — Synchronous and asynchronous mixed

```
console.log("Start");

setTimeout(() => {
    console.log("Timer");
}, 0);

console.log("Middle");

console.log("End");
```

Expected output:

```
Start
Middle
End
Timer
```

Important: `setTimeout(..., 0)` does not mean the callback runs immediately. It schedules the callback to run after the current synchronous JavaScript work has completed and the timer is eligible.

## 8. Output

Predict the output before checking the answers.

Output prediction practice

4 questions

Question 1

console.log("One");\
console.log("Two");\
console.log("Three");

Show answer

Question 2

console.log("A");\
setTimeout(() => console.log("B"), 1000);\
console.log("C");

Show answer

Question 3

console.log("Start");\
setTimeout(() => console.log("Timer"), 0);\
console.log("End");

Show answer

Question 4

setTimeout(() => console.log("First"), 0);\
setTimeout(() => console.log("Second"), 0);\
console.log("Third");

Show answer

## 9. Line-by-line explanation

Let's understand a practical asynchronous example.

File: `asyncFile.js`

```
// Import the built-in File System module
const fs = require("fs");

// Step 1: Print starting message
console.log("Application started");

// Step 2: Read file asynchronously
fs.readFile("sample.txt", "utf-8", (err, data) => {

    // Step 3: Handle errors
    if (err) {
        console.log("File reading failed:", err.message);
        return;
    }

    // Step 4: Print file content
    console.log("File content:", data);
});

// Step 5: Continue other JavaScript work
console.log("Application is still working");
```

### Explanation

Line 1:

```
const fs = require("fs");
```

Imports Node.js's built-in File System module.

Line 2:

```
console.log("Application started");
```

Prints the starting message.

Line 3:

```
fs.readFile("sample.txt", "utf-8", (err, data) => {
```

Starts reading the file asynchronously.

Parameters:

- `"sample.txt"` — File name.
- `"utf-8"` — Encoding.
- `err` — Error information if reading fails.
- `data` — File content if reading succeeds.

Line 4:

```
if (err) {
```

Checks whether an error occurred.

Line 5:

```
return;
```

Stops the callback from continuing when an error occurs.

Line 6:

```
console.log("File content:", data);
```

Displays the content after the file is successfully read.

Final line:

```
console.log("Application is still working");
```

This statement does not wait for file reading. It executes while the file operation is in progress.

## 10. Practical example

### Project: Student Management System

Imagine you are developing a backend application that reads student information from a file.

We will compare synchronous and asynchronous file reading.

Folder structure:

```
student-app/
│
├── sync.js
├── async.js
└── students.txt
```

students.txt

```
Ramesh
Rahul
Suresh
```

### A. Synchronous student reading

sync.js

```
const fs = require("fs");

console.log("Student application started");

// Read student file synchronously
const students = fs.readFileSync("students.txt", "utf-8");

// Display students
console.log("Student list:");
console.log(students);

console.log("Application completed");
```

Output:

```
Student application started
Student list:
Ramesh
Rahul
Suresh

Application completed
```

### B. Asynchronous student reading

async.js

```
const fs = require("fs");

console.log("Student application started");

// Read student file asynchronously
fs.readFile("students.txt", "utf-8", (err, students) => {

    // Check error
    if (err) {
        console.log("Unable to read students:", err.message);
        return;
    }

    // Display students
    console.log("Student list:");
    console.log(students);

});

// Other work continues
console.log("Application is ready");
```

Output:

```
Student application started
Application is ready
Student list:
Ramesh
Rahul
Suresh
```

### Which approach is better?

| Situation                                           | Recommended approach        |
| --------------------------------------------------- | --------------------------- |
| Reading a file in a server request                  | Asynchronous                |
| Reading a large file in a server                    | Asynchronous or streaming   |
| A small startup script where blocking is acceptable | Synchronous may be suitable |
| Database operations                                 | Asynchronous                |
| External API requests                               | Asynchronous                |

Professional note: Synchronous operations are not always wrong. They can be useful in scripts or controlled startup tasks. Avoid blocking the main JavaScript thread during normal server request handling.

## 11. Common mistakes

### Mistake 1 — Thinking `setTimeout()` pauses JavaScript

Wrong understanding

```
console.log("Start");

setTimeout(() => {
    console.log("Waited");
}, 3000);

console.log("End");
```

Some beginners expect:

```
Start
Waited
End
```

But the actual output is:

```
Start
End
Waited
```

Reason: `setTimeout()` schedules a callback; it does not pause the current JavaScript execution.

### Mistake 2 — Using synchronous file operations in server request handling

Avoid this for normal server request handling

```
const fs = require("fs");

const data = fs.readFileSync("students.txt", "utf-8");

console.log(data);
```

This blocks the JavaScript thread while the file is read.

Better approach

```
const fs = require("fs");

fs.readFile("students.txt", "utf-8", (err, data) => {

    if (err) {
        console.log(err.message);
        return;
    }

    console.log(data);

});
```

### Mistake 3 — Forgetting error handling

Avoid

```
fs.readFile("students.txt", "utf-8", (err, data) => {
    console.log(data);
});
```

If reading fails, `data` will not contain the expected file content.

Correct

```
fs.readFile("students.txt", "utf-8", (err, data) => {

    if (err) {
        console.log(err.message);
        return;
    }

    console.log(data);

});
```

### Mistake 4 — Assuming asynchronous operations finish in the order they start

```
setTimeout(() => {
    console.log("Task A");
}, 2000);

setTimeout(() => {
    console.log("Task B");
}, 500);
```

Output:

```
Task B
Task A
```

The callback with the shorter timer becomes eligible earlier.

Remember: Starting an operation first does not guarantee that it finishes first.

## 12. Best practices

1. Prefer non-blocking APIs for I/O operations in Node.js servers.
2. Use `fs.readFile()` instead of `fs.readFileSync()` when you do not want to block the JavaScript thread.
3. Always handle errors in callbacks and Promises.
4. Use Promises and async/await for readable asynchronous code.
5. Do not use `setTimeout()` as a replacement for proper asynchronous coordination.
6. Use `Promise.all()` when independent operations can run concurrently.
7. Use sequential `await` when one operation depends on the result of another.
8. Avoid CPU-heavy synchronous work on the main JavaScript thread.
9. Use streaming for large files when loading the entire file into memory is unnecessary.
10. Understand the event loop before building complex asynchronous applications.

Professional tip: Node.js is especially effective for I/O-heavy applications, but asynchronous programming does not automatically make CPU-intensive work faster.

## 13. Interview questions

### 🟢 Beginner level

Q1. What is synchronous programming?

Synchronous programming executes statements one after another. Each operation must finish before the next statement continues.

Q2. What is asynchronous programming?

Asynchronous programming allows an operation to start without making the JavaScript thread wait for its completion.

Q3. What is blocking?

Blocking means an operation prevents further execution on the same thread until it completes.

Q4. What is non-blocking?

Non-blocking means an operation allows the program to continue doing other work while the operation is in progress.

Q5. What is the difference between synchronous and asynchronous code?

| Synchronous                     | Asynchronous                 |
| ------------------------------- | ---------------------------- |
| Waits for the current operation | Can continue without waiting |
| Can block execution             | Often non-blocking for I/O   |
| Simpler execution order         | Completion order may differ  |
| Example: `readFileSync()`       | Example: `readFile()`        |

### 🟡 Intermediate level

Q6. Why does Node.js use asynchronous programming?

Node.js uses asynchronous programming to handle I/O operations efficiently without blocking the main JavaScript thread while waiting for those operations.

Q7. What is a callback?

A callback is a function passed as an argument to another function. It can be executed later when an operation completes.

Q8. What is a Promise?

A Promise is a JavaScript object representing the eventual success or failure of an asynchronous operation.

Q9. What is async/await?

`async` and `await` provide a cleaner way to write code that works with Promises.

Q10. Is `setTimeout()` synchronous or asynchronous?

The timer callback is asynchronous. The call to `setTimeout()` itself executes synchronously and schedules the callback.

### 🔴 Advanced level

Q11. Is Node.js single-threaded?

JavaScript execution in a typical Node.js application runs on a main thread. However, Node.js also uses operating-system facilities and libuv's thread pool for certain operations. Worker threads can be used for parallel JavaScript execution.

Q12. Does asynchronous programming mean parallel execution?

No. Asynchronous execution and parallel execution are different concepts. Asynchronous code allows work to continue without waiting; parallel execution means multiple operations are actually running at the same time.

Q13. What is libuv?

libuv is a library used by Node.js to provide its event loop and asynchronous I/O support.

Q14. Can synchronous code block Node.js?

Yes. Synchronous operations can block the JavaScript thread, preventing it from processing other JavaScript work.

Q15. Is async/await faster than callbacks?

Not necessarily. Async/await mainly improves code readability and structure. It does not automatically make an operation faster.

## 14. Practice problems

Try these exercises in VS Code.

Exercise 1 — Synchronous output

Write a program that prints:

```
Start
Middle
End
```

Use only `console.log()`.

Exercise 2 — Asynchronous timer

Use `setTimeout()` to print:

```
Start
End
Hello after 2 seconds
```

Exercise 3 — File reading

Create `message.txt` and write some text inside it.

Read the file using:

- `fs.readFileSync()`
- `fs.readFile()`

Compare their output order.

Exercise 4 — Multiple timers

Create three timers:

- Timer A: 3 seconds.
- Timer B: 1 second.
- Timer C: 2 seconds.

Predict the output order before running the program.

Exercise 5 — Error handling

Try reading a file that does not exist.

Display a useful error message without crashing your application.

## 15. Mini challenge 🏆

Independent coding challenge

### Build a Student Data Loading Program

Requirement:

Create a Node.js program that reads student data asynchronously from a text file.

Folder structure:

```
student-project/
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

Expected output:

```
Student application started

Loading student data...

Application is running

Student data loaded successfully:

Ramesh
Rahul
Suresh
Priya
```

### Your task

1. Import the `fs` module.
2. Print the application starting message.
3. Read `students.txt` using `fs.readFile()`.
4. Handle errors.
5. Print student information after reading completes.
6. Print `Application is running` without waiting for the file.

Hint:

The important method is:

```
fs.readFile("students.txt", "utf-8", callback);
```

Try to write the complete program yourself.

## 16. Chapter summary

| Topic            | What you learned                                   |
| ---------------- | -------------------------------------------------- |
| Synchronous      | Executes statements in order and waits             |
| Asynchronous     | Allows other work while an operation is pending    |
| Blocking         | Prevents further execution on the same thread      |
| Non-blocking     | Allows execution to continue                       |
| Callback         | Function executed when another operation completes |
| Promise          | Represents an eventual result                      |
| async/await      | Cleaner Promise-based syntax                       |
| `readFileSync()` | Synchronous file reading                           |
| `readFile()`     | Asynchronous file reading                          |
| `setTimeout()`   | Schedules a callback after a delay                 |

### Most important difference

```
// Synchronous
console.log("A");
console.log("B");
console.log("C");

// Output: A B C
```

```
// Asynchronous
console.log("A");

setTimeout(() => {
    console.log("B");
}, 1000);

console.log("C");

// Output: A C B
```

## 17. Quick revision

## Chapter 11 — Quick Revision

Synchronous

- Executes one statement at a time.
- Waits for the current operation.
- Can block the JavaScript thread.

Asynchronous

- Starts an operation without waiting for its completion.
- Allows other JavaScript work to continue.
- Commonly used for I/O operations.

Important methods

| Method           | Meaning                |
| ---------------- | ---------------------- |
| `readFileSync()` | Blocking file read     |
| `readFile()`     | Non-blocking file read |
| `setTimeout()`   | Schedule a callback    |
| `.then()`        | Handle Promise success |
| `.catch()`       | Handle Promise failure |
| `async/await`    | Work with Promises     |

Remember this flow:

```
Synchronous:
Start → Task 1 → Task 2 → End

Asynchronous:
Start → Start async task → Continue
                            ↓
                      Task completes
                            ↓
                       Callback runs
```

Chapter 11 completed

Before moving forward: Practise the timer examples and file-reading exercises. The next chapter will explain exactly how the Call Stack, Event Loop, Callback Queue, Microtasks, and Timers work together in Node.js.

I'll wait for your `NEXT`.