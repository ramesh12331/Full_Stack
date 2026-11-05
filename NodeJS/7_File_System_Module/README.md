# 📁 Chapter 7 — File System (`fs`) Module

### 🔑 Requires Before Starting

Before starting Chapter 7, you should understand:

1. **JavaScript variables and functions**
2. **Basic Node.js**
   ```bash
   node app.js
   ```
3. **Node.js modules**
   ```js
   const something = require("something");
   ```
4. **Chapter 5 — Modules**
5. **Chapter 6 — `path` module**
   ```js
   path.join()
   path.resolve()
   __dirname
   __filename
   ```
6. **Basic file and folder concepts**

### 🎯 What we will learn

```text
fs
│
├── 📖 Reading files
├── ✏️ Writing files
├── ➕ Appending files
├── 🗑️ Deleting files
├── 🔄 Renaming files
├── 📁 Creating directories
│
├── ⏳ Synchronous methods
├── ⚡ Asynchronous methods
├── 📞 Callback style
├── 🤝 Promise style
└── 🚀 fs/promises
```

---

# 1️⃣ What is `fs`?

`fs` means **File System**.

Node.js provides the `fs` module to work with files and directories.

For example, Node.js can:

```text
📖 Read a file
✏️ Write a file
➕ Add content
🗑️ Delete a file
🔄 Rename a file
📁 Create a folder
```

`fs` is a **built-in Node.js module**.

So we don't need:

```bash
npm install fs
```

Instead:

```js
const fs = require("fs");
```

---

# 2️⃣ 🤔 Why do we need `fs`?

Imagine a backend application that needs to create a log:

```text
Application started
User logged in
Order created
Server stopped
```

Node.js can save these messages into:

```text
logs/app.log
```

Similarly, `fs` can work with:

```text
data/users.json
data/products.json
uploads/profile.jpg
logs/server.log
reports/report.txt
```

> 💡 Later, databases such as PostgreSQL and MongoDB will be better for most application data. But file-system operations are still important for logs, files, uploads, configuration, reports, temporary files, etc.

---

# 3️⃣ 🌍 Real-World Analogy

Think about a notebook.

You can:

```text
📖 Read the notebook
✏️ Write something
➕ Add another line
🗑️ Remove something
📁 Create another notebook
```

The `fs` module gives Node.js similar abilities with computer files.

---

# 4️⃣ Import `fs`

## CommonJS

```js
const fs = require("fs");
```

For now, because we are learning CommonJS:

```js
const fs = require("fs");
```

is the syntax we will mainly use.

---

# 5️⃣ 📖 Reading Files

Suppose our project is:

```text
node-project/
│
├── app.js
└── message.txt
```

`message.txt`:

```text
Hello Node.js!
I am learning the File System module.
```

We can read it using:

```js
const fs = require("fs");

fs.readFile(
    "message.txt",
    "utf8",
    (err, data) => {
        if (err) {
            console.log(err);
            return;
        }

        console.log(data);
    }
);
```

### Output

```text
Hello Node.js!
I am learning the File System module.
```

---

# 6️⃣ 🔍 Understanding `readFile()`

```js
fs.readFile(
    "message.txt",
    "utf8",
    (err, data) => {
        // code
    }
);
```

### `"message.txt"`

The file we want to read.

### `"utf8"`

We want the content as readable text.

### `err`

Contains information if something goes wrong.

### `data`

Contains the file content if the operation succeeds.

---

# 7️⃣ 📞 Callback Style

The above example is called **callback style**.

A callback is a function that is passed to another function and executed later.

Here:

```js
(err, data) => {
    // ...
}
```

is the callback.

The flow is:

```text
fs.readFile()
      ↓
Start reading file
      ↓
File operation finishes
      ↓
Callback runs
      ↓
(err, data)
```

---

# 8️⃣ 🔍 Callback Dry Run

Suppose:

```text
message.txt
```

contains:

```text
Hello Node.js
```

Node.js does:

```text
fs.readFile()
     ↓
Open message.txt
     ↓
Read content
     ↓
No error
     ↓
err = null
data = "Hello Node.js"
     ↓
console.log(data)
```

Output:

```text
Hello Node.js
```

---

# 9️⃣ ⚠️ Error Handling

Always handle possible errors.

```js
const fs = require("fs");

fs.readFile(
    "abc.txt",
    "utf8",
    (err, data) => {

        if (err) {
            console.log("Unable to read file");
            return;
        }

        console.log(data);
    }
);
```

If `abc.txt` doesn't exist:

```text
Unable to read file
```

---

# 🔟 ✏️ Writing Files

We use:

```js
fs.writeFile()
```

Example:

```js
const fs = require("fs");

fs.writeFile(
    "message.txt",
    "Hello Node.js",
    (err) => {

        if (err) {
            console.log(err);
            return;
        }

        console.log("File written successfully");
    }
);
```

If `message.txt` doesn't exist:

```text
message.txt
```

will be created.

---

# 1️⃣1️⃣ What happens if the file already exists?

Suppose:

```text
message.txt
```

contains:

```text
Hello
Welcome
```

Now:

```js
fs.writeFile(
    "message.txt",
    "New Content",
    callback
);
```

The old content is replaced.

The file becomes:

```text
New Content
```

### Remember:

```text
writeFile()
     ↓
Create OR replace
```

---

# 1️⃣2️⃣ ➕ Appending Files

If you want to **add content without removing existing content**, use:

```js
fs.appendFile()
```

Example:

```js
const fs = require("fs");

fs.appendFile(
    "message.txt",
    "\nWelcome to Node.js!",
    (err) => {

        if (err) {
            console.log(err);
            return;
        }

        console.log("Content added");
    }
);
```

If the file initially contains:

```text
Hello Node.js
```

After appending:

```text
Hello Node.js
Welcome to Node.js!
```

### Easy memory:

```text
writeFile()
    ↓
replace

appendFile()
    ↓
add
```

---

# 1️⃣3️⃣ 🗑️ Deleting Files

Use:

```js
fs.unlink()
```

Example:

```js
const fs = require("fs");

fs.unlink(
    "message.txt",
    (err) => {

        if (err) {
            console.log(err);
            return;
        }

        console.log("File deleted");
    }
);
```

The file:

```text
message.txt
```

is deleted.

---

# 1️⃣4️⃣ 🔄 Renaming Files

Use:

```js
fs.rename()
```

Example:

```js
const fs = require("fs");

fs.rename(
    "old.txt",
    "new.txt",
    (err) => {

        if (err) {
            console.log(err);
            return;
        }

        console.log("File renamed");
    }
);
```

Before:

```text
old.txt
```

After:

```text
new.txt
```

---

# 1️⃣5️⃣ 📁 Creating Directories

Use:

```js
fs.mkdir()
```

Example:

```js
const fs = require("fs");

fs.mkdir(
    "uploads",
    (err) => {

        if (err) {
            console.log(err);
            return;
        }

        console.log("Directory created");
    }
);
```

Before:

```text
project/
└── app.js
```

After:

```text
project/
├── app.js
└── uploads/
```

---

# 1️⃣6️⃣ ⭐ Using `path` + `fs`

This is an important real-world pattern.

Suppose:

```text
project/
│
├── app.js
│
└── data/
    └── users.txt
```

Use:

```js
const fs = require("fs");
const path = require("path");

const filePath = path.join(
    __dirname,
    "data",
    "users.txt"
);

fs.readFile(
    filePath,
    "utf8",
    (err, data) => {

        if (err) {
            console.log(err);
            return;
        }

        console.log(data);
    }
);
```

### Why use `path`?

Instead of manually writing:

```js
"data/users.txt"
```

we create the complete path:

```js
path.join(
    __dirname,
    "data",
    "users.txt"
);
```

This is especially useful when working with files from different directories.

---

# 1️⃣7️⃣ ⏳ Synchronous Methods

Now an important concept:

> **Synchronous = wait until the operation finishes.**

For example:

```js
fs.readFileSync()
```

Example:

```js
const fs = require("fs");

const data = fs.readFileSync(
    "message.txt",
    "utf8"
);

console.log(data);

console.log("Finished");
```

The order is:

```text
read file
   ↓
wait
   ↓
file completed
   ↓
console.log(data)
   ↓
console.log("Finished")
```

---

# 1️⃣8️⃣ ⚡ Asynchronous Methods

> **Asynchronous = start the operation and continue without waiting for the operation to finish.**

Example:

```js
const fs = require("fs");

fs.readFile(
    "message.txt",
    "utf8",
    (err, data) => {

        if (err) {
            console.log(err);
            return;
        }

        console.log(data);
    }
);

console.log("Finished");
```

You may see:

```text
Finished
Hello Node.js
```

Why?

Because `readFile()` is asynchronous.

---

# 1️⃣9️⃣ 🆚 Synchronous vs Asynchronous

| Synchronous | Asynchronous |
|---|---|
| Waits | Doesn't block waiting |
| `readFileSync()` | `readFile()` |
| Simpler for small scripts | Better suited to server workloads |
| Can block execution | Allows other work to continue |
| Use carefully in servers | Common in Node.js backend code |

### Simple memory trick

```text
SYNC
 ↓
WAIT

ASYNC
 ↓
DON'T WAIT
```

---

# 2️⃣0️⃣ 📞 Callback Style

The traditional asynchronous `fs` API commonly uses callbacks.

Example:

```js
const fs = require("fs");

fs.readFile(
    "message.txt",
    "utf8",
    (err, data) => {

        if (err) {
            console.log(err);
            return;
        }

        console.log(data);
    }
);
```

The callback receives:

```text
err
 ↓
error information

data
 ↓
file content
```

---

# 2️⃣1️⃣ 🤝 Promise Style

Node.js also provides Promise-based APIs.

Promises allow us to write asynchronous code using:

```js
.then()
.catch()
```

For example:

```js
const fs = require("fs").promises;

fs.readFile(
    "message.txt",
    "utf8"
)
.then((data) => {
    console.log(data);
})
.catch((error) => {
    console.log(error);
});
```

### Flow

```text
readFile()
    ↓
Promise
    ↓
.then() → success
.catch() → error
```

---

# 2️⃣2️⃣ 🚀 `fs/promises`

Node.js provides a dedicated Promise-based module:

```js
const fs = require("fs/promises");
```

This is a clean modern approach.

Example:

```js
const fs = require("fs/promises");

async function readFileData() {

    try {

        const data = await fs.readFile(
            "message.txt",
            "utf8"
        );

        console.log(data);

    } catch (error) {

        console.log(error);
    }
}

readFileData();
```

---

# 2️⃣3️⃣ 🧠 Why `fs/promises`?

Compare these styles.

### Callback

```js
fs.readFile(
    "message.txt",
    "utf8",
    (err, data) => {

        if (err) {
            console.log(err);
            return;
        }

        console.log(data);
    }
);
```

### Promise

```js
const fs = require("fs/promises");

fs.readFile(
    "message.txt",
    "utf8"
)
.then((data) => {
    console.log(data);
})
.catch((error) => {
    console.log(error);
});
```

### Async/Await

```js
const fs = require("fs/promises");

async function readFileData() {

    try {

        const data = await fs.readFile(
            "message.txt",
            "utf8"
        );

        console.log(data);

    } catch (error) {

        console.log(error);
    }
}
```

For modern backend development, you will frequently see the **Promise + `async/await`** style.

---

# 2️⃣4️⃣ 📊 Three Styles Compared

| Style | Example | Main idea |
|---|---|---|
| Synchronous | `readFileSync()` | Wait |
| Callback | `readFile()` | Callback after operation |
| Promise | `fs/promises` | Promise + `async/await` |

---

# 2️⃣5️⃣ 🧪 Complete Practical Example

Let's create:

```text
node-fs-practice/
│
├── app.js
│
└── data/
```

Our program will:

```text
1. Create users.txt
2. Write users
3. Read users
4. Add another user
5. Read again
```

### `app.js`

```js
const fs = require("fs/promises");
const path = require("path");

async function main() {

    const filePath = path.join(
        __dirname,
        "data",
        "users.txt"
    );

    try {

        // 1. Write users
        await fs.writeFile(
            filePath,
            "Ramesh\nRahul\nSuresh"
        );

        console.log("Users file created");

        // 2. Read users
        const users = await fs.readFile(
            filePath,
            "utf8"
        );

        console.log("\nUsers:");
        console.log(users);

        // 3. Add another user
        await fs.appendFile(
            filePath,
            "\nKiran"
        );

        console.log("\nNew user added");

        // 4. Read again
        const updatedUsers = await fs.readFile(
            filePath,
            "utf8"
        );

        console.log("\nUpdated Users:");
        console.log(updatedUsers);

    } catch (error) {

        console.log("Error:", error);
    }
}

main();
```

---

# 2️⃣6️⃣ 🔍 Dry Run

The program starts:

```text
main()
 ↓
Create file path
 ↓
writeFile()
 ↓
users.txt created
 ↓
readFile()
 ↓
Display users
 ↓
appendFile()
 ↓
Kiran added
 ↓
readFile()
 ↓
Display updated users
```

Final file:

```text
Ramesh
Rahul
Suresh
Kiran
```

---

# 2️⃣7️⃣ 📝 Line-by-Line Important Parts

### Import Promise-based `fs`

```js
const fs = require("fs/promises");
```

Now `fs.readFile()`, `fs.writeFile()`, etc. return Promises.

### Import `path`

```js
const path = require("path");
```

Used to create a reliable file path.

### Create file path

```js
const filePath = path.join(
    __dirname,
    "data",
    "users.txt"
);
```

Creates:

```text
project/data/users.txt
```

### Write

```js
await fs.writeFile(
    filePath,
    "Ramesh\nRahul\nSuresh"
);
```

Creates or replaces the file.

### Read

```js
const users = await fs.readFile(
    filePath,
    "utf8"
);
```

Reads the file as text.

### Append

```js
await fs.appendFile(
    filePath,
    "\nKiran"
);
```

Adds content without replacing the existing content.

---

# 2️⃣8️⃣ 📋 Important `fs` Methods

| Method | Purpose | Async Callback |
|---|---|---|
| `readFile()` | Read file | ✅ |
| `writeFile()` | Create/replace | ✅ |
| `appendFile()` | Add content | ✅ |
| `unlink()` | Delete file | ✅ |
| `rename()` | Rename/move | ✅ |
| `mkdir()` | Create directory | ✅ |
| `readFileSync()` | Read synchronously | ❌ |

With:

```js
const fs = require("fs/promises");
```

these operations use Promises instead.

---

# 2️⃣9️⃣ ⚠️ Common Mistakes

### ❌ Mistake 1 — Installing `fs`

Don't:

```bash
npm install fs
```

`fs` is built into Node.js.

---

### ❌ Mistake 2 — Confusing `writeFile()` and `appendFile()`

```text
writeFile()
    ↓
Replace

appendFile()
    ↓
Add
```

---

### ❌ Mistake 3 — Forgetting `await`

If using:

```js
const fs = require("fs/promises");
```

and inside an `async` function:

```js
const data = await fs.readFile(
    filePath,
    "utf8"
);
```

Don't forget `await` when you need the resolved result.

---

### ❌ Mistake 4 — Reading a file before its directory exists

If:

```text
data/
```

doesn't exist, this:

```js
fs.readFile("data/users.txt");
```

will fail.

You may need to create the directory first.

---

### ❌ Mistake 5 — Using synchronous methods everywhere

Avoid making a habit of:

```js
fs.readFileSync()
```

for normal server request processing.

Synchronous operations can block the Node.js process.

---

# ✅ 3️⃣0️⃣ Best Practices

### ✔ Use `path.join()`

```js
const filePath = path.join(
    __dirname,
    "data",
    "users.txt"
);
```

### ✔ Handle errors

Callback:

```js
if (err) {
    console.log(err);
    return;
}
```

Promise:

```js
try {
    // operation
} catch (error) {
    console.log(error);
}
```

### ✔ Prefer asynchronous APIs for server applications

Use:

```js
fs.readFile()
```

or:

```js
fs/promises
```

instead of unnecessarily blocking with:

```js
fs.readFileSync()
```

### ✔ Use `async/await` for readable asynchronous code

```js
try {

    const data = await fs.readFile(
        filePath,
        "utf8"
    );

} catch (error) {

    console.log(error);
}
```

---

# 🎯 3️⃣1️⃣ Interview Questions

### 🟢 Beginner

**1. What is the `fs` module?**

It is Node.js's built-in File System module used to work with files and directories.

**2. Do we install `fs` using npm?**

No.

**3. How do you read a file?**

```js
fs.readFile()
```

**4. How do you write a file?**

```js
fs.writeFile()
```

**5. How do you append data?**

```js
fs.appendFile()
```

**6. How do you delete a file?**

```js
fs.unlink()
```

---

### 🟡 Intermediate

**7. What is the difference between synchronous and asynchronous file operations?**

Synchronous operations block until they finish. Asynchronous operations allow the Node.js process to continue handling other work while the file operation completes.

**8. What is a callback in `fs.readFile()`?**

It is a function executed after the asynchronous file operation completes.

```js
(err, data) => {
    // result
}
```

**9. What is `fs/promises`?**

It is the Promise-based File System API, which works well with `async/await`.

---

### 🔴 Advanced

**10. Why are asynchronous file operations important in Node.js?**

Node.js is designed around non-blocking I/O. Avoiding unnecessary synchronous file operations helps the process remain responsive while handling other work.

**11. When might a synchronous operation be acceptable?**

Small startup scripts, simple command-line utilities, or initialization code can sometimes use synchronous operations when the blocking behavior is intentional and limited.

---

# 🧩 3️⃣2️⃣ Practice Problems

### Task 1 — Write

Create:

```text
student.txt
```

with:

```text
Name: Ramesh
Course: Node.js
```

---

### Task 2 — Read

Read `student.txt` using:

```js
fs.readFile()
```

---

### Task 3 — Append

Add:

```text
Experience: Full Stack Development
```

---

### Task 4 — Rename

Rename:

```text
student.txt
```

to:

```text
student-info.txt
```

---

### Task 5 — Delete

Delete:

```text
student-info.txt
```

using:

```js
fs.unlink()
```

---

# 🚀 3️⃣3️⃣ Mini Challenge

Build this project:

```text
node-fs-project/
│
├── app.js
│
├── data/
│   └── users.txt
│
└── logs/
    └── app.log
```

Your `app.js` should:

```text
1️⃣ Create data/ if necessary
2️⃣ Create users.txt
3️⃣ Write 3 users
4️⃣ Read users.txt
5️⃣ Append a 4th user
6️⃣ Create logs/
7️⃣ Create app.log
8️⃣ Write "Application started"
9️⃣ Read app.log
```

Try to implement it using:

```js
const fs = require("fs/promises");
const path = require("path");
```

and:

```js
async/await
```

---

# 📌 3️⃣4️⃣ Chapter Summary

You learned the complete beginner foundation of Node.js File System operations:

```text
                 fs
                  │
        ┌─────────┴─────────┐
        ↓                   ↓
    Synchronous        Asynchronous
        │                   │
 readFileSync()       readFile()
                        │
                  ┌─────┴─────┐
                  ↓           ↓
              Callback     Promise
                              │
                         fs/promises
                              │
                         async/await
```

### File operations:

```text
📖 readFile()
✏️ writeFile()
➕ appendFile()
🗑️ unlink()
🔄 rename()
📁 mkdir()
```

### Three styles to remember:

```text
1. Synchronous
   readFileSync()

2. Callback
   fs.readFile(..., callback)

3. Promise
   fs/promises + async/await
```

---

# ⚡ 3️⃣5️⃣ Quick Revision

```text
fs
 ↓
File System

readFile()
 ↓
Read

writeFile()
 ↓
Create / Replace

appendFile()
 ↓
Add

unlink()
 ↓
Delete

rename()
 ↓
Rename

mkdir()
 ↓
Create directory

readFileSync()
 ↓
Synchronous / blocking

fs/promises
 ↓
Promise-based API

async/await
 ↓
Clean asynchronous code
```

## 🛑 Chapter 7 Complete

**Next → Chapter 8 — Node.js `os` Module**

We will learn how Node.js gets information about the operating system, CPU, memory, platform, architecture, hostname, and more.

👉 Type **`NEXT`** when you're ready.