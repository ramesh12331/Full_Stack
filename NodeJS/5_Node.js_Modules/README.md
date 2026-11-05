# 📦 Chapter 5 — Node.js Modules

Welcome to **Chapter 5** 🚀

In this chapter, you will learn one of the most important Node.js concepts: **Modules**.

A beginner often writes everything inside one JavaScript file. As the project grows, that becomes difficult to manage. Modules help us **split our code into separate files and reuse it**.

---

## 1️⃣ What is a Module?

A **module** is a separate JavaScript file that contains related code.

For example:

```text
backend/
│
├── app.js
├── user.js
└── calculator.js
```

Here:

- `app.js` → main application
- `user.js` → user-related code
- `calculator.js` → calculation-related code

Each file can contain its own variables, functions, classes, etc.

### Simple idea

Instead of:

```text
app.js
 ├── user code
 ├── calculator code
 ├── product code
 ├── database code
 └── authentication code
```

We organize it:

```text
app.js
 ├── user.js
 ├── calculator.js
 ├── product.js
 ├── database.js
 └── auth.js
```

This makes the application easier to understand and maintain.

---

# 2️⃣ Why Do We Need Modules?

Imagine you are building an e-commerce application.

You may have:

```text
users
products
orders
payments
authentication
database
```

If everything is written inside `server.js`, the file can become thousands of lines long.

Instead:

```text
src/
│
├── users.js
├── products.js
├── orders.js
├── payments.js
├── auth.js
└── database.js
```

Now each file has a clear responsibility.

### Main benefits

✅ Code organization  
✅ Code reuse  
✅ Easier debugging  
✅ Easier maintenance  
✅ Better teamwork  
✅ Separation of responsibilities  

---

# 3️⃣ Real-World Analogy 🏠

Think about a house.

You don't keep everything in one room.

```text
🏠 House
│
├── 🛏️ Bedroom
├── 🍳 Kitchen
├── 🚿 Bathroom
├── 🛋️ Living Room
└── 📚 Study Room
```

Each room has a specific purpose.

Similarly:

```text
Node.js Application
│
├── user.js
├── product.js
├── order.js
├── database.js
└── auth.js
```

Each module has a specific responsibility.

---

# 4️⃣ Types of Modules in Node.js

There are mainly **three types** you should understand:

### 1. Built-in modules

Provided by Node.js itself.

Examples:

```javascript
fs
path
http
os
events
url
```

You don't need to install them.

---

### 2. Custom modules

Modules created by **you**.

Example:

```text
calculator.js
user.js
database.js
```

---

### 3. Third-party modules

Modules created by other developers and installed using npm.

Examples:

```text
express
mongoose
dotenv
cors
jsonwebtoken
```

You install them using:

```bash
npm install express
```

---

# 5️⃣ Node.js Module Systems

Node.js supports two important module styles:

```text
Module Systems
│
├── CommonJS
│   ├── require()
│   └── module.exports
│
└── ES Modules
    ├── import
    └── export
```

You should understand **both** because you will see both in real projects.

---

# 6️⃣ CommonJS Modules

CommonJS is traditionally very common in Node.js projects.

It uses:

```javascript
require()
```

and

```javascript
module.exports
```

---

## 7️⃣ Creating Your First Custom Module

Create this structure:

```text
node-modules-demo/
│
├── app.js
└── calculator.js
```

### `calculator.js`

```javascript
function add(a, b) {
    return a + b;
}

module.exports = add;
```

Here we created an `add()` function.

But another file cannot automatically use it.

We need to **export** it.

```javascript
module.exports = add;
```

---

# 8️⃣ Importing the Module

Now open `app.js`.

```javascript
const add = require("./calculator");

const result = add(10, 20);

console.log(result);
```

### Output

```text
30
```

---

# 9️⃣ How This Works

Let's understand the flow:

```text
calculator.js
     │
     │ export
     ▼
module.exports = add
     │
     ▼
app.js
     │
     │ require()
     ▼
const add = require("./calculator")
     │
     ▼
add(10, 20)
     │
     ▼
30
```

---

# 🔍 10️⃣ Line-by-Line Explanation

### calculator.js

```javascript
function add(a, b) {
```

Creates a function called `add`.

---

```javascript
return a + b;
```

Adds the two values and returns the result.

---

```javascript
module.exports = add;
```

This makes the `add` function available to other files.

Think:

```text
module.exports
      ↓
"Other files can use this"
```

---

### app.js

```javascript
const add = require("./calculator");
```

`require()` loads our custom module.

```text
./calculator
```

means:

> Look for `calculator.js` in the current folder.

---

```javascript
const result = add(10, 20);
```

Calls the imported function.

---

```javascript
console.log(result);
```

Prints:

```text
30
```

---

# 🧪 11️⃣ Dry Run

Suppose:

```javascript
const add = require("./calculator");
```

Node.js loads:

```text
calculator.js
```

It finds:

```javascript
module.exports = add;
```

So:

```text
add
↓
function add(a, b)
```

Now:

```javascript
add(10, 20)
```

becomes:

```text
10 + 20
   ↓
30
```

Then:

```javascript
console.log(30);
```

Output:

```text
30
```

---

# 1️⃣2️⃣ Exporting Multiple Functions

We can export multiple functions.

### `calculator.js`

```javascript
function add(a, b) {
    return a + b;
}

function subtract(a, b) {
    return a - b;
}

function multiply(a, b) {
    return a * b;
}

module.exports = {
    add,
    subtract,
    multiply
};
```

Now `app.js`:

```javascript
const calculator = require("./calculator");

console.log(calculator.add(10, 5));
console.log(calculator.subtract(10, 5));
console.log(calculator.multiply(10, 5));
```

### Output

```text
15
5
50
```

---

# 1️⃣3️⃣ Destructuring with require()

Instead of:

```javascript
const calculator = require("./calculator");

console.log(calculator.add(10, 5));
```

We can write:

```javascript
const { add, subtract, multiply } = require("./calculator");

console.log(add(10, 5));
console.log(subtract(10, 5));
console.log(multiply(10, 5));
```

This is cleaner when you only need specific functions.

---

# 1️⃣4️⃣ Built-in Modules

Node.js provides many modules.

For example:

```javascript
const os = require("os");

console.log(os.platform());
console.log(os.arch());
```

Here:

```javascript
require("os")
```

loads the Node.js built-in `os` module.

Notice the difference:

```javascript
require("./calculator")
```

Custom module.

```javascript
require("os")
```

Built-in Node.js module.

Later we will study built-in modules deeply.

---

# 1️⃣5️⃣ Third-Party Modules

Suppose we install Express:

```bash
npm install express
```

Then:

```javascript
const express = require("express");
```

Here:

```text
express
   ↓
Third-party npm package
```

You did not create it, and it is not built into Node.js.

It came from npm.

---

# 1️⃣6️⃣ ES Modules

Modern JavaScript provides another module system:

```text
ES Modules
```

It uses:

```javascript
export
```

and:

```javascript
import
```

---

## Example

### `calculator.js`

```javascript
export function add(a, b) {
    return a + b;
}
```

### `app.js`

```javascript
import { add } from "./calculator.js";

console.log(add(10, 20));
```

Output:

```text
30
```

---

# 1️⃣7️⃣ CommonJS vs ES Modules

| CommonJS | ES Modules |
|---|---|
| `require()` | `import` |
| `module.exports` | `export` |
| Traditional Node.js style | Modern JavaScript standard |
| Common in older Node projects | Common in modern projects |
| `const x = require()` | `import x from` |

### CommonJS

```javascript
const add = require("./calculator");
```

### ES Modules

```javascript
import { add } from "./calculator.js";
```

---

# 1️⃣8️⃣ Enabling ES Modules

If your project uses ES Modules, you can specify this in `package.json`:

```json
{
  "type": "module"
}
```

Then you can write:

```javascript
import { add } from "./calculator.js";
```

instead of:

```javascript
const { add } = require("./calculator");
```

---

# 1️⃣9️⃣ When Should You Use Which?

For your learning, understand both.

### CommonJS

You will encounter it in:

- older Node.js projects
- existing backend code
- some tutorials
- some npm packages/projects

### ES Modules

You will commonly see it in:

- modern JavaScript
- modern Node.js projects
- frontend JavaScript
- modern full-stack applications

The important thing is:

> Don't mix the two styles randomly in the same project.

---

# 🔥 20️⃣ Practical Example — User Module

Let's create:

```text
backend/
│
├── app.js
└── user.js
```

### `user.js`

```javascript
const user = {
    name: "Ramesh",
    role: "Full Stack Developer"
};

function getUser() {
    return user;
}

module.exports = {
    user,
    getUser
};
```

### `app.js`

```javascript
const { user, getUser } = require("./user");

console.log(user);

console.log(getUser());
```

### Output

```text
{
  name: 'Ramesh',
  role: 'Full Stack Developer'
}

{
  name: 'Ramesh',
  role: 'Full Stack Developer'
}
```

The important idea is:

```text
user.js
   ↓
Exports data + functions
   ↓
app.js
   ↓
Imports and uses them
```

---

# ⚠️ 21️⃣ Common Mistakes

### Mistake 1 — Forgetting `./`

Wrong:

```javascript
require("calculator");
```

Correct for your own file:

```javascript
require("./calculator");
```

`./` means:

> current folder

---

### Mistake 2 — Wrong filename

If your file is:

```text
calculator.js
```

use:

```javascript
require("./calculator");
```

Don't accidentally write:

```javascript
require("./calculater");
```

---

### Mistake 3 — Forgetting export

You created:

```javascript
function add(a, b) {
    return a + b;
}
```

But forgot:

```javascript
module.exports = add;
```

Another file won't receive the function as expected.

---

### Mistake 4 — Mixing module systems

For example:

```javascript
const add = require("./calculator");
```

and inside the module:

```javascript
export function add() {}
```

Don't mix styles without understanding the module configuration.

---

# ✅ 22️⃣ Best Practices

For real projects:

### Keep modules focused

Good:

```text
user.js
product.js
order.js
```

Avoid putting everything into:

```text
everything.js
```

### Use meaningful names

Good:

```text
database.js
auth.js
userController.js
```

Avoid:

```text
abc.js
test1.js
file2.js
```

### Export only what other modules need

Don't expose unnecessary internal implementation.

---

# 🎯 23️⃣ Interview Questions

### Beginner

**Q1. What is a module in Node.js?**

A module is a separate JavaScript file that contains reusable code such as functions, variables, classes, or objects.

---

**Q2. Why do we use modules?**

To organize code, reuse functionality, make applications easier to maintain, and separate responsibilities.

---

**Q3. What is `require()`?**

`require()` is used in CommonJS to load/import a module.

---

**Q4. What is `module.exports`?**

`module.exports` is used to expose values, functions, objects, or classes from a CommonJS module.

---

### Intermediate

**Q5. What are the three main types of Node.js modules?**

```text
1. Built-in modules
2. Custom modules
3. Third-party modules
```

---

**Q6. Difference between `require()` and `import`?**

```text
require() → CommonJS
import    → ES Modules
```

---

**Q7. What is `./` in `require("./calculator")`?**

It refers to the current directory.

---

### Advanced

**Q8. CommonJS vs ES Modules?**

CommonJS uses:

```javascript
require()
module.exports
```

ES Modules use:

```javascript
import
export
```

Both are module systems, but ES Modules are the modern JavaScript standard.

---

# 🧩 24️⃣ Practice Problems

Try these yourself before looking for a solution.

### Practice 1

Create:

```text
math.js
app.js
```

Export:

```javascript
add()
```

Import it into `app.js`.

---

### Practice 2

Create three functions:

```text
add()
subtract()
multiply()
```

Export all three.

Import them using destructuring.

---

### Practice 3

Create:

```text
user.js
product.js
app.js
```

Export a user object from `user.js`.

Export a product object from `product.js`.

Import both into `app.js`.

---

# 🚀 25️⃣ Mini Challenge

Build this:

```text
module-practice/
│
├── app.js
├── calculator.js
└── user.js
```

### `calculator.js`

Create:

```javascript
add()
subtract()
multiply()
divide()
```

Export all four.

### `user.js`

Create:

```javascript
const user = {
    name: "Ramesh",
    role: "Developer"
};
```

Export it.

### `app.js`

Import everything and produce output similar to:

```text
User: Ramesh
Role: Developer

Addition: 30
Subtraction: 10
Multiplication: 200
Division: 2
```

Try writing it yourself first. This is important for building your Node.js logic.

---

# 🧠 Chapter 5 Summary

You learned:

```text
Module
   ↓
Separate JavaScript file
   ↓
Reusable code
```

### Important concepts

```text
Built-in Module
Custom Module
Third-party Module

CommonJS
   ↓
require()
module.exports

ES Modules
   ↓
import
export
```

### Most important examples

```javascript
const add = require("./calculator");
```

and:

```javascript
module.exports = add;
```

Modern ES Module style:

```javascript
import { add } from "./calculator.js";
```

```javascript
export function add(a, b) {
    return a + b;
}
```

---

# ⚡ Quick Revision

| Concept | Meaning |
|---|---|
| Module | Separate reusable JS file |
| Built-in module | Provided by Node.js |
| Custom module | Created by us |
| Third-party module | Installed through npm |
| `require()` | Import CommonJS module |
| `module.exports` | Export CommonJS code |
| `import` | Import ES Module |
| `export` | Export ES Module |
| `./` | Current folder |
| `package.json` | Project configuration |

---

## ⏸️ STOP — Chapter 5 Complete

**Next chapter → Chapter 6: Node.js Core Modules**

We will start with the most important built-in modules:

```text
📦 path
📁 fs
💻 os
🔗 url
⚡ events
```

and use them with **real VS Code examples + dry runs**.

Type **`NEXT`** when you are ready.