## Express 5 Wildcard Route Error

### Problem Code (works in Express 4, breaks in Express 5)

`app.get("*", (req, res) => {     res.send("404 error"); });`

### Error Seen

`PathError [TypeError]: Missing parameter name at index 1: * originalPath: '*'`

---

## Root Cause

- Express 5 uses a newer **path-to-regexp** library.
    
- In this version, `"*"` is **no longer a valid route pattern**.
    
- Wildcards now require **named parameters**.
    
- Therefore, `app.get("*")` throws an error.
    

---

## Correct Way to Handle Catch-All Routes in Express 5

### Option 1

`app.get("/*", (req, res) => {     res.send("404 error"); });`

### Option 2 (Recommended)

`app.use((req, res) => {     res.status(404).send("404 error"); });`

---

## Why `app.use()` is Recommended for 404

- Handles **all HTTP methods** (GET, POST, PUT, DELETE, etc.)
    
- Official and future-proof approach
    
- Cleaner and standard middleware pattern
    

---

## Correct Working Example (Express 5)

`const express = require('express'); const app = express();  app.get("/", (req, res) => {     res.send("Hello World!"); });  // 404 Catch-all app.use((req, res) => {     res.status(404).send("404 error"); });  app.listen(3000, () => console.log("Server running on port 3000"));`

---

## Key Learning Point (Interview / Exam)

> In Express 5, `"*"` route patterns are invalid due to changes in `path-to-regexp`.  
> Use `app.use()` middleware for implementing catch-all 404 routes.