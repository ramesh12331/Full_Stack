# 🚀 CHAPTER 3 — Node.js Project Structure

### 📚 In This Chapter We Will Learn

- 📁 Project folder
- 📦 `package.json`
- 🔒 `package-lock.json`
- 📦 `node_modules`
- 📂 `src`
- 🚀 `server.js`
- ⚙️ `app.js`
- 🔐 `.env`
- 🚫 `.gitignore`

### 🎯 We Will Also Understand

- Why each file exists
- How Node.js projects are organized
- Professional Node.js folder structure

---

# 1️⃣ 📁 Project Folder

A **project folder** is the main folder where we keep all the files and folders related to our Node.js application.

For example:

```text
my-node-app/
│
├── package.json
├── package-lock.json
├── node_modules/
├── src/
├── app.js
├── server.js
├── .env
└── .gitignore
```

Instead of keeping files randomly on your computer, we keep everything belonging to one application inside one project folder.

### 🧠 Beginner idea

Think of the project folder like a **school bag** 🎒.

Inside the bag, you have different things:

```text
🎒 Node.js Project
│
├── 📦 Packages
├── 💻 Source code
├── ⚙️ Configuration
├── 🔐 Environment settings
└── 📝 Project information
```

Each file has a different job.

---

# 2️⃣ 📦 `package.json`

`package.json` is one of the most important files in a Node.js project.

When we create a Node.js project using:

```bash
npm init -y
```

npm creates:

```text
package.json
```

A simple example:

```json
{
  "name": "my-node-app",
  "version": "1.0.0",
  "description": "My Node.js application",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  }
}
```

### 🧠 Why do we need it?

`package.json` stores important information about our project.

For example:

```text
package.json
     │
     ├── Project name
     ├── Project version
     ├── Description
     ├── Scripts
     └── Dependencies
```

Suppose we install Express:

```bash
npm install express
```

npm adds Express to `package.json`:

```json
{
  "dependencies": {
    "express": "^5.1.0"
  }
}
```

The exact version may be different on your computer.

### 💡 Simple understanding

Think of `package.json` as the **information card of your project**.

It tells npm:

> "This is my project, these are the packages I need, and these are the commands I can run."

---

# 3️⃣ 🔒 `package-lock.json`

When we install a package:

```bash
npm install express
```

npm creates or updates:

```text
package-lock.json
```

This file keeps track of the **resolved versions of packages and their dependencies**.

For example:

```text
Your project
     ↓
   Express
     ↓
Other packages required by Express
     ↓
Other dependencies
```

There may be many packages inside this dependency tree.

`package-lock.json` records the resolved dependency information so that npm can reproduce the installation more consistently.

### 🧠 Beginner understanding

Think:

```text
package.json
      ↓
"I need Express"

package-lock.json
      ↓
"Here is the resolved dependency information
for this installation."
```

### Important

Unlike `node_modules`, `package-lock.json` is normally committed to Git.

---

# 4️⃣ 📦 `node_modules`

When we install a package:

```bash
npm install express
```

npm downloads Express and the packages it needs.

They are stored in:

```text
node_modules/
```

Example:

```text
my-node-app/
│
├── node_modules/
│   ├── express/
│   └── ...
│
├── package.json
└── package-lock.json
```

### 🧠 Why do we need `node_modules`?

Your application may depend on packages such as:

```text
Express
Mongoose
dotenv
jsonwebtoken
bcrypt
```

Those packages need to exist on your computer so your application can use them.

`node_modules` contains those installed dependencies.

### ⚠️ Important

Normally, we don't manually edit files inside `node_modules`.

npm manages this folder for us.

---

# 5️⃣ 🚫 Why Don't We Upload `node_modules` to GitHub?

`node_modules` can become very large.

For example:

```text
node_modules/
    ↓
Hundreds or thousands of files
    ↓
Large folder
```

Instead, we keep:

```text
package.json
package-lock.json
```

in the repository.

Another developer can download the project and run:

```bash
npm install
```

npm will recreate `node_modules`.

So normally:

```text
GitHub
│
├── package.json          ✅
├── package-lock.json     ✅
└── node_modules/         ❌
```

---

# 6️⃣ 📂 `src`

`src` means **source**.

It is commonly used to store the actual application source code.

For example:

```text
src/
│
├── controllers/
├── models/
├── routes/
├── services/
├── middleware/
└── utils/
```

### 🧠 Why do we need `src`?

Imagine your application becomes large.

If everything is inside one file:

```text
server.js
   ↓
Routes
Database
Authentication
Validation
Business logic
Error handling
...
3000+ lines 😵
```

It becomes difficult to understand and maintain.

Instead, we divide the code:

```text
src/
│
├── routes/
├── controllers/
├── services/
├── models/
└── middleware/
```

Now every part has a clear responsibility.

This idea is called **separation of concerns**.

---

# 7️⃣ 🚀 `server.js`

`server.js` is commonly used to **start the Node.js server**.

For example:

```javascript
const app = require("./app");

const PORT = 5000;

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

The important line is:

```javascript
app.listen(PORT);
```

It tells the application to start listening for incoming requests on a port.

### 🧠 Beginner understanding

Think of `server.js` as the **ON button** 🔘 for your backend server.

```text
server.js
    ↓
Start application
    ↓
Listen on port 5000
    ↓
Server running 🚀
```

---

# 8️⃣ ⚙️ `app.js`

`app.js` commonly contains the configuration of the application itself.

For example, with Express:

```javascript
const express = require("express");

const app = express();

app.use(express.json());

app.get("/", (req, res) => {
  res.send("Hello Node.js");
});

module.exports = app;
```

Here we:

1. Import Express.
2. Create the application.
3. Add middleware.
4. Add a route.
5. Export the application.

### 🧠 Beginner understanding

Think of `app.js` as the **setup/control room** of your application.

```text
app.js
  ↓
Create application
  ↓
Configure middleware
  ↓
Configure routes
  ↓
Export application
```

---

# 9️⃣ 🔄 `app.js` vs `server.js`

This is very important.

### `app.js`

Main question:

> **What should my application do?**

```text
app.js
  ↓
Application configuration
  ↓
Middleware
  ↓
Routes
```

### `server.js`

Main question:

> **How do I start my application?**

```text
server.js
  ↓
Import app
  ↓
Choose port
  ↓
app.listen()
  ↓
Server starts
```

So:

```text
             app.js
               │
               │ Application
               ▼
           server.js
               │
               │ Starts
               ▼
        HTTP Server 🚀
```

Keeping these responsibilities separate makes the project easier to organize and test.

---

# 🔐 1️⃣0️⃣ `.env`

`.env` is commonly used to store **environment variables**.

For example:

```env
PORT=5000
DATABASE_URL=postgresql://localhost/mydatabase
JWT_SECRET=my-secret-key
```

These values may change depending on the environment.

For example:

```text
Development
      ↓
PORT=5000

Production
      ↓
PORT=8080
```

Instead of hard-coding configuration directly into your source code, we can use environment variables.

Later, we will learn how `dotenv` loads `.env` values into `process.env`.

For example:

```javascript
console.log(process.env.PORT);
```

---

# 🚨 Why Should We Protect `.env`?

`.env` may contain sensitive information:

```text
Database password
API keys
JWT secret
Cloud credentials
```

For example:

```env
DATABASE_PASSWORD=very-secret-password
```

We should not normally publish this information on GitHub.

That's why we put `.env` inside `.gitignore`.

---

# 1️⃣1️⃣ 🚫 `.gitignore`

`.gitignore` is a file that tells **Git which files/folders should not be tracked**.

Example:

```gitignore
node_modules/
.env
```

This means:

```text
node_modules/
     ↓
Don't track it

.env
     ↓
Don't track it
```

### 🧠 Beginner understanding

Think of `.gitignore` as a **"Do Not Upload" list** 📋.

For example:

```text
.gitignore

Don't upload:
❌ node_modules
❌ .env
```

---

# 1️⃣2️⃣ 🏗️ Simple Node.js Project

At the beginning, your project can be simple:

```text
my-node-app/
│
├── app.js
├── server.js
├── package.json
├── package-lock.json
├── .env
└── .gitignore
```

This is enough for a small application.

But as the project grows, we need more folders.

---

# 1️⃣3️⃣ 🏢 Professional Node.js Structure

A professional backend can look like this:

```text
backend/
│
├── node_modules/
│
├── src/
│   │
│   ├── config/
│   │   └── db.js
│   │
│   ├── controllers/
│   │   ├── userController.js
│   │   └── productController.js
│   │
│   ├── models/
│   │   ├── userModel.js
│   │   └── productModel.js
│   │
│   ├── routes/
│   │   ├── userRoutes.js
│   │   └── productRoutes.js
│   │
│   ├── services/
│   │   ├── userService.js
│   │   └── productService.js
│   │
│   ├── middleware/
│   │   ├── authMiddleware.js
│   │   └── errorMiddleware.js
│   │
│   └── utils/
│       └── helper.js
│
├── app.js
├── server.js
├── .env
├── .gitignore
├── package.json
└── package-lock.json
```

Don't worry about all these folders yet. We will learn them one by one in later chapters.

---

# 1️⃣4️⃣ 📂 `routes`

Routes define **which URL should perform which operation**.

For example:

```text
GET    /users
POST   /users
GET    /users/10
PUT    /users/10
DELETE /users/10
```

A file might be:

```text
routes/
└── userRoutes.js
```

Later, when we learn Express, you'll understand this deeply.

---

# 1️⃣5️⃣ 🎮 `controllers`

Controllers handle the request and response.

For example:

```text
Client
  ↓
Route
  ↓
Controller
  ↓
Response
```

A controller might contain logic such as:

```javascript
const getUsers = (req, res) => {
  // Get users
  // Send response
};
```

The controller should focus mainly on handling the HTTP request/response rather than putting the entire application logic into one function.

---

# 1️⃣6️⃣ 🧠 `services`

Services are commonly used for **business logic**.

For example, suppose a customer places an order.

The service may handle:

```text
Check product
     ↓
Check stock
     ↓
Calculate total
     ↓
Create order
```

Then the controller can remain simpler.

A common flow is:

```text
Route
  ↓
Controller
  ↓
Service
  ↓
Model
  ↓
Database
```

---

# 1️⃣7️⃣ 🗃️ `models`

Models represent the application's data/database layer.

For example:

```text
models/
├── userModel.js
└── productModel.js
```

Later, when we learn MongoDB, PostgreSQL, Mongoose, and ORMs, this folder will become very important.

---

# 1️⃣8️⃣ 🛡️ `middleware`

Middleware is code that runs during the request/response process.

Common examples:

```text
Authentication
Authorization
Validation
Logging
Error handling
```

For example:

```text
Request
   ↓
Authentication middleware
   ↓
Route
   ↓
Controller
```

We'll learn middleware properly when we reach Express.

---

# 1️⃣9️⃣ 🔧 `utils`

`utils` contains reusable helper functions.

For example:

```text
utils/
└── helper.js
```

A helper function might perform a common task that is needed in multiple places.

---

# 2️⃣0️⃣ 🔄 Professional Request Flow

When we eventually build a real API, a common structure is:

```text
             Client
                │
                ▼
              Route
                │
                ▼
           Controller
                │
                ▼
             Service
                │
                ▼
              Model
                │
                ▼
            Database
```

For example:

```text
POST /users
     ↓
userRoutes.js
     ↓
userController.js
     ↓
userService.js
     ↓
userModel.js
     ↓
Database
```

This structure keeps the application organized.

---

# 🧠 2️⃣1️⃣ Easy Way to Remember

Think of a restaurant 🍽️:

```text
Customer
   ↓
Route
```

The customer tells the waiter what they want.

```text
Waiter
   ↓
Controller
```

The waiter handles the request.

```text
Kitchen
   ↓
Service
```

The kitchen performs the actual business work.

```text
Storage/Ingredients
   ↓
Model + Database
```

The data comes from storage.

So:

```text
Customer
   ↓
Route
   ↓
Controller
   ↓
Service
   ↓
Model
   ↓
Database
```

This is why professional applications separate different responsibilities.

---

# 🛠️ 2️⃣2️⃣ Create the Project Yourself

Create a folder:

```text
node-chapter-3
```

Open it in VS Code.

Run:

```bash
npm init -y
```

Then create:

```text
node-chapter-3/
│
├── src/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── services/
│   ├── middleware/
│   └── utils/
│
├── app.js
├── server.js
├── .env
├── .gitignore
├── package.json
└── package-lock.json
```

If you install a package later, you'll also get:

```text
node_modules/
```

---

# ✍️ 2️⃣3️⃣ `.gitignore`

Put:

```gitignore
node_modules/
.env
```

---

# ✍️ 2️⃣4️⃣ `.env`

For practice:

```env
PORT=5000
```

---

# ✍️ 2️⃣5️⃣ `app.js`

For now, just understand the structure:

```javascript
const express = require("express");

const app = express();

app.use(express.json());

app.get("/", (req, res) => {
  res.send("Hello Node.js");
});

module.exports = app;
```

Don't worry if you don't understand Express yet.

We will learn Express properly later.

---

# ✍️ 2️⃣6️⃣ `server.js`

```javascript
const app = require("./app");

const PORT = 5000;

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

The important idea is:

```text
server.js
    ↓
loads app.js
    ↓
gets application
    ↓
starts server
```

---

# 🔄 2️⃣7️⃣ Dry Run

When you run:

```bash
node server.js
```

### Step 1

Node starts:

```text
server.js
```

### Step 2

This line runs:

```javascript
const app = require("./app");
```

It loads `app.js`.

### Step 3

`app.js` creates the application:

```javascript
const app = express();
```

### Step 4

`app.js` exports it:

```javascript
module.exports = app;
```

### Step 5

`server.js` receives the application.

### Step 6

This starts the server:

```javascript
app.listen(PORT);
```

Final flow:

```text
node server.js
      ↓
  server.js
      ↓
   app.js
      ↓
Create application
      ↓
Export application
      ↓
server.js receives it
      ↓
app.listen()
      ↓
🚀 Server starts
```

---

# ⚠️ Common Beginner Mistakes

### Mistake 1: Uploading `.env`

❌ Don't normally commit:

```text
.env
```

Add:

```gitignore
.env
```

---

### Mistake 2: Uploading `node_modules`

❌ Don't normally commit:

```text
node_modules/
```

Add:

```gitignore
node_modules/
```

---

### Mistake 3: Putting everything in one file

Avoid creating:

```text
server.js
   ↓
Routes
Database
Authentication
Validation
Business logic
Error handling
2000+ lines
```

As the project grows, separate the responsibilities.

---

### Mistake 4: Thinking `src` is mandatory

`src` is a **common organizational convention**. Node.js itself does not require you to use a `src` folder.

You can have:

```text
app.js
server.js
```

directly in the root.

But professional projects often use folders to keep source code organized.

---

# 🎯 2️⃣8️⃣ Interview Questions

### Beginner

**Q1. What is `package.json`?**

`package.json` is the main project information file in a Node.js application. It contains things such as the project name, version, scripts, and declared dependencies.

---

**Q2. What is `node_modules`?**

It contains the packages installed for the project and the dependencies required by those packages.

---

**Q3. Why don't we normally commit `node_modules`?**

Because it can be very large. The project can recreate it using `npm install` based on `package.json` and the lockfile.

---

**Q4. What is `.env`?**

It is commonly used to store environment-specific configuration such as ports, database connection information, and secrets.

---

**Q5. What is `.gitignore`?**

It tells Git which files and folders should not be tracked.

---

### Intermediate

**Q6. Why separate `app.js` and `server.js`?**

Separating application configuration from server startup makes the code easier to organize, test, and maintain.

---

**Q7. What is the purpose of `src`?**

It provides a place to organize the application's source code.

---

**Q8. What is the difference between `package.json` and `package-lock.json`?**

`package.json` describes the project's declared dependencies and configuration, while `package-lock.json` records the resolved dependency tree and package versions.

---

# 🧪 2️⃣9️⃣ Practice

Try creating this structure without copying:

```text
backend/
│
├── src/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── services/
│   ├── middleware/
│   └── utils/
│
├── app.js
├── server.js
├── .env
├── .gitignore
├── package.json
└── package-lock.json
```

Then explain each folder/file in your own words.

---

# 🏁 Chapter 3 Summary

The main idea of this chapter is:

> **A Node.js project should be organized so that each part of the application has a clear responsibility.**

```text
📁 Project
│
├── 📦 package.json
│      → Project information + dependencies
│
├── 🔒 package-lock.json
│      → Resolved dependency information
│
├── 📦 node_modules
│      → Installed packages
│
├── 📂 src
│      → Application source code
│
├── ⚙️ app.js
│      → Application configuration
│
├── 🚀 server.js
│      → Starts the server
│
├── 🔐 .env
│      → Environment configuration
│
└── 🚫 .gitignore
       → Files Git should ignore
```

### ⭐ Most important professional concept

```text
Request
   ↓
Route
   ↓
Controller
   ↓
Service
   ↓
Model
   ↓
Database
```

You don't need to memorize every folder now. As we build real Node.js applications, each one will become clear through practice.

🛑 **Chapter 3 complete.**

When you're ready, type **NEXT** for **Chapter 4 — npm & Package Management**.