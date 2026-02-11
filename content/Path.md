The **`path` module** in Node.js is a **core (built-in) module** that provides utilities for working with **file and directory paths**.

It helps **handle and transform paths in a platform-independent way**:

- **Windows** uses backslashes (`\`)
    
- **Unix/Linux/macOS** use forward slashes (`/`)
    

The `path` module automatically handles these differences, ensuring **cross-platform compatibility**.

---

## Commonly Used Methods in `path` Module

### 1. `path.basename()`

Returns the **file name** portion of a path.

`path.basename('/users/admin/file.txt'); // Output: file.txt`

---

### 2. `path.extname()`

Returns the **file extension** of the path.

`path.extname('/users/admin/file.txt'); // Output: .txt`

---

### 3. `path.dirname()`

Returns the **directory name** of a given path.

`path.dirname('/users/admin/file.txt'); // Output: /users/admin`

---

### 4. `path.join()`

Joins multiple path segments into a **single normalized path**.

`path.join('users', 'admin', 'file.txt'); // Output: users/admin/file.txt`

---

### 5. `path.normalize()`

Normalizes a path by:

- Resolving `.` (current directory)
    
- Resolving `..` (parent directory)
    
- Removing extra slashes
    
- Converting it into a **proper, clean path**
    

`path.normalize('/users/admin/../docs/./file.txt'); // Output: /users/docs/file.txt`

 Useful when paths are dynamically generated or user-provided.

---

### 6. `path.parse()`

Returns an **object** with detailed information about the path.

`path.parse('/users/admin/file.txt');`

`{   root: '/',   dir: '/users/admin',   base: 'file.txt',   ext: '.txt',   name: 'file' }`

---

### 7. `path.resolve()`

Resolves a sequence of paths into an **absolute path**.

`path.resolve('users', 'admin', 'file.txt'); // Output: /current/working/directory/users/admin/file.txt`

---

### 8. `path.isAbsolute()`

Checks whether a given path is **absolute** or not.

`path.isAbsolute('/users/admin'); // Output: true`

`path.isAbsolute('users/admin'); // Output: false`

---

## Why Use `path` Module?

 Avoids hard-coding OS-specific separators  
 Prevents path errors  
 Makes applications **portable across Windows, Linux, and macOS**  
 Essential for file system operations in Node.js


The **Node.js `path` module** is a **built-in core module** that provides utilities to work with and manipulate **file and directory paths** in a platform-independent way.

To use it in your code:

`const path = require('path');`

---

##  Why Use `path` Module

Handles differences between operating systems (Windows vs Linux/macOS)  
 Makes file path operations safer and easier  
 Avoids manually concatenating strings for file paths  
 Improves readability and reliability of code

---

##  Important `path` Methods & What They Do

---

###  `path.basename(path)`

Returns the **last part** of a file path (usually file name).

`console.log(path.basename("/user/docs/readme.txt"));  // Output: readme.txt`

---

###  `path.extname(path)`

 Returns the **extension** of the file.

`console.log(path.extname("index.js"));  // Output: .js`

---

###  `path.dirname(path)`

 Returns the **directory name** of a path.

`console.log(path.dirname("/user/docs/readme.txt"));  // Output: /user/docs`

---

###  `path.join([...paths])`

 Joins multiple path segments together and **normalizes** them.

`path.join("folder1", "folder2", "file.txt"); // Output on Unix: folder1/folder2/file.txt // On Windows: folder1\folder2\file.txt`

---

###  `path.normalize(path)`

 Normalizes a path, resolving `".."`, `"."`, and extra separators.

`path.normalize("folder//sub/../file.txt"); // Output: folder/file.txt`

---

###  `path.resolve([...paths])`

 Resolves segments into an **absolute path**.

`path.resolve("folder", "file.txt"); // Output: (absolute path based on current working directory)`

---

###  `path.isAbsolute(path)`

 Checks if a path is **absolute** or not.

`console.log(path.isAbsolute("/user"));  // true`

---

###  `path.parse(path)`

 Returns an object with detailed components:

`const p = path.parse("/user/docs/readme.txt"); console.log(p); /* {   root: "/",   dir: "/user/docs",   base: "readme.txt",   ext: ".txt",   name: "readme" } */`

---

##  Bonus Useful Things

### __dirname and __filename

- `__dirname` → Absolute path to the **current folder**
    
- `__filename` → Absolute path to the **current file**
    

These are _provided automatically in Node.js scripts_ (not part of `path` module but often used with it)

---

##  Example Use Case

### Suppose you want to build a file path safely:

`const path = require('path');  // join parts into platform-safe path const filePath = path.join(__dirname, "data", "users.json");  console.log(filePath);`

This will produce correct path separators on Windows and Unix systems.

---

##  Summary

|Method|Purpose|
|---|---|
|`path.basename()`|Gets file name from path|
|`path.extname()`|Gets file extension|
|`path.dirname()`|Gets directory path|
|`path.join()`|Joins path segments|
|`path.normalize()`|Cleans up path string|
|`path.resolve()`|Converts to absolute path|
|`path.isAbsolute()`|Checks for absolute path|
|`path.parse()`|Breaks path into parts|