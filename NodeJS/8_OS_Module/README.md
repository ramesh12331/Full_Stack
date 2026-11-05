# 💻 Chapter 8 — Node.js `os` Module

### 🔑 Requires Before Starting

Before starting Chapter 8, you should understand:

1. **Basic JavaScript variables**
   ```js
   const name = "Ramesh";
   ```

2. **Node.js basics**
   ```bash
   node app.js
   ```

3. **Node.js modules**
   ```js
   const something = require("something");
   ```

4. **Chapter 5 — Modules**

5. **Chapter 6 — `path` module**

6. **Chapter 7 — `fs` module**

You should already understand that Node.js provides **built-in modules** such as:

```text
path
fs
os
```

---

# 1️⃣ What is the `os` Module?

`os` means **Operating System**.

The Node.js `os` module provides information about the computer's operating system.

For example, Node.js can find:

```text
💻 Operating system
🧠 CPU information
💾 Total memory
📊 Free memory
🏠 Home directory
👤 Current user
🌐 Hostname
⚙️ CPU architecture
```

`os` is a **built-in Node.js module**.

You don't install it.

```js
const os = require("os");
```

---

# 2️⃣ 🤔 Why Do We Need `os`?

Imagine you are creating a backend monitoring application.

You may want to know:

```text
Which operating system is running?
How much memory is available?
How many CPU cores are available?
What is the computer hostname?
Which user is running the application?
```

Node.js can get this information through the `os` module.

---

# 3️⃣ 🌍 Real-World Analogy

Think about a doctor checking a person's basic information:

```text
Name
Age
Height
Weight
Temperature
```

Similarly, the `os` module checks information about the computer:

```text
Operating System
CPU
Memory
Hostname
User
Architecture
```

---

# 4️⃣ Import the `os` Module

```js
const os = require("os");
```

Now we can use:

```js
os.platform()
os.arch()
os.cpus()
os.totalmem()
os.freemem()
os.hostname()
os.homedir()
os.userInfo()
```

---

# 5️⃣ 🖥️ `os.platform()`

`os.platform()` tells us the operating-system platform.

```js
const os = require("os");

console.log(os.platform());
```

On Windows, you may get:

```text
win32
```

On Linux:

```text
linux
```

On macOS:

```text
darwin
```

### Easy memory

```text
os.platform()
      ↓
Which platform?
```

---

# 6️⃣ ⚙️ `os.arch()`

`os.arch()` tells us the CPU architecture.

```js
const os = require("os");

console.log(os.arch());
```

You may see:

```text
x64
```

Common values include:

```text
x64
arm64
```

### Meaning

```text
x64
 ↓
64-bit x86 architecture

arm64
 ↓
64-bit ARM architecture
```

---

# 7️⃣ 🧠 `os.cpus()`

`os.cpus()` returns information about the computer's CPU cores.

```js
const os = require("os");

console.log(os.cpus());
```

The output can be large because each CPU core has information such as:

```text
model
speed
times
```

---

# 8️⃣ 🔢 Finding Number of CPU Cores

Instead of printing everything:

```js
const os = require("os");

console.log(os.cpus().length);
```

Example:

```text
8
```

This means Node.js detected:

```text
8 logical CPU processors
```

### Important

```js
os.cpus()
```

returns an array.

Therefore:

```js
os.cpus().length
```

gives the number of entries.

---

# 9️⃣ 💾 `os.totalmem()`

`os.totalmem()` returns the total amount of system memory in **bytes**.

```js
const os = require("os");

console.log(os.totalmem());
```

You might see:

```text
17179869184
```

That number is bytes.

That's difficult for humans to read.

---

# 🔟 Converting Bytes to GB

We can convert bytes into GB.

```js
const os = require("os");

const totalMemory = os.totalmem();

const totalMemoryGB =
    totalMemory / (1024 ** 3);

console.log(totalMemoryGB);
```

You might get:

```text
16
```

So the computer has approximately:

```text
16 GB RAM
```

---

# 1️⃣1️⃣ 🆓 `os.freemem()`

`os.freemem()` tells us how much memory is currently available.

```js
const os = require("os");

console.log(os.freemem());
```

Again, the result is in bytes.

We can convert it:

```js
const freeMemoryGB =
    os.freemem() / (1024 ** 3);

console.log(freeMemoryGB);
```

Example:

```text
6.25
```

This means approximately:

```text
6.25 GB available memory
```

---

# 1️⃣2️⃣ 🏠 `os.homedir()`

`os.homedir()` returns the current user's home directory.

```js
const os = require("os");

console.log(os.homedir());
```

On Windows, you might get something similar to:

```text
C:\Users\Ramesh
```

On Linux:

```text
/home/ramesh
```

---

# 1️⃣3️⃣ 🌐 `os.hostname()`

`os.hostname()` returns the computer's hostname.

```js
const os = require("os");

console.log(os.hostname());
```

Example:

```text
DESKTOP-ABC123
```

The exact result depends on your computer.

---

# 1️⃣4️⃣ 👤 `os.userInfo()`

`os.userInfo()` gives information about the current operating-system user.

```js
const os = require("os");

console.log(os.userInfo());
```

It can contain information such as:

```text
username
homedir
shell
uid
gid
```

The exact fields can differ depending on the operating system.

---

# 1️⃣5️⃣ ⏱️ `os.uptime()`

`os.uptime()` tells us how long the operating system has been running.

The result is in **seconds**.

```js
const os = require("os");

console.log(os.uptime());
```

Example:

```text
7200
```

That means:

```text
7200 seconds
```

which is:

```text
2 hours
```

---

# 1️⃣6️⃣ 🔢 Convert Uptime to Hours

```js
const os = require("os");

const uptime = os.uptime();

const hours = uptime / 3600;

console.log(hours);
```

---

# 1️⃣7️⃣ 🧮 `os.EOL`

`os.EOL` gives the operating system's default line-ending character.

```js
const os = require("os");

console.log(os.EOL);
```

Why is this useful?

Different operating systems traditionally use different line endings.

Using:

```js
os.EOL
```

can help when generating platform-specific text.

---

# 1️⃣8️⃣ 📦 `os.tmpdir()`

`os.tmpdir()` gives the operating system's temporary directory.

```js
const os = require("os");

console.log(os.tmpdir());
```

Example:

```text
C:\Users\Ramesh\AppData\Local\Temp
```

This can be useful when an application needs temporary files.

---

# 1️⃣9️⃣ 🧪 Complete Example

Create:

```text
os-practice/
└── app.js
```

`app.js`:

```js
const os = require("os");

console.log("Platform:", os.platform());

console.log("Architecture:", os.arch());

console.log("CPU Cores:", os.cpus().length);

console.log(
    "Total Memory:",
    os.totalmem() / (1024 ** 3),
    "GB"
);

console.log(
    "Free Memory:",
    os.freemem() / (1024 ** 3),
    "GB"
);

console.log("Hostname:", os.hostname());

console.log("Home Directory:", os.homedir());

console.log("User Information:", os.userInfo());

console.log(
    "Uptime:",
    os.uptime(),
    "seconds"
);

console.log("Temp Directory:", os.tmpdir());
```

Run:

```bash
node app.js
```

---

# 2️⃣0️⃣ 🔍 Example Output

Your output will be different depending on your computer.

For example:

```text
Platform: win32
Architecture: x64
CPU Cores: 12
Total Memory: 15.8 GB
Free Memory: 6.4 GB
Hostname: DESKTOP-ABC123
Home Directory: C:\Users\Ramesh
User Information: {
    username: 'Ramesh',
    ...
}
Uptime: 54231 seconds
Temp Directory: C:\Users\Ramesh\AppData\Local\Temp
```

Don't worry if your values are different.

That's expected.

---

# 2️⃣1️⃣ 🔍 Dry Run

Consider:

```js
const os = require("os");

console.log(os.platform());

console.log(os.arch());

console.log(os.cpus().length);
```

### Step 1

```js
require("os")
```

loads the Node.js operating-system module.

### Step 2

```js
os.platform()
```

asks:

> Which operating-system platform is this?

### Step 3

```js
os.arch()
```

asks:

> Which CPU architecture is being used?

### Step 4

```js
os.cpus()
```

gets CPU information.

### Step 5

```js
.length
```

counts the CPU entries.

---

# 2️⃣2️⃣ 🌍 Real-World Example — Server Information

Imagine your Node.js backend has an endpoint:

```text
GET /system-info
```

The server could return:

```json
{
  "platform": "win32",
  "architecture": "x64",
  "cpuCores": 12,
  "totalMemoryGB": 16,
  "freeMemoryGB": 6,
  "hostname": "DESKTOP-ABC123"
}
```

This can be useful for:

```text
📊 Server monitoring
🐛 Debugging
🖥️ System diagnostics
⚡ Performance monitoring
```

---

# 2️⃣3️⃣ 🧪 Practical System Information Program

Let's create a cleaner version.

```js
const os = require("os");

const totalMemory =
    os.totalmem() / (1024 ** 3);

const freeMemory =
    os.freemem() / (1024 ** 3);

const systemInfo = {
    platform: os.platform(),
    architecture: os.arch(),
    cpuCores: os.cpus().length,
    totalMemoryGB: totalMemory.toFixed(2),
    freeMemoryGB: freeMemory.toFixed(2),
    hostname: os.hostname()
};

console.log(systemInfo);
```

Example:

```text
{
  platform: 'win32',
  architecture: 'x64',
  cpuCores: 12,
  totalMemoryGB: '15.82',
  freeMemoryGB: '6.41',
  hostname: 'DESKTOP-ABC123'
}
```

---

# 2️⃣4️⃣ 🧠 Important `os` Methods

| Method | Purpose |
|---|---|
| `os.platform()` | Operating-system platform |
| `os.arch()` | CPU architecture |
| `os.cpus()` | CPU information |
| `os.totalmem()` | Total memory |
| `os.freemem()` | Available memory |
| `os.hostname()` | Computer hostname |
| `os.homedir()` | User home directory |
| `os.userInfo()` | Current user information |
| `os.uptime()` | OS uptime |
| `os.tmpdir()` | Temporary directory |
| `os.EOL` | OS line ending |

---

# ⚠️ 2️⃣5️⃣ Common Mistakes

### ❌ Mistake 1 — Forgetting to import `os`

Wrong:

```js
console.log(os.platform());
```

Correct:

```js
const os = require("os");

console.log(os.platform());
```

---

### ❌ Mistake 2 — Thinking `totalmem()` returns GB

It returns **bytes**.

```js
os.totalmem()
```

For GB:

```js
os.totalmem() / (1024 ** 3)
```

---

### ❌ Mistake 3 — Confusing `cpus()` with CPU count

```js
os.cpus()
```

returns CPU information.

To get the number of entries:

```js
os.cpus().length
```

---

### ❌ Mistake 4 — Expecting the same output on every computer

For example:

```js
os.hostname()
```

will be different on different computers.

Memory and CPU information will also vary.

---

# ✅ 2️⃣6️⃣ Best Practices

### ✔ Don't hard-code operating-system paths

Instead of assuming:

```text
C:\Users\...
```

use Node.js APIs such as:

```js
os.homedir()
```

and:

```js
path.join()
```

### ✔ Convert bytes when displaying memory

```js
const memoryGB =
    os.totalmem() / (1024 ** 3);
```

### ✔ Use `os` when you actually need system information

Don't use it unnecessarily in every application.

---

# 🎯 2️⃣7️⃣ Interview Questions

### 🟢 Beginner

**1. What is the `os` module?**

It is a built-in Node.js module that provides information about the operating system.

**2. How do you import it?**

```js
const os = require("os");
```

**3. How do you find the operating-system platform?**

```js
os.platform()
```

**4. How do you find CPU information?**

```js
os.cpus()
```

**5. How do you find total memory?**

```js
os.totalmem()
```

---

### 🟡 Intermediate

**6. How do you find the number of CPU entries?**

```js
os.cpus().length
```

**7. What unit does `os.totalmem()` return?**

Bytes.

**8. What does `os.homedir()` return?**

The current user's home directory.

**9. What does `os.uptime()` return?**

The amount of time the operating system has been running, in seconds.

---

### 🔴 Advanced

**10. Why might the `os` module be useful in a backend application?**

It can provide system information for diagnostics, monitoring, resource checks, and environment-aware application behavior.

**11. Can `os.cpus().length` be treated as the exact number of physical CPU cores?**

Not necessarily. It represents the number of CPU entries reported by Node.js, which can include logical processors.

---

# 🧩 2️⃣8️⃣ Practice

### Task 1

Print:

```text
Operating System:
Architecture:
```

using:

```js
os.platform()
os.arch()
```

---

### Task 2

Print the number of CPU entries.

```js
os.cpus().length
```

---

### Task 3

Print total RAM in GB.

---

### Task 4

Print available RAM in GB.

---

### Task 5

Print:

```text
Hostname:
Home Directory:
Temporary Directory:
```

---

### Task 6

Convert uptime from seconds into hours.

---

# 🚀 2️⃣9️⃣ Mini Challenge

Create:

```text
node-os-practice/
└── app.js
```

Build a **System Information Dashboard**.

Expected output:

```text
================================
      SYSTEM INFORMATION
================================

Platform       : win32
Architecture   : x64
CPU Cores      : 12
Total Memory   : 15.82 GB
Free Memory    : 6.41 GB
Hostname       : DESKTOP-ABC123
Home Directory : C:\Users\Ramesh
Temp Directory : C:\Users\Ramesh\AppData\Local\Temp

================================
```

Use:

```js
os.platform()
os.arch()
os.cpus()
os.totalmem()
os.freemem()
os.hostname()
os.homedir()
os.tmpdir()
```

Try building it yourself before looking at a solution.

---

# 📌 3️⃣0️⃣ Chapter Summary

The `os` module helps Node.js communicate with the operating system.

```text
os
│
├── platform()
│      → operating system
│
├── arch()
│      → CPU architecture
│
├── cpus()
│      → CPU information
│
├── totalmem()
│      → total memory
│
├── freemem()
│      → free memory
│
├── hostname()
│      → computer name
│
├── homedir()
│      → user home directory
│
├── userInfo()
│      → current user
│
├── uptime()
│      → OS running time
│
└── tmpdir()
       → temporary directory
```

---

# ⚡ 3️⃣1️⃣ Quick Revision

Remember these first:

```text
os.platform()
→ Which OS?

os.arch()
→ Which architecture?

os.cpus()
→ CPU information

os.cpus().length
→ Number of CPU entries

os.totalmem()
→ Total RAM in bytes

os.freemem()
→ Free RAM in bytes

os.hostname()
→ Computer hostname

os.homedir()
→ User's home directory

os.uptime()
→ OS uptime

os.tmpdir()
→ Temporary directory
```

---

# 🛑 Chapter 8 Complete

### ➡️ Next Chapter — **Chapter 9: Node.js `events` Module**

We will learn:

- `events`
- `EventEmitter`
- creating events
- `.on()`
- `.emit()`
- `.once()`
- `.removeListener()`
- custom events
- event-driven architecture
- practical Node.js examples

👉 Type **`NEXT`** when you're ready.