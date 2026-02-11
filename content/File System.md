### What I included (important for exams + interviews)

- **Synchronous vs Asynchronous fs**
    
- **All major fs sync methods**
    
-  **writeFileSync / readFileSync parameters & return values**
    
-  **Flags (`r`, `w`, `a`, etc.) – with meanings**
    
-  **`mode` (permissions) – clear octal table**
    
-  **Why write-only mode still allows reading (Windows vs Linux reality)**
    
-  **`flag` vs `mode` vs `encoding` (very common confusion)**
    
-  **Directory operations**
    
-  **File deletion & stats**
    
-  **Best practices**
    
-  **Interview one-liners**

Database vs File system :
| Aspect       | File System            | Database              |
| ------------ | ---------------------- | --------------------- |
| Purpose      | Store files & raw data | Store structured data |
| Best for       | Files, logs, media     | Records, relations    |
| Performance | Fast for file access   | Fast for queries      |
| Querying      | No querying            | Advanced querying     |
| Transactions | No                           | Yes                 |
| Indexing       |  No                          |  Yes                 |
# Node.js File System (fs) Module — Complete Notes

The `fs` module allows Node.js to **interact with the file system**: create, read, write, update, delete files and directories.

---

## 13. Importing `fs` Module

const fs = require('fs'); // CommonJS

// OR

import fs from 'fs'; // ES Modules

---

## 14. File System Types

|   |   |
|---|---|
|Type|Description|
|**Synchronous**|Blocks execution until operation completes|
|**Asynchronous**|Non-blocking, uses callbacks/promises|

---

## 15. Synchronous File Operations (Blocking)

### writeFileSync

fs.writeFileSync('test.txt', 'Hello World', {

encoding: 'utf8',

flag: 'w',

mode: 0o644

});

### Parameters

|   |   |   |
|---|---|---|
|Parameter|Required|Purpose|
|path|Yes|File path|
|data|Yes|Content to write|
|options|No|encoding, flag, mode|

### Return Value

`undefined`

---

### readFileSync

const data = fs.readFileSync('test.txt', 'utf8');

console.log(data);

### Return Value

Returns **file content** (string or Buffer)

---

## 16. Asynchronous File Operations (Non-Blocking)

### writeFile

fs.writeFile('test.txt', 'Hello', (err) => {

if (err) throw err;

console.log('File written');

});

### readFile

fs.readFile('test.txt', 'utf8', (err, data) => {

if (err) throw err;

console.log(data);

});

---

## 17. Flags in `fs`

Flags define **how** the file is opened.

|   |   |
|---|---|
|Flag|Meaning|
|`r`|Read|
|`w`|Write (overwrite)|
|`a`|Append|
|`r+`|Read + Write|
|`w+`|Write + Read|
|`a+`|Append + Read|

Flags do **not** control permissions.

---

## 18. File `mode` (Permissions)

Mode controls **WHO can read/write/execute** a file (Unix-based systems).

|   |   |
|---|---|
|Mode|Permission|
|`0o200`|Write only|
|`0o400`|Read only|
|`0o600`|Read + Write|
|`0o700`|Full access|
|`0o644`|Owner RW, others R|

⚠️ **Windows does NOT strictly enforce Unix modes**.

---

## 19. Why Write-Only Mode Still Allows Read

fs.writeFileSync('test.txt', 'Secret', { mode: 0o200 });

fs.readFileSync('test.txt', 'utf8'); // Still works on Windows

### Reason

- Windows uses **ACL**, not Unix permissions
    
- `mode` is best-effort only on Windows
    
- Fully enforced on Linux/macOS
    

---

## 20. `flag` vs `mode` vs `encoding`

|   |   |
|---|---|
|Option|Controls|
|`flag`|Operation (read/write/append)|
|`mode`|Permissions|
|`encoding`|Data format|

---

## 21. Directory Operations

fs.mkdirSync('data');

fs.rmdirSync('data');

fs.readdirSync('./');

---

## 22. File Deletion

fs.unlinkSync('test.txt');

---

## 23. File Information

const stats = fs.statSync('test.txt');

console.log(stats.isFile());

console.log(stats.size);

---

## 24. Best Practices

- Prefer async `fs` in production
    
- Avoid heavy sync calls
    
- Do not rely on `mode` for security
    
- Use application-level authorization
    

---

## 25. Interview One-Liners (File System)

- `writeFileSync()` returns `undefined`
    
- `readFileSync()` returns data
    
- Flags define operation, not permission
    
- Mode is OS-dependent
    
- Windows ignores Unix permissions
    
- Async fs improves performance
    

---

**End of Document**

I’ve added **complete, structured File System (fs) notes** to your existing Node.js document in the canvas.

    

### Ke
y clarification you were concerned about

> **“Still write mode value is missing to deny reading permission”**

This is now clearly explained:

- `mode` works properly on **Linux/macOS**
    
- On **Windows**, Unix permissions are **not enforced**
    
- Hence read access still works even with write-only modes
    

This explanation is **exam-safe and technically correct**.