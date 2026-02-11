# Node.js Modules – Notes

## What is a Module in Node.js?

- In **Node.js**, **any JavaScript file with a `.js` extension is called a module**.
    
- A module can contain:
    
    - Functions
        
    - Classes
        
    - Objects
        
    - Variables
        
- These definitions can be **referenced and used in another JavaScript file**.
    

---

## Why Do We Need Modules?

- When an application becomes **large**, maintaining all code in **one single file** becomes difficult.
    
- Problems with a single large file:
    
    - Hard to understand the code
        
    - Difficult to debug
        
    - Easy to lose track of what each part of the code does
        
    - Poor code reusability
        

---

## Modularization

- **Modularization** is the process of:
    
    - Splitting code into **multiple files**
        
    - Treating each file as a **module**
        
- Each module handles a **specific functionality**.
    
- This improves:
    
    - Code organization
        
    - Readability
        
    - Maintainability
        

---

##  Reusability of Code

- Functions defined in one module can be:
    
    - **Imported**
        
    - **Used in other modules**
        
- This avoids:
    
    - Rewriting or copying the same function in multiple files
        
- Promotes **code reuse**.
    

---

## Independent Development

- Each module can be:
    
    - Edited separately
        
    - Debugged independently
        
- Makes it easier to:
    
    - Add new features
        
    - Remove existing features
        
    - Maintain the application efficiently
        

---

## Advantages of Modules in Node.js

Better code organization  
Easy maintenance  
High reusability  
Simplified debugging  
Scalable application structure

---

## Key Exam Points

- Every `.js` file in Node.js is a module
    
- Modularization helps manage large applications
    
- Modules improve reusability and maintainability
    
- Node.js uses `require()` and `module.exports` to work with modules

### What this document covers

- CommonJS **default export** and **named exports**
    
- Multiple named exports
    
- ES Modules (`import / export`)
    
- Default vs named exports (rules + use cases)
    
- `require()` vs `import` comparison
    
- **Module execution vs export**
    
- **Module caching** with `require.cache`
    
- Interview one-liners and best practices
    
- Clean, corrected code examples
# Node.js Modules: CommonJS vs ES Modules

This document explains **module creation, exports, imports, execution behavior, and caching** in Node.js with clear examples.


---

## 1. CommonJS – Default Export (Single Export)

### `mergeclass.js`

```js
console.log("hello class FB and FF");

function add() {
  console.log("hello");
}

module.exports = add;
```

### `useclass.js`

```js
const dummy = require("./mergeclass");
dummy();
```

### Explanation

- Entire file executes when required
    
- `module.exports` points to a **single function**
    
- `dummy` holds the exported function
    

---

## 2. CommonJS – Named Exports (Single Function)

### `mergeclass.js`

```js
console.log("hello class FB and FF");

function add() {
  console.log("hello");
}

module.exports = { add };
```

### `useclass.js`

```js
const { add } = require("./mergeclass");
add();
```

---

## 3. CommonJS – Multiple Named Exports

### `mergeclass.js`

```js
const add = (a, b) => a + b;
const subtract = (a, b) => a - b;
console.log("hello"); 
module.exports = {
  add,
  subtract
};
```

### `useclass.js`

```js
const { add, subtract } = require('./mergeclass');

console.log(add(5, 3));      // 8
console.log(subtract(5, 3)); // 2
```

### Alternative Import Style

```js
const { add } = require('./mergeclass');
const { subtract } = require('./mergeclass');
```

---

## 4. ES Modules (Modern Node.js)

### When to Use ES Modules

- File extension is `.mjs`
    
- OR `"type": "module"` in `package.json`
    

---

## 5. ES Modules – Named Exports

### `mergeclass.js`

```js
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;
```

### `useclass.js`

```js
import { add, subtract } from './mergeclass.js';

console.log(add(10, 5));      // 15
console.log(subtract(10, 5)); // 5
```

### Rules

- Must use **same export names**
    
- Must use `{ }`
    

---

## 6. ES Modules – Default Export

### `mergeclass.js`

```js
export default function multiply(a, b) {
  return a * b;
}
```

### `useclass.js`

```js
import multiply from './mergeclass.js';

console.log(multiply(6, 7)); // 42
```

### Rules

- Only **one default export per file**
    
- Import name can be anything
    

---

## 7. Named + Default Export Together

### `mergeclass.js`

```js
export const add = (a, b) => a + b;

export default function multiply(a, b) {
  return a * b;
}
```

### `useclass.js`

```js
import multiply, { add } from './mergeclass.js';

console.log(add(2, 3));      // 5
console.log(multiply(2, 3)); // 6
```

---

## 8. Named vs Default Export Comparison

|Feature|Named Export|Default Export|
|---|---|---|
|Number allowed|Multiple|Only one|
|Import syntax|`{ name }`|No `{}`|
|Name flexibility|Must match|Any name|
|Best use case|Utilities, helpers|Main functionality|

---

## 9. `require()` vs `import`

|Feature|`require()`|`import`|
|---|---|---|
|Module system|CommonJS|ES Modules|
|Execution|Synchronous|Asynchronous|
|Can be conditional|Yes|No|
|Top-level use|Anywhere|Top-level only|
|Default in Node|Yes|With `"type":"module"`|
|Caching|Yes|Yes|

Note : You **cannot mix** `require()` and `import` in the same file.

---

## 10. Important Concept: Module Execution vs Export

- `require()` executes the file immediately
    
- Returns `module.exports`
    
- Top-level code runs **once only**
    
- Even if functions are not called
    

---

## 11. Module Caching in Node.js

### Concept

- Module executes once
    
- Stored in memory cache
    
- Future `require()` returns cached version
    

### Example

```js
const { add } = require('./mergeclass');

delete require.cache[require.resolve('./mergeclass.js')];// optional

const { subtract } = require('./mergeclass');
```

### Use Cases

- Unit testing
    
- Hot reloading
    
- Development tools
    

---

## 12. Interview One-Liners

- `require()` executes the module immediately
    
- All top-level code runs once
    
- Modules are cached after first load
    
- Avoid heavy logic at top-level
    
- Prefer functions for controlled execution
    

---
## File: `mergeclass.js`

module.exports = {
    display: function display() {
        console.log("akash");
    },
    age: 30
}
### What this does

- `module.exports` is used to **export data from a file** in Node.js.
    
- You are exporting an **object** that contains:
    
    - `display` → a function that prints `"akash"`
        
    - `age` → a number (`30`)
        

So this file is making these two things available to other files.

---

## File: another JS file (useclass.js)

`const dis = require("./mergeclass");  console.log(dis.age);`

### What this does

- `require("./mergeclass")`:
    
    - Imports whatever is exported from `mergeclass.js`
        
- The imported object is stored in `dis`
    

So effectively:

`dis = {   display: [Function],   age: 30 }`

---

## Output

`30`

Because you are accessing:

`dis.age`

---

##  If you also call the function

If you add this line:

`dis.display();`

### Output will be:

`30 akash`

---

## Key Notes 

- `module.exports` → used to export **object, function, variable**
    
- `require()` → used to import exported content
    
- Access members using **dot notation** (`dis.age`, `dis.display()`)
**End of Document**