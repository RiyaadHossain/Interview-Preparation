# 📘 JavaScript Scope — Interview Notes

## 🔹 What is Scope?

Scope determines where variables, functions, and objects are accessible in your code. JavaScript decides this based on where you declare things.

## 🔥 Types of Scope in JavaScript

### 1️⃣ Global Scope

Variables declared outside any block or function.

**Definition:** Accessible from anywhere in the program unless shadowed.

**Example:**
```javascript
let name = "Riyad";

function greet() {
  console.log(name); // accessible
}

console.log(name);
```

### 2️⃣ Function Scope

Variables declared inside a function using `var`, `let`, or `const`.

**Definition:** Accessible only inside the function.

**Example:**
```javascript
function test() {
  let a = 5;
  console.log(a); 
}

test();
console.log(a); // ReferenceError
```

### 3️⃣ Block Scope

Variables declared using `let` or `const` inside `{}`.

**Definition:** Accessible only within that block.

**Example:**
```javascript
{
  let x = 10;
  const y = 20;
}

console.log(x); // ReferenceError
console.log(y); // ReferenceError
```

### 4️⃣ Module Scope

Available only within the current ES module file.

**Example:**

**utils.js**
```javascript
const secret = "xyz";
export function sum(a, b) {
  return a + b;
}
```

**app.js**
```javascript
import { sum } from "./utils.js";

sum(2, 3); 
console.log(secret); // ReferenceError
```

### 5️⃣ Lexical Scope (Scope Chain)

Inner functions can access variables defined in outer scopes.

**Example:**
```javascript
function outer() {
  let x = 10;

  function inner() {
    console.log(x);
  }

  inner();
}

outer(); // 10
```

## 🧠 Scope Chain

When accessing a variable, JavaScript searches:

1. Local scope
2. Parent scope
3. Global scope

If not found → `ReferenceError`

---

## 🚀 JavaScript Scope — Interview "Guess the Output"

Below are common interview questions with complete answers + explanations.

### ⭐ Q1 — Function vs Block Scope

```javascript
var x = 10;

if (true) {
  var x = 20;
  let y = 30;
}

console.log(x);
console.log(y);
```

**✔ Output:**
```
20
ReferenceError: y is not defined
```

**✔ Explanation:**
- `var` is function-scoped, so `x` gets overwritten.
- `let y` is block-scoped, not accessible outside.

---

### ⭐ Q2 — Shadowing + Lexical Scope

```javascript
let a = 1;

function test() {
  let a = 2;
  function inner() {
    console.log(a);
  }
  inner();
}

test();
```

**✔ Output:**
```
2
```

**✔ Explanation:**
- Inner function accesses the closest `a` → lexical scope.

---

### ⭐ Q3 — var Hoisting

```javascript
function foo() {
  console.log(a);
  var a = 5;
  console.log(a);
}

foo();
```

**✔ Output:**
```
undefined
5
```

**✔ Explanation:**
- `var a` is hoisted as `undefined`.

---

### ⭐ Q4 — TDZ (Tricky)

```javascript
let z = 99;

{
  console.log(z);
  let z = 50;
}
```

**✔ Output:**
```
ReferenceError: Cannot access 'z' before initialization
```

**✔ Explanation:**
- The inner block creates a new `z`; accessing it before declaration hits TDZ.

---

### ⭐ Q5 — Lexical Scope Chain

```javascript
let m = 1;

function outer() {
  function inner() {
    console.log(m, n);
  }
  let n = 2;
  inner();
}

outer();
```

**✔ Output:**
```
1 2
```

---

### ⭐ Q6 — var in Loops

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
```

**✔ Output:**
```
3
3
3
```

**✔ Explanation:**
- `var` creates one shared `i`.

---

### ⭐ Q7 — let in Loops

```javascript
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
```

**✔ Output:**
```
0
1
2
```

**✔ Explanation:**
- Each iteration has a new block-scoped `i`.

---

### ⭐ Q8 — Function Scope vs Block Scope

```javascript
function run() {
  if (true) {
    var a = 1;
    let b = 2;
  }
  console.log(a);
  console.log(b);
}

run();
```

**✔ Output:**
```
1
ReferenceError: b is not defined
```

---

### ⭐ Q9 — NOT a TDZ Error (Important!)

```javascript
let p = 10;

function calc() {
  console.log(p);
  if (true) {
    let p = 20;
  }
}

calc();
```

**✔ Output:**
```
10
```

**✔ Explanation:**
- TDZ applies only inside the block where `let p` is declared.
- `console.log(p)` is outside, so it sees the global `p`.

---

### ⭐ Q10 — Closure with Mutation

```javascript
let count = 0;

function inc() {
  console.log(count);
  count++;
}

inc();
inc();
inc();
```

**✔ Output:**
```
0
1
2
```

---

## 🎯 Final Tips for Interviews

- Always identify scope boundaries (function, block, global).
- Watch for shadowing (same variable name in inner scope).
- Remember TDZ only applies inside the block of `let`/`const`.
- `var` = hoisted + function-scoped → often causes bugs.
- `let` and `const` are safer because they are block-scoped.