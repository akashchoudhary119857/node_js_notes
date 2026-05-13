# SESSION BASED AUTHENTICATION IN NODE.JS USING EXPRESS AND EJS

---

## 1. What is Session

A session is a server-side mechanism used to store user data across multiple requests.

HTTP is stateless, so sessions help maintain:

- Login state
- User identity
- Navigation access

---

## 2. Technologies Used

- Node.js
- Express.js
- EJS
- express-session

---

## 3. Project Structure

project/  
│  
├── app.js  
├── package.json  
├── views/  
│   ├── login.ejs  
│   ├── home.ejs  
│   ├── product.ejs  
│   └── logout.ejs

---

## 4. Installation

npm init -y  
npm install express express-session ejs

---

## 5. Session Setup Code (app.js)

const express = require("express");  
const session = require("express-session");  
const path = require("path");  
  
const app = express();  
  
// Middleware to read form data  
app.use(express.urlencoded({ extended: true }));  
  
// Session Middleware  
app.use(  
  session({  
    secret: "mySecretKey",  
    resave: false,  
    saveUninitialized: false,  
    cookie: {  
      maxAge: 5 * 60 * 1000  
    }  
  })  
);  
  
// View Engine Setup  
app.set("view engine", "ejs");  
app.set("views", path.join(__dirname, "views"));

---

## 6. Routes Explanation

---

### Login Page Route

app.get("/", (req, res) => {  
  if (req.session.user) {  
    return res.redirect("/home");  
  }  
  res.render("login");  
});

Explanation:

- Checks if session already exists
- If yes, redirects to home
- If no, shows login page

---

### Login Handler

app.post("/login", (req, res) => {  
  const { username } = req.body;  
  
  req.session.user = username;  
  
  res.redirect("/home");  
});

Explanation:

- Takes username from form
- Stores it in session
- Creates session ID
- Redirects to home

---

### Home Page

app.get("/home", (req, res) => {  
  if (!req.session.user) {  
    return res.redirect("/");  
  }  
  
  res.render("home", { user: req.session.user });  
});

Explanation:

- Checks session
- If not logged in, redirect to login
- If logged in, show home page

---

### Product Page

app.get("/product", (req, res) => {  
  if (!req.session.user) {  
    return res.redirect("/");  
  }  
  
  res.render("product", { user: req.session.user });  
});

Explanation:

- Same session check as home
- Only logged-in users can access

---

### Logout Route

app.get("/logout", (req, res) => {  
  req.session.destroy(() => {  
    res.render("logout");  
  });  
});

Explanation:

- Deletes session from server
- User becomes logged out
- Shows logout page

---

## 7. EJS Pages Summary

---

### login.ejs

- Form to take username
- Sends POST request to /login

---

### home.ejs

- Displays logged-in user
- Links to product and logout

---

### product.ejs

- Displays user info
- Navigation links

---

### logout.ejs

- Shows logout message
- Can include auto redirect

---

## 8. How Session Works Step by Step

1. User opens login page
2. User submits username
3. Server creates session:  
    req.session.user = username
4. Server generates session ID
5. Session ID sent as cookie:  
    connect.sid
6. Browser stores cookie
7. On next request:
    - Cookie sent automatically
    - Server matches session ID
    - Retrieves user data

---

## 9. Cookie and Session Relation

Browser stores:

connect.sid = abc123

Server stores:

abc123 maps to { user: "Akki" }

Session ID connects both.

---

## 10. Where Session Data is Stored

Default behavior:

- Stored in server memory
- No file created

Memory structure:

{  
  "abc123": { user: "Akki" }  
}

---

## 11. Why No Session File is Visible

Because default store is MemoryStore:

- Uses RAM
- Not stored on disk
- Lost on server restart

---

## 12. How to View Cookie in Browser

Steps:

1. Open browser developer tools
2. Go to Application tab
3. Click Cookies
4. Select your site

You will see:  
connect.sid

---

## 13. Types of Sessions

---

### Time Bound Session

- Expires after fixed time
- Controlled using maxAge

---

### Non Time Bound Session

- No expiry set
- Ends on logout or server restart

---

## 14. Security Checks in Code

- Prevent access without login:

if (!req.session.user) {  
  return res.redirect("/");  
}

- Prevent login page access after login:

if (req.session.user) {  
  return res.redirect("/home");  
}

---

## 15. Important Points for Exams

- Session is stored on server
- Cookie stores only session ID
- Session ID links client and server
- Default storage is memory
- No file is created unless custom store used
- Session destroyed on logout