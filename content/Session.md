# SESSION IN NODE.JS NOTES

---

## What is a Session

A session is a server-side mechanism used to store user data across multiple requests.

It is used because HTTP is stateless.

Sessions help maintain:

- Login state
- User data
- Shopping cart

---

## Why Sessions are Needed

HTTP does not remember users.

Request 1 -> No memory  
Request 2 -> Treated as new request

Session solves this by storing user data on the server.

---

## How Session Works

1. User sends request such as login
2. Server creates a session object
3. Server generates a session ID
4. Session ID is sent to browser as a cookie
5. Browser stores the cookie
6. On next request:
    - Browser sends cookie automatically
    - Server reads session ID
    - Server fetches session data

---

## Key Concept

Cookie stores only session ID  
Session stores actual data

---

## Session and Cookie Link

Browser Cookie:  
connect.sid = abc123

Server Store:  
abc123 maps to user data

Session ID works like a key.

---

## Session Setup in Node.js

Install:

npm install express express-session

---

Basic Code:

const express = require("express");  
const session = require("express-session");  
  
const app = express();  
  
app.use(  
  session({  
    secret: "mySecretKey",  
    resave: false,  
    saveUninitialized: false,  
    cookie: { maxAge: 60000 }  
  })  
);  
  
app.get("/login", (req, res) => {  
  req.session.user = "Akki";  
  res.send("Session Created");  
});  
  
app.get("/profile", (req, res) => {  
  res.send(req.session.user);  
});  
  
app.listen(3000);

---

## Session Configuration Parameters

secret  
Required. Used to sign session ID

resave  
Controls whether session is saved again

saveUninitialized  
Controls saving empty sessions

cookie  
Used for cookie settings

---

## Minimum Required Configuration

session({  
  secret: "mySecretKey"  
});

---

## Where Session Data is Stored

Default:  
Stored in server memory

No file is created

Production:

- Redis
- MongoDB
- SQL databases

---

## Types of Sessions Based on Time

---

### Time Bound Session

Expires after a fixed time

Controlled using maxAge

cookie: { maxAge: 60000 }

Used in secure applications

---

### Non Time Bound Session

No fixed expiry

Ends when:

- User logs out
- Server restarts

No maxAge defined

Used in remember me functionality

---

## Cookie Types in Sessions

---

Session Cookie  
Deleted when browser closes

cookie: { maxAge: null }

---

Persistent Cookie  
Stored for fixed duration

cookie: { maxAge: 86400000 }

---

## Internal Storage Example

{  
  "abc123": {  
    user: "Akki"  
  }  
}

---

## Real Life Example

Cloakroom token system

Token is cookie  
Stored item is session data  
Token is used to retrieve data

---

## Best Practices

Use:

cookie: {  
  maxAge: 15 * 60 * 1000,  
  httpOnly: true,  
  secure: true  
}

Use database or Redis in production

Regenerate session after login:

req.session.regenerate(() => {  
  req.session.user = user;  
});