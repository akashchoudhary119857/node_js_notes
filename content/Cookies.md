Node Express Cookies XSS and cookie parser Notes

---

1. Installation and Setup

Code

npm init -y   or
npm init
npm install express cookie-parser

Explanation  
Initializes Node project and installs required dependencies

---

2. Basic Express Server with Cookies

Code

const express = require('express');  
const cookieParser = require('cookie-parser');  
  
const app = express();  
  
// Middleware to parse cookies  
app.use(cookieParser());  
  
// Route to set a cookie  
app.get('/set-cookie', (req, res) => {  
    res.cookie('username', 'Akki', {  
        maxAge: 24 * 60 * 60 * 1000, // 1 day  
        httpOnly: true, // prevents JavaScript access  
        secure: false   // use true in HTTPS  
    });  
  
    res.send('Cookie has been set');  
});  
  
// Route to read cookie  
app.get('/get-cookie', (req, res) => {  
    const user = req.cookies.username;  
  
    if (user) {  
        res.send('Cookie value is ' + user);  
    } else {  
        res.send('No cookie found');  
    }  
});  
  
// Route to delete cookie  
app.get('/delete-cookie', (req, res) => {  
    res.clearCookie('username');  
    res.send('Cookie deleted');  
});  
  
// Start server  
app.listen(3000, () => {  
    console.log('Server running on http://localhost:3000');  
});

Explanation  
res.cookie sets a cookie  
req.cookies reads cookies  
res.clearCookie deletes cookies  
cookie parser middleware enables cookie reading

---

3. Signed Cookies Implementation

Code

const cookieParser = require('cookie-parser');  
  
// use secret key  
app.use(cookieParser('secretKey123'));  
  
// set signed cookie  
app.get('/set-signed-cookie', (req, res) => {  
    res.cookie('token', 'secureData', { signed: true });  
    res.send('Signed cookie set');  
});  
  
// get signed cookie  
app.get('/get-signed-cookie', (req, res) => {  
    res.send(req.signedCookies);  
});

Explanation  
Signed cookies include a signature  
If cookie is modified it becomes invalid  
Returned value becomes false if tampered

Important  
Signed cookies are not encrypted  
They only prevent modification

---

4. What is XSS Attack

Definition  
XSS Cross Site Scripting is a vulnerability where attacker injects malicious JavaScript into web pages

Example

Code

<p>User comment: {{comment}}</p>

Malicious input

<script>alert('Hacked')</script>

Explanation  
If input is not sanitized script executes in user browser

---

Why XSS is dangerous

Can steal cookies using document.cookie  
Can hijack sessions  
Can redirect users  
Can perform actions as user

---

Prevention

Use httpOnly true in cookies  
Sanitize and validate inputs  
Escape HTML output  
Use security libraries

---

5. How Signed Cookies Work Internally

Concept

Code

res.cookie('user', 'Akki', { signed: true });

Internal representation

user equals Akki dot signature

Verification

Server recalculates signature and compares

Code

req.signedCookies.user

Results  
Valid cookie returns value  
Modified cookie returns false

---

6. Why cookie parser Middleware is Required

Problem  
Express cannot read cookies directly

---

Without cookie parser

Code

console.log(req.cookies);

Output  
undefined

---

With cookie parser

Code

app.use(cookieParser());  
  
console.log(req.cookies);

Output

username Akki

---

Internal Working

Browser sends

Cookie username equals Akki semicolon token equals one two three

Converted to

Code

req.cookies = {  
  username: "Akki",  
  token: "123"  
};

---

7. Security Best Practices

Code

res.cookie('token', 'value', {  
    httpOnly: true,  
    secure: true,  
    sameSite: 'strict'  
});

Explanation  
httpOnly prevents XSS cookie access  
secure ensures HTTPS only  
sameSite prevents CSRF attacks

---

8. Final Quick Revision

Cookies store data in browser  
cookie parser reads cookies into req.cookies  
Signed cookies prevent tampering  
XSS is script injection attack  
httpOnly helps protect cookies