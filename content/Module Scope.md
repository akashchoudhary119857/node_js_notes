## Module Scope in Node.js

In Node.js, each file is treated as a separate module.

Variables, functions, and objects declared at the top level of a file are not added to the global scope. They are scoped only to that module. This is called **module scope**.

### Example

`// a.js var x = 10; let y = 20; const z = 30;  console.log(global.x); // undefined`

Even though `x` is declared at the top level, it is not global.

---

## Why this happens (behind the scenes)

Node.js does not run your file directly.

Before executing your code, Node wraps the entire file inside a special function. This is called the **module wrapper function**.

### Actual wrapper used by Node.js

`(function (exports, require, module, __filename, __dirname) {     // Your module code lives here });`

So your code:

`var x = 10; console.log(x);`

Actually becomes:

`(function (exports, require, module, __filename, __dirname) {     var x = 10;     console.log(x); });`

Because of this wrapper, variables become local to this function, not global. This creates module scope.

---

## Special variables provided by the wrapper

The wrapper function provides five variables that look global but are module-specific:

|Variable|Purpose|
|---|---|
|exports|Used to export values from the module|
|require|Used to import other modules|
|module|Contains information about the current module|
|__filename|Absolute path of the current file|
|__dirname|Absolute path of the current directory|

---

## Benefits of module wrapper and module scope

1. Prevents global variable pollution
    
2. Avoids variable and function name conflicts
    
3. Provides encapsulation
    
4. Improves code reusability
    
5. Enables modular architecture
    
6. Provides useful module-specific variables
    

---

## How to debug and see the module wrapper

You can prove that Node wraps your code.

### Step 1: Create a file test.js

`console.log(arguments);`

### Step 2: Run

`node test.js`

### Output

You will see something like:

`[Arguments] {   '0': {},   '1': [Function: require],   '2': { id: '.', ... },   '3': '/path/test.js',   '4': '/path' }`

These correspond to:

exports, require, module, __filename, __dirname

---

### Another debugging proof

`console.log(__filename); console.log(__dirname); console.log(module); console.log(exports);`

These values exist only because of the wrapper.

---

## Key interview statement

“Node.js wraps every module inside a function called the module wrapper function, which provides module scope and injects special variables like exports, require, module, __filename, and __dirname.”

---

## Summary

- Every file in Node.js is a module
    
- Node wraps your code in a function before execution
    
- This wrapper creates module scope
    
- Top-level variables are not global
    
- Wrapper provides useful module-specific variables
    
- Prevents conflicts and enables modular coding