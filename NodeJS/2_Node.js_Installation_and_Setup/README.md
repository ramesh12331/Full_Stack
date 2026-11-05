# 🚀 CHAPTER 2 — Node.js Installation and Setup

In Chapter 2, we will prepare your computer for Node.js development.

We will learn:

1. 📦 Installing Node.js
2. 🟢 LTS version
3. 🔢 Node.js version
4. 📦 npm
5. ⚡ npx
6. 💻 VS Code
7. ⌨️ Terminal
8. 🔍 Checking Node version
9. 🔍 Checking npm version
10. ▶️ Running `.js` files
11. `node app.js`
12. 🧪 Node REPL
13. 📁 Creating a Node.js project

---

# 1️⃣ What is Node.js Installation?

Before writing Node.js programs, we need to install **Node.js** on our computer.

When Node.js is installed, we get important tools such as:

```text
Node.js
   │
   ├── node
   │
   ├── npm
   │
   └── npx
```

### Simple idea

```text
Your JavaScript file
        ↓
      Node.js
        ↓
    JavaScript runs
        ↓
      Output
```

For example:

```javascript
console.log("Hello Node.js");
```

Node.js allows us to execute this JavaScript outside the browser.

---

# 2️⃣ Installing Node.js

Go to the official Node.js website and download Node.js.

[Node.js Official Website](https://nodejs.org/?utm_source=chatgpt.com)

You will normally see versions such as:

```text
LTS
Current
```

For learning and professional backend development, **LTS** is generally the safest choice.

---

# 3️⃣ 🟢 What is LTS?

**LTS = Long Term Support**

It means the version is intended to receive long-term maintenance and stability.

Think of it like this:

```text
Current
   ↓
Newest features
   ↓
May change more frequently

LTS
   ↓
Stable
   ↓
Long-term support
   ↓
Recommended for most projects
```

### Beginner rule

👉 When installing Node.js for learning/backend development, choose **LTS** unless a project specifically requires another version.

---

# 4️⃣ 🔢 What is Node.js Version?

After installing Node.js, we can check its version.

Open your terminal and type:

```bash
node -v
```

or:

```bash
node --version
```

Example:

```text
v24.x.x
```

The exact version on your computer may be different.

### What does `v24.x.x` mean?

It represents the installed Node.js version.

```text
v24.1.0
│  │ │
│  │ └── patch
│  └──── minor
└─────── major
```

You don't need to memorize version numbering now.

---

# 5️⃣ 📦 What is npm?

**npm = Node Package Manager**

npm comes with Node.js.

Its main job is to help us manage packages/libraries for our projects.

For example, later we may install:

```text
express
mongoose
cors
dotenv
jsonwebtoken
bcrypt
```

We can install packages using npm.

Example:

```bash
npm install express
```

---

## Why do we need npm?

Suppose you are building a Node.js backend.

You need Express.

Instead of manually downloading Express files, npm can install it:

```bash
npm install express
```

Flow:

```text
Your Project
     ↓
    npm
     ↓
Download package
     ↓
 Express
     ↓
Use Express in project
```

---

# 6️⃣ ⚡ What is npx?

`npx` is another command-line tool that comes with modern npm installations.

It is mainly used to **execute packages/commands**, often without needing to install the command globally.

For example, later you may see commands like:

```bash
npx some-command
```

### Simple difference

| Tool | Main purpose |
|---|---|
| `node` | Run JavaScript |
| `npm` | Manage packages |
| `npx` | Execute packages/commands |

Remember:

```text
node → Run JS

npm → Install/manage packages

npx → Execute package commands
```

---

# 7️⃣ 💻 What is VS Code?

**VS Code = Visual Studio Code**

It is a code editor that we can use to write Node.js applications.

You can download it from Microsoft's official website.

[Visual Studio Code](https://code.visualstudio.com/?utm_source=chatgpt.com)

We will use VS Code for:

- Writing JavaScript
- Creating Node.js projects
- Opening the terminal
- Running Node.js commands
- Debugging
- Managing project files

---

# 8️⃣ ⌨️ What is Terminal?

The terminal allows us to communicate with the computer using commands.

For example:

```bash
node -v
```

```bash
npm -v
```

```bash
node app.js
```

Instead of clicking buttons, we type commands.

### Example

```text
You
 ↓
Terminal
 ↓
node app.js
 ↓
Node.js
 ↓
Execute app.js
 ↓
Output
```

---

# 9️⃣ 🔍 Check Node.js Version

Open VS Code.

Then open the terminal:

```text
Terminal → New Terminal
```

You can also use the shortcut:

```text
Ctrl + `
```

Then type:

```bash
node -v
```

Example:

```text
v24.1.0
```

If you see a version number, Node.js is installed correctly.

---

# 🔟 🔍 Check npm Version

Run:

```bash
npm -v
```

Example:

```text
11.x.x
```

Again, your exact version may be different.

### Important

You don't need the exact same version shown in examples.

What matters is that the commands work.

---

# 1️⃣1️⃣ ▶️ Running a `.js` File

Now let's create our first Node.js program.

Create a folder:

```text
node-learning
```

Open this folder in VS Code.

Create:

```text
app.js
```

Inside `app.js`:

```javascript
console.log("Hello Node.js");
```

Your project:

```text
node-learning/
│
└── app.js
```

---

# 1️⃣2️⃣ Run `app.js`

Open the terminal inside the project folder.

Run:

```bash
node app.js
```

Output:

```text
Hello Node.js
```

🎉 Congratulations!

You have executed your first Node.js program.

---

# 🧠 Understand `node app.js`

This command:

```bash
node app.js
```

has two important parts:

```text
node     app.js
 │          │
 │          └── JavaScript file
 │
 └── Node.js runtime
```

Meaning:

> "Node, please execute the JavaScript code inside `app.js`."

---

# 🔄 Dry Run

Our code:

```javascript
console.log("Hello Node.js");
```

Command:

```bash
node app.js
```

### Step-by-step

```text
Step 1
↓
Terminal receives:
node app.js

Step 2
↓
Node.js starts

Step 3
↓
Node.js reads app.js

Step 4
↓
console.log() executes

Step 5
↓
Output:
Hello Node.js
```

---

# 1️⃣3️⃣ 🧪 What is Node REPL?

REPL allows us to execute JavaScript directly in the terminal.

REPL means:

```text
R → Read
E → Evaluate
P → Print
L → Loop
```

Run:

```bash
node
```

You may see something similar to:

```text
Welcome to Node.js
>
```

Now type:

```javascript
2 + 3
```

Output:

```text
5
```

Try:

```javascript
10 * 5
```

Output:

```text
50
```

Try:

```javascript
console.log("Hello")
```

Output:

```text
Hello
undefined
```

The `undefined` is related to the return value of `console.log()` and is normal in the REPL.

---

# 🛑 Exit Node REPL

You can type:

```javascript
.exit
```

Or press:

```text
Ctrl + C
```

twice.

Then you return to your normal terminal.

---

# 1️⃣4️⃣ 📁 Creating a Node.js Project

Now let's create a proper Node.js project.

Create a folder:

```text
my-node-app
```

Open it in VS Code.

Open terminal:

```text
Terminal → New Terminal
```

Run:

```bash
npm init
```

npm will ask several questions.

You can accept the default values by pressing:

```text
Enter
```

At the end, npm creates:

```text
package.json
```

Your project becomes:

```text
my-node-app/
│
├── package.json
│
└── app.js
```

---

# ⭐ `package.json`

We will study `package.json` deeply in **Chapter 3**.

For now, remember:

> `package.json` is an important configuration file for a Node.js project.

It contains information such as:

```text
Project name
Version
Scripts
Dependencies
Other project information
```

Don't worry if you don't understand all of it yet.

---

# 1️⃣5️⃣ `npm init -y`

There is a faster way to create `package.json`.

Instead of:

```bash
npm init
```

you can use:

```bash
npm init -y
```

`-y` automatically accepts the default answers.

So:

```bash
npm init -y
```

creates `package.json` quickly.

---

# 🧪 Complete Beginner Practice

Let's do everything together.

## STEP 1 — Create folder

```text
node-practice
```

## STEP 2 — Open in VS Code

```text
File → Open Folder
```

Select:

```text
node-practice
```

## STEP 3 — Open terminal

```text
Terminal → New Terminal
```

## STEP 4 — Check Node

```bash
node -v
```

## STEP 5 — Check npm

```bash
npm -v
```

## STEP 6 — Create project

```bash
npm init -y
```

## STEP 7 — Create file

```text
app.js
```

## STEP 8 — Write code

```javascript
console.log("My first Node.js application");
```

## STEP 9 — Run

```bash
node app.js
```

Expected output:

```text
My first Node.js application
```

---

# 🧩 Important Commands

Keep these commands in your notes:

```bash
# Check Node.js version
node -v

# Check npm version
npm -v

# Start Node REPL
node

# Create package.json interactively
npm init

# Create package.json with defaults
npm init -y

# Run JavaScript file
node app.js
```

---

# ⚠️ Common Beginner Mistakes

### ❌ Mistake 1 — Typing `node app.js` in the wrong folder

Suppose your file is:

```text
D:\Projects\node-practice\app.js
```

But your terminal is somewhere else.

Then:

```bash
node app.js
```

may produce an error because Node cannot find the file.

### Check your current folder

In Windows terminal:

```bash
dir
```

Make sure you can see:

```text
app.js
```

---

### ❌ Mistake 2 — Wrong filename

You created:

```text
app.js
```

but run:

```bash
node server.js
```

Node cannot find `server.js`.

Use:

```bash
node app.js
```

---

### ❌ Mistake 3 — Node is not installed

If:

```bash
node -v
```

doesn't work, Node.js may not be installed correctly or may not be available in your PATH.

---

### ❌ Mistake 4 — Confusing npm and node

Don't confuse:

```bash
node app.js
```

with:

```bash
npm app.js
```

For running JavaScript:

```bash
node app.js
```

For managing packages:

```bash
npm install express
```

---

# 🎯 Interview Questions

### Beginner

**1. What is Node.js?**

Node.js is a JavaScript runtime that allows JavaScript to run outside the browser.

---

**2. What is npm?**

npm is the Node Package Manager used to manage packages and dependencies.

---

**3. What is npx?**

npx is used to execute packages/commands, commonly without requiring a global installation.

---

**4. What is LTS?**

LTS means Long Term Support. It refers to a version intended for long-term stability and maintenance.

---

**5. How do you check the Node.js version?**

```bash
node -v
```

---

**6. How do you check npm version?**

```bash
npm -v
```

---

**7. How do you run a JavaScript file using Node.js?**

```bash
node app.js
```

---

**8. What is Node REPL?**

REPL allows us to interactively execute JavaScript directly from the Node.js terminal.

---

**9. How do you create `package.json`?**

```bash
npm init
```

or:

```bash
npm init -y
```

---

# 🧠 Quick Revision

```text
Node.js
   ↓
Runs JavaScript outside browser

LTS
   ↓
Long Term Support

node
   ↓
Runs JavaScript

npm
   ↓
Manages packages

npx
   ↓
Executes packages/commands

VS Code
   ↓
Code editor

Terminal
   ↓
Run commands

node -v
   ↓
Node version

npm -v
   ↓
npm version

node app.js
   ↓
Run app.js

node
   ↓
Node REPL

npm init -y
   ↓
Create package.json
```

---

# 🏁 Chapter 2 Summary

You now know how to:

- ✅ Install Node.js
- ✅ Understand LTS
- ✅ Check Node.js version
- ✅ Understand npm
- ✅ Understand npx
- ✅ Use VS Code
- ✅ Use the terminal
- ✅ Run `.js` files
- ✅ Use `node app.js`
- ✅ Use Node REPL
- ✅ Create a Node.js project
- ✅ Create `package.json` using `npm init`

### 🔥 Your practice task

Create this project yourself:

```text
node-chapter-2/
│
├── app.js
└── package.json
```

`app.js`:

```javascript
console.log("Hello, I am learning Node.js");
console.log("This is Chapter 2");
```

Run:

```bash
node app.js
```

Expected:

```text
Hello, I am learning Node.js
This is Chapter 2
```

**STOP HERE.** 🛑

When you are ready, type **NEXT** and we will start **Chapter 3 — Node.js Project Structure**, including `package.json`, `package-lock.json`, `node_modules`, `src`, `app.js`, `server.js`, `.env`, `.gitignore`, and a professional backend folder structure.