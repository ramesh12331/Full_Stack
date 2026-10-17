# 📘 Chapter 2 — React Environment Setup

Now we move to **Chapter 2 — React Environment Setup**.

This chapter is important because before writing React code, you need to understand **what tools are required, why they are required, and how a React project is created and run**.

---

# 1. What is React Environment Setup?

React itself is a JavaScript library, but when we develop a real React application, we normally use several development tools.

A typical setup looks like:

```text
VS Code
   ↓
Node.js
   ↓
npm
   ↓
Vite
   ↓
React Project
   ↓
Development Server
   ↓
Browser
```

We will understand each one.

---

# 2. What is Node.js? 🟢

### Simple definition

**Node.js allows JavaScript to run outside the browser.**

Normally, JavaScript runs inside a browser:

```text
JavaScript
    ↓
Chrome / Edge / Firefox
    ↓
Browser
```

With Node.js:

```text
JavaScript
    ↓
Node.js
    ↓
Operating System
```

React development tools use Node.js.

For example, commands such as:

```bash
npm install
npm run dev
npm run build
```

are executed through the Node.js ecosystem.

---

# 3. Why do we need Node.js for React?

You may wonder:

> "If React runs in the browser, why do I need Node.js?"

Good question.

During development, we need tools for:

- installing packages
- running the development server
- processing/building application files
- managing dependencies
- creating production builds

Node.js provides the runtime required by these development tools.

### Important

Node.js is **not the React library**.

Think:

```text
Node.js
   ↓
Development environment

React
   ↓
UI library
```

---

# 4. Check Node.js Installation

Open **VS Code → Terminal**.

You can also use Command Prompt or PowerShell.

Run:

```bash
node --version
```

or:

```bash
node -v
```

Example:

```text
v22.x.x
```

The exact version may differ on your computer.

Now check npm:

```bash
npm --version
```

Example:

```text
10.x.x
```

Again, your version can be different.

---

# 5. What is npm? 📦

**npm** stands for **Node Package Manager**.

It is used to manage JavaScript packages.

For example, if your application needs React, npm can install it.

```bash
npm install react
```

You can think of npm as a package manager:

```text
Your Project
     ↓
npm
     ↓
Download packages
     ↓
node_modules
```

---

# 6. What is a Package?

A package is reusable code created and distributed so developers can use it in their projects.

For example:

```text
react
react-dom
react-router-dom
axios
redux
```

Instead of writing everything ourselves, we can install existing packages.

Example:

```bash
npm install axios
```

Then our project can use Axios.

---

# 7. What is npx?

You will commonly see:

```bash
npm
```

and:

```bash
npx
```

They are different.

### npm

Mainly used to manage packages.

Example:

```bash
npm install react
```

### npx

Used to execute a package/tool.

For example:

```bash
npx ...
```

Think:

```text
npm
 ↓
Install/manage packages

npx
 ↓
Run a package/tool
```

Modern React projects commonly use **Vite** for project creation rather than the older Create React App workflow.

---

# 8. What is VS Code? 💻

**Visual Studio Code** is a code editor.

You can use it to:

- write React code
- create files
- manage folders
- use terminal
- install extensions
- debug code
- work with Git

Your basic development environment can be:

```text
VS Code
│
├── React code
├── Terminal
├── Files
└── Extensions
```

---

# 9. What is Vite? ⚡

This is one of the most important concepts in modern React development.

**Vite is a frontend build tool and development tool.**

It provides:

- project scaffolding
- development server
- fast development workflow
- production build

In simple terms:

> **Vite helps us create, run, and build modern React applications.**

---

# 10. Why do we use Vite?

Imagine manually setting up everything:

```text
React
Babel
Development server
Build configuration
Package configuration
```

That would be inconvenient for beginners.

Vite gives us a convenient project setup.

For example:

```bash
npm create vite@latest
```

Then we select React.

---

# 11. Create Your First React Project 🚀

Open your VS Code terminal.

Run:

```bash
npm create vite@latest
```

Vite will ask questions.

You can choose:

```text
Project name:
react-demo

Select a framework:
React

Select a variant:
JavaScript
```

Your project will then be created.

---

# 12. Alternative: Create Directly

You can also use:

```bash
npm create vite@latest react-demo
```

Then choose:

```text
React
```

and:

```text
JavaScript
```

For your current learning, I recommend:

```text
React
+
JavaScript
```

rather than TypeScript.

We can learn TypeScript later.

---

# 13. Complete Setup Flow

After creating the project:

```bash
cd react-demo
```

Then install dependencies:

```bash
npm install
```

Then start the development server:

```bash
npm run dev
```

The general flow is:

```text
1. Create project
       ↓
2. cd react-demo
       ↓
3. npm install
       ↓
4. npm run dev
       ↓
5. Open browser
```

---

# 14. What does `cd` mean?

`cd` means:

> **Change Directory**

Suppose your terminal is currently here:

```text
C:\Users\Ramesh>
```

You create:

```text
react-demo
```

Then:

```bash
cd react-demo
```

means:

```text
Go inside the react-demo folder
```

---

# 15. What does `npm install` do?

When Vite creates the project, your project contains a `package.json`.

That file tells npm which dependencies the project needs.

When you run:

```bash
npm install
```

npm reads the dependency information and installs the required packages.

They are stored mainly inside:

```text
node_modules/
```

So:

```text
package.json
      ↓
npm install
      ↓
node_modules
```

---

# 16. What does `npm run dev` do?

This command starts the development server.

```bash
npm run dev
```

You will normally see something similar to:

```text
VITE ready

Local:
http://localhost:5173/
```

The exact port may vary if another application is already using the default port.

---

# 17. What is `localhost`?

`localhost` means:

> **Your own computer.**

For example:

```text
http://localhost:5173
```

means:

```text
Your computer
     ↓
Port 5173
     ↓
React development server
```

It is not automatically a public website.

---

# 18. What is a Port? 🔌

A port is like a numbered entry point used by network applications.

For example:

```text
localhost:5173
```

contains:

```text
localhost
    ↓
Your computer

5173
    ↓
Port
```

You may see different ports such as:

```text
5173
5174
3000
8000
```

depending on the application.

---

# 19. Vite Development Server

When you execute:

```bash
npm run dev
```

the flow is:

```text
VS Code Terminal
       ↓
npm run dev
       ↓
Vite
       ↓
Development Server
       ↓
localhost:5173
       ↓
Browser
       ↓
React Application
```

This is an important flow to remember.

---

# 20. Your First React Project Structure 📁

After creating the Vite React project, you will see something similar to:

```text
react-demo/
│
├── node_modules/
├── public/
│
├── src/
│   ├── assets/
│   ├── App.css
│   ├── App.jsx
│   ├── index.css
│   └── main.jsx
│
├── .gitignore
├── eslint.config.js
├── index.html
├── package.json
├── package-lock.json
└── vite.config.js
```

Don't worry if your exact generated files differ slightly between Vite versions/templates.

We will study the project structure in **Chapter 3**.

---

# 21. What is `package.json`?

This is one of the most important files in a JavaScript project.

Example:

```json
{
    "name": "react-demo",
    "scripts": {
        "dev": "vite",
        "build": "vite build"
    }
}
```

It contains project information and dependencies/scripts.

For example:

```bash
npm run dev
```

looks at the project's scripts and executes the configured `dev` command.

---

# 22. What is `node_modules`?

`node_modules` contains installed packages.

For example:

```text
node_modules/
│
├── react/
├── react-dom/
├── vite/
└── ...
```

### Important rule

Usually, you **do not manually edit files inside `node_modules`**.

If dependencies need to be installed:

```bash
npm install
```

npm manages them.

---

# 23. What is `package-lock.json`?

When npm installs dependencies, it creates:

```text
package-lock.json
```

It records detailed information about installed dependency versions and their dependency tree.

This helps make installations more consistent across environments.

---

# 24. What is `index.html`?

A Vite React project has an HTML entry point.

Simplified:

```html
<!doctype html>

<html>
    <head>
        <title>React App</title>
    </head>

    <body>
        <div id="root"></div>

        <script type="module" src="/src/main.jsx"></script>
    </body>
</html>
```

Notice:

```html
<div id="root"></div>
```

This is important.

React will render the application into this root element.

We will understand the complete flow in Chapter 3.

---

# 25. What is `main.jsx`?

A typical Vite React application has:

```text
src/main.jsx
```

It connects the React application to the HTML root.

A simplified example:

```jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App.jsx";

createRoot(document.getElementById("root")).render(
    <StrictMode>
        <App />
    </StrictMode>
);
```

Don't worry if you don't understand everything here yet.

For now, remember:

```text
index.html
     ↓
root
     ↓
main.jsx
     ↓
App.jsx
     ↓
React UI
```

---

# 26. What is `App.jsx`?

`App.jsx` is commonly used as the main application component.

Example:

```jsx
function App() {

    return (
        <h1>Hello React</h1>
    );

}

export default App;
```

Then:

```text
App.jsx
   ↓
App component
   ↓
UI
```

---

# 27. Complete Application Flow 🔥

This is one of the most important things in this chapter.

Remember:

```text
Browser
   ↓
index.html
   ↓
<div id="root">
   ↓
main.jsx
   ↓
<App />
   ↓
App.jsx
   ↓
React Components
   ↓
UI
```

Later, when you learn API integration:

```text
User
 ↓
React UI
 ↓
Event
 ↓
API request
 ↓
Backend
 ↓
Database
 ↓
Response
 ↓
React state
 ↓
Updated UI
```

This will become the foundation for your full-stack React applications.

---

# 28. Production Build

During development we use:

```bash
npm run dev
```

For production, we usually create a production build:

```bash
npm run build
```

The build process prepares the application for deployment.

Typical flow:

```text
Development
    ↓
npm run dev
    ↓
Write/test application
    ↓
npm run build
    ↓
Production files
    ↓
Deploy
```

We will study production builds and deployment in later chapters.

---

# 29. Development vs Production

### Development

```bash
npm run dev
```

Used while developing.

```text
Developer
   ↓
Edit code
   ↓
Save
   ↓
Browser updates
```

### Production

```bash
npm run build
```

Used to generate optimized production assets.

```text
Source code
    ↓
Build process
    ↓
Production assets
    ↓
Deploy
```

---

# 30. Create → Run → Build

Remember this simple formula:

```text
CREATE
   ↓
npm create vite@latest
   ↓
INSTALL
   ↓
npm install
   ↓
RUN
   ↓
npm run dev
   ↓
BUILD
   ↓
npm run build
```

⭐ This is worth memorizing.

---

# 31. Dry Run 🔍

Suppose you run:

```bash
npm create vite@latest react-demo
```

### Step 1

Vite asks for the project configuration.

```text
Framework → React
Variant   → JavaScript
```

### Step 2

Project created:

```text
react-demo/
```

### Step 3

Enter project:

```bash
cd react-demo
```

### Step 4

Install dependencies:

```bash
npm install
```

### Step 5

Start development:

```bash
npm run dev
```

### Step 6

Vite starts its development server.

Example:

```text
http://localhost:5173/
```

### Step 7

Open the address in your browser.

### Step 8

React application appears.

---

# 32. Common Mistakes ❌

## Mistake 1 — Node.js not installed

You may get something like:

```text
'node' is not recognized...
```

Check:

```bash
node -v
```

If Node.js is not installed, install a current supported Node.js release from the official Node.js website.

---

## Mistake 2 — Running npm commands outside the project

For example:

```bash
npm run dev
```

should normally be executed from the project directory containing `package.json`.

Correct:

```text
react-demo/
   package.json
```

Terminal:

```bash
cd react-demo
npm run dev
```

---

## Mistake 3 — Forgetting `npm install`

If dependencies aren't installed:

```bash
npm run dev
```

may fail.

Run:

```bash
npm install
```

first.

---

## Mistake 4 — Port already being used

You may see Vite choose another port.

For example:

```text
5173
```

is busy, so Vite may use:

```text
5174
```

This is not necessarily an error.

---

# 33. Best Practices ⭐

### ✅ Use Vite for new React projects

For your learning and new projects, use:

```bash
npm create vite@latest
```

### ✅ Use VS Code

Keep your project organized.

### ✅ Don't edit `node_modules`

Let npm manage dependencies.

### ✅ Understand your commands

Don't just copy:

```bash
npm run dev
```

Understand what it does.

### ✅ Keep your project folder organized

Later we'll use structures such as:

```text
src/
├── components/
├── pages/
├── hooks/
├── services/
├── assets/
└── App.jsx
```

---

# 34. Interview Questions 🎯

### Beginner

**Q1. What is Node.js?**

> Node.js is a JavaScript runtime that allows JavaScript to run outside the browser.

---

**Q2. What is npm?**

> npm is the Node Package Manager used to install and manage JavaScript packages and project dependencies.

---

**Q3. What is npx?**

> npx is a tool used to execute packages/commands, often without requiring a separate global installation.

---

**Q4. What is Vite?**

> Vite is a modern frontend development and build tool commonly used to create and run React applications.

---

### Intermediate

**Q5. What does `npm install` do?**

> It installs the dependencies specified by the project's package configuration.

---

**Q6. What does `npm run dev` do?**

> It runs the development script defined in `package.json`, which commonly starts the Vite development server.

---

**Q7. What is localhost?**

> `localhost` refers to the local computer on which the application is running.

---

### Advanced

**Q8. What is the difference between development and production builds?**

> Development mode is optimized for building and debugging the application, while a production build prepares optimized assets for deployment.

---

# 35. Practice Questions 📝

Try answering these yourself:

### Practice 1

What is the difference between:

```text
Node.js
React
Vite
npm
```

### Practice 2

What does this command do?

```bash
npm install
```

### Practice 3

What does this command do?

```bash
npm run dev
```

### Practice 4

What is the purpose of:

```text
package.json
```

### Practice 5

What is `localhost:5173`?

---

# 36. Mini Challenge 💪

Create a React project yourself.

### Step 1

Open VS Code.

### Step 2

Open Terminal.

### Step 3

Run:

```bash
npm create vite@latest react-learning
```

### Step 4

Select:

```text
React
```

### Step 5

Select:

```text
JavaScript
```

### Step 6

Run:

```bash
cd react-learning
```

### Step 7

Run:

```bash
npm install
```

### Step 8

Run:

```bash
npm run dev
```

### Step 9

Open the displayed localhost URL.

---

## 🧠 Your task

Before looking at the answer, try to explain this flow:

```text
npm create vite@latest
        ↓
    React project
        ↓
    npm install
        ↓
    npm run dev
        ↓
   Vite server
        ↓
     Browser
```

If you understand this flow, you have understood the main purpose of this chapter.

---

# 37. Chapter Summary 📚

| Tool | Purpose |
|---|---|
| **Node.js** | JavaScript runtime used by development tools |
| **npm** | Package/dependency manager |
| **npx** | Executes packages/commands |
| **VS Code** | Code editor |
| **Vite** | Development/build tool |
| **localhost** | Your local computer |
| **Port** | Network entry point |
| **package.json** | Project metadata, scripts, dependencies |
| **node_modules** | Installed packages |
| **npm install** | Installs dependencies |
| **npm run dev** | Starts development server |
| **npm run build** | Creates production build |

---

# 🔄 Quick Revision

```text
                    React Development
                           │
                           ↓
                         Node.js
                           │
                           ↓
                          npm
                           │
                           ↓
                         Vite
                           │
                           ↓
                    React Project
                           │
              ┌────────────┴────────────┐
              ↓                         ↓
        npm run dev              npm run build
              ↓                         ↓
       Development                 Production
         Server                       Build
              ↓                         ↓
          Browser                    Deploy
```

### ⭐ Most important commands

```bash
# Create React project
npm create vite@latest

# Enter project
cd project-name

# Install dependencies
npm install

# Start development server
npm run dev

# Create production build
npm run build
```

**Chapter 2 complete.** 🛑

Type **`NEXT`** when you're ready for **Chapter 3 — React Project Structure**, where we'll open the project and understand **`src`, `public`, `package.json`, `node_modules`, `index.html`, `main.jsx`, `App.jsx` and the complete React startup flow**.