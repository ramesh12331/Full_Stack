# 📘 Chapter 13 — Callbacks in Node.js



PART 3 — Asynchronous Node.js

Beginner to Advanced



In this chapter, you will learn how Callback Functions work in JavaScript and Node.js.

Callbacks are one of the most important concepts in backend development. They help us handle asynchronous operations such as file reading, database operations, API requests, and network communication.

## 🔑 Requires Before Starting

Before starting this chapter, you should understand:

1. JavaScript functions — Creating and calling functions.
2. Arrow functions — Writing `() => {}`.
3. Function parameters — Passing values into functions.
4. Asynchronous programming — Understanding operations that do not block JavaScript.
5. Event Loop — Basic understanding of how asynchronous callbacks are scheduled.

### 🎮 Interactive chapter guide

Tap an icon to explore the learning activities.

&#x20;Read

&#x20;Code

&#x20;Dry run

&#x20;Quiz

📖 Read: Learn callback concepts with simple definitions and examples.

## 1. What is it?

### 1.1 What is a callback function?

A callback function is a function that we pass as an argument to another function.

The receiving function can call that callback when needed.

Let's understand with a simple example.

```
// Callback function
function greet() {
    console.log("Hello Ramesh!");
}

// Another function accepts a callback
function welcome(callback) {

    console.log("Welcome to Node.js");

    // Execute callback
    callback();
}

// Pass greet function as an argument
welcome(greet);
```

Output:

```
Welcome to Node.js
Hello Ramesh!
```

Here:

- `greet()` is the callback function.
- `welcome()` accepts a function as a parameter.
- `callback()` executes the function passed to `welcome()`.

Important: We pass `greet`, not `greet()`.

```
welcome(greet);   // Pass function reference
welcome(greet()); // Execute immediately and pass its return value
```

These two statements have different meanings.

### 1.2 What is a synchronous callback?

A synchronous callback executes immediately during the execution of the receiving function.

Example:

```
function calculate(callback) {

    console.log("Calculating...");

    callback();
}

function result() {
    console.log("Calculation completed");
}

calculate(result);
```

Output:

```
Calculating...
Calculation completed
```

### 1.3 What is an asynchronous callback?

An asynchronous callback executes later, when an asynchronous operation completes or another scheduled condition is met.

Example:

```
console.log("Start");

setTimeout(() => {
    console.log("Callback executed");
}, 2000);

console.log("End");
```

Output:

```
Start
End
Callback executed
```

Remember: A callback can be synchronous or asynchronous. The word callback describes how a function is passed and invoked, not necessarily when it executes.

## 2. Why do we need it?

Imagine you are building a student management application.

You want to:

1. Read student information from a file.
2. Display the student information.
3. Show a success message after reading finishes.

Reading a file takes time.

If we want to execute some code after reading finishes, we can use a callback.

### Without callback

```
const fs = require("fs");

console.log("Start");

const data = fs.readFileSync("students.txt", "utf-8");

console.log(data);

console.log("File reading completed");
```

The program waits for the file-reading operation to finish.

### With asynchronous callback

```
const fs = require("fs");

console.log("Start");

fs.readFile("students.txt", "utf-8", (err, data) => {

    if (err) {
        console.log(err.message);
        return;
    }

    console.log(data);

    console.log("File reading completed");
});

console.log("Application continues");
```

Possible output:

```
Start
Application continues
Ramesh
Rahul
Suresh
File reading completed
```

The callback runs after the file-reading operation completes.

### Main advantages

- Handles asynchronous operations.
- Executes code after another operation completes.
- Helps separate different tasks.
- Allows functions to be reusable.
- Provides a way to handle errors from asynchronous operations.

## 3. Real-world analogy

Imagine you order food from a restaurant. 🍕

1. You place an order.
2. The restaurant prepares your food.
3. You do other activities while waiting.
4. The restaurant calls you when the food is ready.

Here:

| Real-world activity      | Callback concept              |
| ------------------------ | ----------------------------- |
| Placing an order         | Calling a function            |
| Restaurant prepares food | Asynchronous operation        |
| Your phone number        | Callback registration/contact |
| Restaurant calls you     | Callback execution            |
| Food is ready            | Operation completed           |

Place food order

Food preparation

Asynchronous operation

You do other work

Restaurant calls you

Callback executes

## 4. Architecture / flow

### 4.1 How a callback works

```
       Main Function
            |
            v
    Accept Callback Function
            |
            v
       Perform Task
            |
            v
      Task Completed
            |
            v
     Execute Callback
            |
            v
        Get Result
```

### 4.2 Asynchronous callback architecture

```
       JavaScript Code
             |
             v
       Start Operation
             |
             v
      Asynchronous Work
             |
             v
    Operation Completes
             |
             v
       Callback Ready
             |
             v
         Event Loop
             |
             v
       Execute Callback
```

### 4.3 Callback function structure

```
function mainFunction(callback) {

    // Perform some work

    callback();
}

function myCallback() {

    console.log("Callback executed");

}

// Pass callback function
mainFunction(myCallback);
```

### 4.4 Callback execution flow

mainFunction(myCallback)

Pass callback as argument

callback parameter receives myCallback

callback()

Executes myCallback function

## 5. Syntax

### 5.1 Basic callback syntax

```
function firstFunction(callback) {

    callback();

}

function secondFunction() {

    console.log("Callback executed");

}

firstFunction(secondFunction);
```

### 5.2 Callback using arrow function

```
function greet(callback) {

    callback();

}

greet(() => {
    console.log("Hello Node.js");
});
```

### 5.3 Callback with parameters

```
function calculate(a, b, callback) {

    const result = a + b;

    callback(result);

}

calculate(10, 20, (answer) => {

    console.log(answer);

});
```

Output:

```
30
```

### 5.4 Error-first callback syntax

Node.js commonly uses the error-first callback pattern.

```
function operation(callback) {

    // If error occurs
    if (error) {
        return callback(error, null);
    }

    // If successful
    callback(null, result);

}
```

The usual parameter structure is:

```
callback(error, result);
```

- First parameter: Error.
- Second parameter: Successful result.

If there is no error, the first parameter is normally `null`.

## 6. Basic example

Let's start with simple callback programs.

### Example 1 — Basic callback

File: `callback1.js`

```
// Callback function
function message() {

    console.log("Hello from callback");

}

// Main function
function display(callback) {

    console.log("Main function started");

    // Execute callback
    callback();

}

// Pass function
display(message);
```

Output:

```
Main function started
Hello from callback
```

### Example 2 — Callback using arrow function

File: `callback2.js`

```
function welcome(callback) {

    console.log("Welcome to Node.js");

    callback();

}

welcome(() => {

    console.log("Start learning callbacks");

});
```

Output:

```
Welcome to Node.js
Start learning callbacks
```

### Example 3 — Callback with data

File: `callback3.js`

```
function getUser(callback) {

    const user = {
        name: "Ramesh",
        age: 25
    };

    // Send user object to callback
    callback(user);

}

getUser((user) => {

    console.log("Name:", user.name);

    console.log("Age:", user.age);

});
```

Output:

```
Name: Ramesh
Age: 25
```

## 7. Dry run

Let's execute callback programs step by step.

### Dry run 1 — Basic callback

```
function greet() {
    console.log("Hello");
}

function welcome(callback) {

    console.log("Welcome");

    callback();

}

welcome(greet);
```

Step-by-step:

| Step | Operation                | Result                  |
| ---- | ------------------------ | ----------------------- |
| 1    | Define `greet()`         | Function created        |
| 2    | Define `welcome()`       | Function created        |
| 3    | Call `welcome(greet)`    | Pass function reference |
| 4    | `console.log("Welcome")` | Print Welcome           |
| 5    | `callback()`             | Execute greet           |
| 6    | `console.log("Hello")`   | Print Hello             |

Output:

```
Welcome
Hello
```

### Dry run 2 — Callback with parameters

```
function add(a, b, callback) {

    const result = a + b;

    callback(result);

}

function display(answer) {

    console.log("Result:", answer);

}

add(10, 20, display);
```

Step-by-step:

| Step | Operation                   | Value          |
| ---- | --------------------------- | -------------- |
| 1    | Call `add(10, 20, display)` | `a=10`, `b=20` |
| 2    | Calculate `a + b`           | `30`           |
| 3    | Call `callback(result)`     | Pass 30        |
| 4    | Execute `display(30)`       | Receive answer |
| 5    | Print result                | 30             |

Output:

```
Result: 30
```

### Dry run 3 — Asynchronous callback

```
console.log("Start");

setTimeout(() => {
    console.log("Callback");
}, 2000);

console.log("End");
```

Execution:

1. Print Start.
2. Schedule timer callback.
3. Print End.
4. Timer becomes eligible after approximately two seconds.
5. Execute callback.

Output:

```
Start
End
Callback
```

## 8. Output

### 🎯 Interactive output prediction

Predict the output before revealing the answer.

Output prediction test

4 questions

Question 1

function greet() {\
&#x20; console.log("Hello");\
}\
function welcome(callback) {\
&#x20; console.log("Welcome");\
&#x20; callback();\
}\
welcome(greet);

&#x20;Reveal answer

Question 2

function add(a, b, callback) {\
&#x20; callback(a + b);\
}\
add(5, 10, (result) => console.log(result));

&#x20;Reveal answer

Question 3

console.log("A");\
setTimeout(() => console.log("B"), 0);\
console.log("C");

&#x20;Reveal answer

Question 4

function test(callback) {\
&#x20; console.log("One");\
&#x20; callback();\
&#x20; console.log("Three");\
}\
test(() => console.log("Two"));

&#x20;Reveal answer

## 9. Line-by-line explanation

Let's understand an important Node.js callback example.

File: `readFile.js`

First create `students.txt`:

```
Ramesh
Rahul
Suresh
Priya
```

Now write this code:

```
// Import File System module
const fs = require("fs");

// Display starting message
console.log("Application started");

// Read file asynchronously
fs.readFile("students.txt", "utf-8", (err, data) => {

    // Check whether an error occurred
    if (err) {

        console.log("Error:", err.message);

        return;
    }

    // Display file content
    console.log("Student data:");

    console.log(data);

});

// Continue other work
console.log("Application is running");
```

### Line-by-line explanation

Line 1:

```
const fs = require("fs");
```

Imports the Node.js File System module.

Line 2:

```
console.log("Application started");
```

Prints the starting message.

Line 3:

```
fs.readFile("students.txt", "utf-8", (err, data) => {
```

Starts asynchronous file reading.

Parameters:

- `students.txt` — File name.
- `utf-8` — Encoding.
- `err` — Error information.
- `data` — File content.

Line 4:

```
if (err) {
```

Checks whether file reading failed.

Line 5:

```
console.log("Error:", err.message);
```

Displays the error message.

Line 6:

```
return;
```

Stops execution inside the callback if an error occurs.

Line 7:

```
console.log(data);
```

Displays the file content after successful reading.

Final line:

```
console.log("Application is running");
```

Executes without waiting for the file-reading operation to complete.

### Expected output

```
Application started
Application is running
Student data:
Ramesh
Rahul
Suresh
Priya
```

## 10. Practical example

### Project: Student Management System

Let's create a small application using callbacks.

Folder structure:

```
student-app/
│
├── app.js
└── students.json
```

students.json

```
[
    {
        "id": 1,
        "name": "Ramesh",
        "course": "Node.js"
    },
    {
        "id": 2,
        "name": "Rahul",
        "course": "React.js"
    },
    {
        "id": 3,
        "name": "Suresh",
        "course": "Python"
    }
]
```

### Example 1 — Get all students

File: `app.js`

```
const fs = require("fs");

// Function to get all students
function getStudents(callback) {

    // Read JSON file asynchronously
    fs.readFile("students.json", "utf-8", (err, data) => {

        // Handle file error
        if (err) {
            return callback(err, null);
        }

        try {

            // Convert JSON string into JavaScript array
            const students = JSON.parse(data);

            // Return students through callback
            callback(null, students);

        } catch (error) {

            // Handle invalid JSON
            callback(error, null);

        }

    });

}

// Call getStudents function
getStudents((err, students) => {

    if (err) {
        console.log("Error:", err.message);
        return;
    }

    console.log("Student list:");

    students.forEach((student) => {

        console.log(student.name, "-", student.course);

    });

});
```

Output:

```
Student list:
Ramesh - Node.js
Rahul - React.js
Suresh - Python
```

### Example 2 — Get student by ID

```
const fs = require("fs");

// Get student by ID
function getStudentById(id, callback) {

    fs.readFile("students.json", "utf-8", (err, data) => {

        if (err) {
            return callback(err, null);
        }

        try {

            const students = JSON.parse(data);

            // Find student by ID
            const student = students.find((item) => item.id === id);

            if (!student) {
                return callback(new Error("Student not found"), null);
            }

            callback(null, student);

        } catch (error) {

            callback(error, null);

        }

    });

}

// Call function
getStudentById(2, (err, student) => {

    if (err) {
        console.log(err.message);
        return;
    }

    console.log("Student:", student.name);

    console.log("Course:", student.course);

});
```

Output:

```
Student: Rahul
Course: React.js
```

### Example 3 — Error-first callback

This is an important Node.js pattern.

```
function divide(a, b, callback) {

    if (b === 0) {

        return callback(new Error("Cannot divide by zero"), null);

    }

    const result = a / b;

    callback(null, result);

}

// Successful operation
divide(20, 5, (err, result) => {

    if (err) {
        console.log("Error:", err.message);
        return;
    }

    console.log("Result:", result);

});

// Failed operation
divide(20, 0, (err, result) => {

    if (err) {
        console.log("Error:", err.message);
        return;
    }

    console.log("Result:", result);

});
```

Output:

```
Result: 4
Error: Cannot divide by zero
```

### Understanding error-first callbacks

```
callback(error, result);
```

| Situation | First argument | Second argument |
| --------- | -------------- | --------------- |
| Success   | `null`         | Result          |
| Failure   | Error object   | Usually `null`  |

This pattern is commonly used in Node.js callback-based APIs.

## 11. Common mistakes

### Mistake 1 — Calling the callback with parentheses when passing it

Wrong

```
function greet() {
    console.log("Hello");
}

function welcome(callback) {
    callback();
}

welcome(greet());
```

Here, `greet()` executes immediately and its return value is passed to `welcome()`.

Correct

```
welcome(greet);
```

Pass the function reference.

### Mistake 2 — Forgetting to execute the callback

Wrong

```
function welcome(callback) {

    console.log("Welcome");

    // Callback is never executed
}
```

Correct

```
function welcome(callback) {

    console.log("Welcome");

    callback();

}
```

### Mistake 3 — Forgetting error handling

Avoid

```
fs.readFile("students.txt", "utf-8", (err, data) => {

    console.log(data);

});
```

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

### Mistake 4 — Callback parameter mismatch

Wrong

```
function add(a, b, callback) {

    callback(a + b);

}

add(10, 20, (x, y) => {

    console.log(x, y);

});
```

The callback receives only one argument, but the callback function expects two.

Correct

```
add(10, 20, (result) => {

    console.log(result);

});
```

### Mistake 5 — Assuming every callback is asynchronous

```
function display(callback) {

    console.log("One");

    callback();

    console.log("Three");

}

display(() => {
    console.log("Two");
});
```

Output:

```
One
Two
Three
```

This is a synchronous callback.

A callback is not automatically asynchronous.

## 12. Best practices

1. Use meaningful callback parameter names.
2. Follow the error-first callback pattern when designing Node.js callback APIs.
3. Always check errors before accessing the result.
4. Use `return` after handling an error to prevent further execution.
5. Keep callback functions small and focused.
6. Avoid deeply nested callbacks.
7. Use named functions when callback logic is reusable.
8. Avoid passing unnecessary data through callbacks.
9. Validate data before processing it.
10. Prefer Promises or async/await when asynchronous workflows become complex.

### Professional tip

Callbacks are still important even though modern Node.js applications commonly use Promises and async/await.

You will encounter callbacks in:

- File System APIs.
- Event listeners.
- Stream handling.
- Database libraries.
- Legacy Node.js applications.

## 13. Interview questions

### 🟢 Beginner level

Q1. What is a callback function?

A callback is a function passed as an argument to another function and executed by that function.

Q2. Why do we use callbacks?

We use callbacks to execute code after a task completes or when a particular condition occurs.

Q3. What is a synchronous callback?

A synchronous callback executes immediately when the receiving function calls it.

Q4. What is an asynchronous callback?

An asynchronous callback executes later, for example, after a timer or file operation completes.

Q5. Can we pass parameters to a callback?

Yes. We can pass values as arguments when calling the callback.

### 🟡 Intermediate level

Q6. What is an error-first callback?

It is a Node.js callback pattern in which the first parameter represents an error and the second parameter represents the successful result.

Q7. What is callback nesting?

Callback nesting means placing one callback inside another callback.

Q8. What is callback hell?

Callback hell is a situation where multiple nested callbacks make code difficult to read, debug, and maintain.

Q9. How do you avoid callback hell?

Use named functions, modular code, Promises, and async/await.

Q10. What is the difference between a callback and a Promise?

| Callback                                        | Promise                                |
| ----------------------------------------------- | -------------------------------------- |
| Function passed as an argument                  | Object representing an eventual result |
| Uses callback execution                         | Uses `.then()` and `.catch()`          |
| Nested callbacks can become difficult to manage | Supports chaining                      |
| Error handling is often manual                  | Provides structured rejection handling |

### 🔴 Advanced level

Q11. Does every callback execute asynchronously?

No. A callback can execute synchronously or asynchronously depending on how the receiving function invokes it.

Q12. What happens if a callback is never executed?

The code inside that callback never runs.

Q13. What is callback hell, and why is it a problem?

It is deeply nested callback code. It reduces readability and makes error handling and maintenance difficult.

Q14. How do Promises solve callback hell?

Promises allow asynchronous operations to be chained with `.then()` and errors to be handled through `.catch()`, reducing deeply nested callback structures.

Q15. Can a callback return a value to the original caller?

Not automatically. When an asynchronous callback executes later, its return value does not become the return value of the original function call. A Promise is commonly used when a future result needs to be returned.

## 14. Practice problems

Try these exercises in VS Code.

Exercise 1 — Welcome callback

Create a function named `welcome()`.

Requirements:

- Accept a callback.
- Print `Welcome to Node.js`.
- Execute the callback.
- Print `Start learning`.

Exercise 2 — Addition callback

Create a function named `add()`.

Requirements:

- Accept two numbers.
- Calculate their sum.
- Pass the result to a callback.
- Display the result.

Exercise 3 — User information

Create a function named `getUser()`.

Requirements:

- Create a user object.
- Pass the object to a callback.
- Display the user's name, email, and age.

Exercise 4 — Error-first callback

Create a function named `divide()`.

Requirements:

- Accept two numbers.
- If the second number is zero, return an error through the callback.
- Otherwise, return the result.
- Handle both cases.

Exercise 5 — Read file

Use `fs.readFile()`.

Requirements:

- Create a text file.
- Read it asynchronously.
- Handle file errors.
- Display its content.

Exercise 6 — Multiple callbacks

Create a function named `studentDetails()`.

Requirements:

- Accept a student object.
- Execute a callback to display the name.
- Execute another callback to display the course.

## 15. Mini challenge 🏆

Independent coding challenge

### Build a Student Result Calculator Using Callbacks

Requirement:

Create a function called `calculateResult()`.

It should:

1. Accept a student name.
2. Accept three subject marks.
3. Calculate the total.
4. Calculate the average.
5. Pass the result to a callback.
6. Display the student's result.

Input:

```
calculateResult("Ramesh", 80, 90, 70, callback);
```

Expected output:

```
Student Name: Ramesh
Total Marks: 240
Average Marks: 80
Result: Pass
```

### Hints

- Create a function named `calculateResult()`.
- Accept student name and three marks.
- Accept one callback parameter.
- Calculate total and average.
- Create a result object.
- Pass the result object to the callback.
- Display the details inside the callback.

### Your task

Try writing the complete program without looking at the solution.

## 16. Chapter summary

| Topic                 | What you learned                             |
| --------------------- | -------------------------------------------- |
| Callback function     | Function passed to another function          |
| Callback pattern      | How a receiving function executes a callback |
| Synchronous callback  | Executes immediately                         |
| Asynchronous callback | Executes later                               |
| Callback parameters   | Pass data to callback functions              |
| Error-first callback  | Error is the first parameter                 |
| Callback nesting      | Callback inside another callback             |
| Callback hell         | Deeply nested callback structure             |
| Promises              | Help organize asynchronous operations        |

### Important callback syntax

```
function mainFunction(callback) {

    console.log("Main function");

    callback();

}

mainFunction(() => {

    console.log("Callback executed");

});
```

### Important Node.js pattern

```
fs.readFile("students.txt", "utf-8", (err, data) => {

    if (err) {
        console.log(err.message);
        return;
    }

    console.log(data);

});
```

## 17. Quick revision

## 📚 Chapter 13 — Quick Revision

1\. Callback

A function passed as an argument to another function.

2\. Synchronous callback

Executes immediately.

3\. Asynchronous callback

Executes after an asynchronous operation completes.

4\. Error-first callback

```
callback(error, result);
```

5\. Callback nesting

A callback inside another callback.

6\. Callback hell

Too many nested callbacks, making code difficult to manage.

7\. Promises

Help write asynchronous code with better chaining and error handling.

Remember this example

```
function getData(callback) {

    setTimeout(() => {

        const data = "Student data";

        callback(null, data);

    }, 1000);

}

getData((err, data) => {

    if (err) {
        console.log(err.message);
        return;
    }

    console.log(data);

});
```

Expected output:

```
Student data
```

Chapter 13 completed

### My revision checklist

Revision progress

0/9

I understand callback functions

I understand synchronous callbacks

I understand asynchronous callbacks

I can pass parameters to callbacks

I understand error-first callbacks

I can read files using callbacks

I understand callback nesting

I understand callback hell

I know how Promises help

Practice the exercises and mini challenge. I'll wait for your `NEXT` before starting Chapter 14 — Promises and Async/Await.