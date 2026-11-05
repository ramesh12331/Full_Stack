# 📁 Chapter 6 — Node.js `path` Module

> 🎯 **Goal:** Learn how Node.js works with file and folder paths.  
> We will focus on `path`, `path.join()`, `path.resolve()`, `path.basename()`, `path.dirname()`, `path.extname()`, `__dirname`, and `__filename`.

---

## 🔑 Requires Before Starting

Before learning this chapter, you should know these basics:

1. **JavaScript variables**
   ```js
   const name = "Ramesh";
   ```

2. **JavaScript functions**
   ```js
   function add(a, b) {
       return a + b;
   }
   ```

3. **Basic Node.js**
   ```bash
   node app.js
   ```

4. **Node.js modules**
   ```js
   const something = require("something");
   ```

5. **Basic file and folder concepts**

   Example:

   ```text
   project/
   ├── app.js
   ├── data/
   │   └── users.json
   └── uploads/
       └── photo.jpg
   ```

6. **Chapter 5 — Modules**

   We will use `require()` to import Node.js's built-in `path` module.

---

# 1️⃣ What is `path`?

`path` is a **built-in Node.js module** used to work with **file and folder paths**.

You don't need to install it.

```js
const path = require("path");
```

### Simple meaning

Suppose your project has:

```text
my-project/
    app.js
    data/
        users.json
```

Node.js needs to know:

> "Where exactly is `users.json`?"

The `path` module helps us create and understand these paths safely.

---

# 2️⃣ 🤔 Why do we need `path`?

Imagine writing:

```js
const file = "data/users.json";
```

This may work in some situations, but real applications often have:

- different folders
- nested folders
- uploaded files
- images
- PDFs
- JSON files
- database backup files
- configuration files

Instead of manually creating paths, we can use:

```js
path.join()
```

For example:

```js
const filePath = path.join("data", "users.json");

console.log(filePath);
```

Output:

```text
data\users.json
```

On another operating system, Node.js can use the appropriate path separator.

So `path` makes our code **safer and more portable**.

---

# 3️⃣ 🌍 Real-World Analogy

Think about a physical address:

```text
India
  ↓
Telangana
  ↓
Hyderabad
  ↓
Madhapur
  ↓
Office
```

A computer file path is similar:

```text
project
  ↓
uploads
  ↓
images
  ↓
profile.jpg
```

The `path` module helps Node.js correctly construct and understand this address.

---

# 4️⃣ Import the `path` Module

Create:

```text
app.js
```

Write:

```js
const path = require("path");

console.log(path);
```

Run:

```bash
node app.js
```

`path` contains many useful functions.

The important ones for beginners are:

```text
path.join()
path.resolve()
path.basename()
path.dirname()
path.extname()
```

---

# 5️⃣ `path.join()`

## 📖 What is `path.join()`?

`path.join()` combines multiple path parts into one path.

### Syntax

```js
path.join(path1, path2, path3, ...)
```

### Example

```js
const path = require("path");

const filePath = path.join("data", "users.json");

console.log(filePath);
```

Output on Windows:

```text
data\users.json
```

---

## 🔍 Dry Run

This:

```js
path.join("data", "users.json");
```

means:

```text
data
 +
users.json
 =
data/users.json
```

Node.js creates the correct path.

---

# 6️⃣ `path.join()` with Multiple Folders

```js
const path = require("path");

const filePath = path.join(
    "project",
    "uploads",
    "images",
    "profile.jpg"
);

console.log(filePath);
```

Result:

```text
project\uploads\images\profile.jpg
```

This is very useful in backend applications.

---

# 7️⃣ Real-World Example — Upload Folder

Suppose your application has:

```text
my-app/
├── app.js
└── uploads/
    └── profile.jpg
```

We can create the path:

```js
const path = require("path");

const imagePath = path.join("uploads", "profile.jpg");

console.log(imagePath);
```

Output:

```text
uploads\profile.jpg
```

---

# 8️⃣ `path.resolve()`

## 📖 What is `path.resolve()`?

`path.resolve()` creates an **absolute path**.

### Syntax

```js
path.resolve(path1, path2, ...)
```

Example:

```js
const path = require("path");

const filePath = path.resolve("data", "users.json");

console.log(filePath);
```

You may get something similar to:

```text
C:\Users\Ramesh\project\data\users.json
```

The exact path depends on where your project is located.

---

## 🆚 `join()` vs `resolve()`

### `path.join()`

Creates/combines a path:

```js
path.join("data", "users.json");
```

Result:

```text
data\users.json
```

### `path.resolve()`

Creates an absolute path:

```js
path.resolve("data", "users.json");
```

Result:

```text
C:\project\data\users.json
```

### Easy memory trick

```text
join()     → combine paths
resolve()  → absolute path
```

---

# 9️⃣ `path.basename()`

## 📖 What is `basename()`?

`path.basename()` returns the **last part of a path**.

Example:

```js
const path = require("path");

const filePath = "/project/uploads/profile.jpg";

console.log(path.basename(filePath));
```

Output:

```text
profile.jpg
```

### Think:

```text
/project/uploads/profile.jpg
                    ↑
                 basename
```

---

## 🧪 Example

```js
const path = require("path");

const filePath = "C:/projects/node/uploads/photo.png";

const fileName = path.basename(filePath);

console.log(fileName);
```

Output:

```text
photo.png
```

### Real-world use

When a user uploads:

```text
C:/fake/path/profile.jpg
```

you may only need:

```text
profile.jpg
```

---

# 🔟 `path.dirname()`

## 📖 What is `dirname()`?

`path.dirname()` returns the **folder containing the file**.

Example:

```js
const path = require("path");

const filePath = "/project/uploads/profile.jpg";

console.log(path.dirname(filePath));
```

Output:

```text
/project/uploads
```

Think:

```text
/project/uploads/profile.jpg
        ↑
      dirname
```

---

# 1️⃣1️⃣ `path.extname()`

## 📖 What is `extname()`?

`path.extname()` returns the **file extension**.

Example:

```js
const path = require("path");

const filePath = "profile.jpg";

console.log(path.extname(filePath));
```

Output:

```text
.jpg
```

Another example:

```js
console.log(path.extname("document.pdf"));
```

Output:

```text
.pdf
```

```js
console.log(path.extname("app.js"));
```

Output:

```text
.js
```

---

## 🌍 Real-World Example

Suppose a user uploads:

```text
resume.pdf
```

We can check:

```js
const extension = path.extname("resume.pdf");

console.log(extension);
```

Output:

```text
.pdf
```

This is useful when validating uploaded files.

---

# 1️⃣2️⃣ `__filename`

## 📖 What is `__filename`?

`__filename` gives the **complete path of the current JavaScript file**.

Example:

```js
console.log(__filename);
```

You may get:

```text
C:\Users\Ramesh\node-project\app.js
```

It tells us:

> "This is the exact location of the current file."

---

# 1️⃣3️⃣ `__dirname`

## 📖 What is `__dirname`?

`__dirname` gives the **directory/folder of the current JavaScript file**.

Example:

```js
console.log(__dirname);
```

Output might be:

```text
C:\Users\Ramesh\node-project
```

Notice:

### `__filename`

```text
C:\Users\Ramesh\node-project\app.js
```

### `__dirname`

```text
C:\Users\Ramesh\node-project
```

---

# 1️⃣4️⃣ 🆚 `__dirname` vs `__filename`

| Feature | Meaning | Example |
|---|---|---|
| `__dirname` | Current folder | `C:\project` |
| `__filename` | Current file | `C:\project\app.js` |

Easy memory:

```text
dirname   → directory
filename  → file
```

---

# 1️⃣5️⃣ ⭐ Most Important Combination

In real Node.js applications, you will frequently see:

```js
const path = require("path");

const filePath = path.join(__dirname, "data", "users.json");

console.log(filePath);
```

Suppose:

```text
C:\project
```

is your project folder.

Then:

```js
__dirname
```

is:

```text
C:\project
```

Then:

```js
path.join(__dirname, "data", "users.json")
```

creates:

```text
C:\project\data\users.json
```

This is a **very important pattern**.

---

# 1️⃣6️⃣ 🌍 Real-World File Path Example

Imagine a Node.js application:

```text
my-app/
│
├── app.js
│
├── data/
│   └── users.json
│
├── uploads/
│   ├── profile.jpg
│   └── resume.pdf
│
└── public/
    └── index.html
```

From `app.js`, we can create paths like this:

### Users JSON

```js
const usersFile = path.join(
    __dirname,
    "data",
    "users.json"
);
```

### Profile image

```js
const profileImage = path.join(
    __dirname,
    "uploads",
    "profile.jpg"
);
```

### Resume

```js
const resume = path.join(
    __dirname,
    "uploads",
    "resume.pdf"
);
```

### HTML file

```js
const htmlFile = path.join(
    __dirname,
    "public",
    "index.html"
);
```

This pattern will become very important when we learn the `fs` module.

---

# 1️⃣7️⃣ 🧪 Complete Example

Create:

```text
app.js
```

```js
const path = require("path");

// Current file
console.log("Filename:", __filename);

// Current directory
console.log("Directory:", __dirname);

// Join paths
const filePath = path.join(
    __dirname,
    "data",
    "users.json"
);

console.log("File Path:", filePath);

// Absolute path
const absolutePath = path.resolve(
    "data",
    "users.json"
);

console.log("Absolute Path:", absolutePath);

// File name
console.log(
    "File Name:",
    path.basename(filePath)
);

// Directory name
console.log(
    "Directory Name:",
    path.dirname(filePath)
);

// Extension
console.log(
    "Extension:",
    path.extname(filePath)
);
```

---

# 1️⃣8️⃣ 🔍 Dry Run

Suppose:

```text
Project:
C:\node-project
```

and:

```text
app.js
```

is inside it.

### Step 1

```js
__filename
```

gives:

```text
C:\node-project\app.js
```

### Step 2

```js
__dirname
```

gives:

```text
C:\node-project
```

### Step 3

```js
path.join(__dirname, "data", "users.json")
```

becomes:

```text
C:\node-project\data\users.json
```

### Step 4

```js
path.basename(filePath)
```

gives:

```text
users.json
```

### Step 5

```js
path.dirname(filePath)
```

gives:

```text
C:\node-project\data
```

### Step 6

```js
path.extname(filePath)
```

gives:

```text
.json
```

---

# 1️⃣9️⃣ 🧠 Quick Comparison

```text
path.join()
      ↓
Combine path parts

path.resolve()
      ↓
Create absolute path

path.basename()
      ↓
Get file name

path.dirname()
      ↓
Get folder name/path

path.extname()
      ↓
Get extension

__dirname
      ↓
Current folder

__filename
      ↓
Current file
```

---

# ⚠️ 2️⃣0️⃣ Common Mistakes

### ❌ Mistake 1 — Forgetting to import `path`

```js
path.join("data", "file.txt");
```

This causes an error if `path` wasn't defined.

### ✅ Correct

```js
const path = require("path");

path.join("data", "file.txt");
```

---

### ❌ Mistake 2 — Manually building complex paths

```js
const file = __dirname + "/data/users.json";
```

It can work, but using `path.join()` is cleaner.

### ✅ Better

```js
const file = path.join(
    __dirname,
    "data",
    "users.json"
);
```

---

### ❌ Mistake 3 — Confusing `basename()` and `dirname()`

```text
C:\project\data\users.json
```

`basename()`:

```text
users.json
```

`dirname()`:

```text
C:\project\data
```

---

# ✅ 2️⃣1️⃣ Best Practices

### ✔ Use `path.join()` for constructing paths

```js
const filePath = path.join(
    __dirname,
    "data",
    "users.json"
);
```

### ✔ Use `path.extname()` when checking extensions

```js
const ext = path.extname(file);
```

### ✔ Use `path.basename()` when you need only the filename

```js
const name = path.basename(file);
```

### ✔ Use `__dirname` for paths relative to the current file

```js
path.join(__dirname, "uploads");
```

### ✔ Avoid hard-coded absolute paths

Avoid:

```js
"C:\\Users\\Ramesh\\Desktop\\project\\data"
```

Prefer:

```js
path.join(__dirname, "data");
```

---

# 🎯 2️⃣2️⃣ Interview Questions

### 🟢 Beginner

**1. What is the Node.js `path` module?**

It is a built-in module used to create, manipulate, and understand file and directory paths.

**2. Do we install `path` using npm?**

No.

```js
const path = require("path");
```

It is built into Node.js.

**3. What does `path.join()` do?**

It combines multiple path segments into a properly formatted path.

---

### 🟡 Intermediate

**4. Difference between `path.join()` and `path.resolve()`?**

`join()` combines path segments, while `resolve()` produces an absolute path.

**5. What does `path.basename()` return?**

The last part of a path, usually the filename.

**6. What does `path.dirname()` return?**

The directory portion of a path.

**7. What does `path.extname()` return?**

The extension of a file.

Example:

```text
photo.jpg → .jpg
```

---

### 🔴 Advanced

**8. Why is `path.join()` preferred over manually concatenating paths?**

Because it handles path separators appropriately and makes code more portable across operating systems.

**9. Why is `__dirname` useful in backend applications?**

It allows us to create paths relative to the current source file instead of depending on the terminal's current working directory.

---

# 🧩 2️⃣3️⃣ Practice

Try these yourself.

### Task 1

Create this path:

```text
uploads/images/profile.jpg
```

using:

```js
path.join()
```

---

### Task 2

Given:

```js
const file = "/project/uploads/resume.pdf";
```

Find:

```text
resume.pdf
```

using `basename()`.

---

### Task 3

Find:

```text
/project/uploads
```

using `dirname()`.

---

### Task 4

Find:

```text
.pdf
```

using `extname()`.

---

### Task 5

Create an absolute path for:

```text
data/products.json
```

using:

```js
path.resolve()
```

---

# 🚀 2️⃣4️⃣ Mini Challenge

Create this project:

```text
node-path-practice/
│
├── app.js
│
├── data/
│   └── products.json
│
└── uploads/
    └── product.jpg
```

Inside `app.js`, create paths for:

```text
data/products.json
uploads/product.jpg
```

Then print:

```text
Current File:
Current Directory:
Products File:
Product Image:
Products File Name:
Products Extension:
Products Directory:
```

Use:

```js
path
path.join()
path.basename()
path.dirname()
path.extname()
__dirname
__filename
```

---

# 📌 2️⃣5️⃣ Chapter Summary

You learned the Node.js `path` module and its most important functions.

```text
path
│
├── path.join()
│     → combine paths
│
├── path.resolve()
│     → absolute path
│
├── path.basename()
│     → filename
│
├── path.dirname()
│     → directory
│
├── path.extname()
│     → file extension
│
├── __dirname
│     → current directory
│
└── __filename
      → current file
```

The most important real-world pattern is:

```js
const path = require("path");

const filePath = path.join(
    __dirname,
    "data",
    "users.json"
);
```

This pattern will be used heavily when we work with **files, uploads, images, JSON data, APIs, and Express applications**.

---

# ⚡ 2️⃣6️⃣ Quick Revision

| Concept | Remember |
|---|---|
| `path` | Work with file/folder paths |
| `path.join()` | Combine paths |
| `path.resolve()` | Create absolute path |
| `path.basename()` | Get filename |
| `path.dirname()` | Get directory |
| `path.extname()` | Get extension |
| `__dirname` | Current directory |
| `__filename` | Current file |

---

## 🛑 Chapter 6 Complete

Don't move to the next chapter until these are clear.

**Next chapter → Chapter 7: Node.js `fs` (File System) Module**

We will learn how Node.js actually **creates, reads, writes, updates, deletes, and manages files and folders**.

👉 Type **`NEXT`** when you're ready.