# EXPRESS MIDDLEWARE NOTES

---

## 1. What is Express

Express.js is a widely used Node.js framework known for its simplicity and flexibility in building web applications and APIs.

---

## 2. What is Middleware

Middleware is a function that has access to:

- Request object (req)
- Response object (res)
- Next function (next)

It works in the **request-response cycle**.

---

## 3. Definition

Middleware is a request handler that allows you to intercept and manipulate requests and responses before they reach route handlers.

---

## 4. Syntax of Middleware

function middleware(req, res, next) {  
    // logic  
    next();  
}

---

## 5. Role of next()

- `next()` is used to pass control to the next middleware
- If not called, request will hang

---

## 6. What Middleware Can Do

Middleware functions can:

- Execute any code
- Modify request object
- Modify response object
- End request-response cycle
- Call next middleware

---

## 7. Middleware Flow

Request → Middleware 1 → Middleware 2 → Route → Response

---

## 8. Example Code

---

### index.js

const express = require("express");  
const app = express();  
  
const resFilter = require("./middleware");  
  
app.use(resFilter);  
  
app.listen(3000);

---

### middleware.js

const fs = require("fs");  
  
const resultFilter = (req, res, next) => {  
  console.log("Hello from middleware...");  
    
  return res.json({ data: "hello" });  
  
  next();  
};  
  
const logfile = (req, res, next) => {  
  console.log("Middleware second call......");  
  
  const date = new Date();  
  
  fs.appendFile(  
    "log.txt",  
    `${date.getDate()}/${date.getMonth()+1}/${date.getFullYear()} : ${req.method} : ${req.path}\n`,  
    (err) => {  
      if (err) console.log(err);  
      console.log("log file generated...");  
    }  
  );  
  
  next();  
};  
  
module.exports = resultFilter;

---

## Important Note

- `return res.json()` ends the response
- So `next()` will NOT execute after that

---

## 9. Types of Middleware

---

### 1. Application Level Middleware

- Applied using `app.use()`
- Works for all routes

app.use(middlewareFunction);

---

### 2. Router Level Middleware

- Applied using router object

const router = express.Router();  
router.use(middlewareFunction);

- Works for specific routes

---

### 3. Error Handling Middleware

Used to handle errors in application.

---

## Error Types

---

### 1. Operational Errors

Predictable errors:

- Invalid route
- Invalid input
- Server connection issue
- Timeout

Handled using middleware

---

### 2. Programming Errors

Developer mistakes:

- Undefined variable
- Wrong syntax
- Logical bugs

Need debugging

---

## Error Handling Middleware Syntax

function errorHandler(err, req, res, next) {  
    res.status(500).json({ error: err.message });  
}

---

## Important Point

- Must have 4 parameters:  
    err, req, res, next
- Automatically called when error occurs

---

## Middleware Types (Other)

- Built-in middleware
- Third-party middleware

---

## 10. CRUD Operations Example

---

### DELETE API

app.delete('/api/users/:id', (req, res) => {  
    const id = Number(req.params.id);  
  
    const users = JSON.parse(fs.readFileSync('./users_400.json', 'utf-8'));  
  
    const filteredUsers = users.filter(user => user.id !== id);  
  
    fs.writeFileSync('./users_400.json', JSON.stringify(filteredUsers, null, 2));  
  
    res.json({ message: "User deleted" });  
});

---

### PATCH API

app.patch('/api/users/:id', (req, res) => {  
    const id = Number(req.params.id);  
    const updates = req.body;  
  
    const users = JSON.parse(fs.readFileSync('./users_400.json', 'utf-8'));  
  
    const updatedUsers = users.map(user =>  
        user.id === id ? { ...user, ...updates } : user  
    );  
  
    fs.writeFileSync('./users_400.json', JSON.stringify(updatedUsers, null, 2));  
  
    res.json({ message: "User updated" });  
});

---

## Explanation

### DELETE

- Reads file
- Removes user by id
- Writes updated data

---

### PATCH

- Reads file
- Updates matching user
- Saves updated data

---

## 11. Key Points for Exams

- Middleware runs before route handler
- next() passes control
- res.json() ends request
- Error middleware has 4 parameters
- app.use() is application-level middleware
- Router middleware works on specific routes

---

## 12. One Line Note

Middleware in Express is a function that processes requests and responses before reaching the final route handler and can modify, stop, or forward the request.