# Cookies & Sessions – Complete Notes (Node.js)

# 1. What are Cookies?

Cookies are small pieces of data stored in the user’s browser (client-side).

- Sent by server → stored in browser
    
- Automatically sent with every request to the same domain
    

Example:

```json
{ "userId": "12345" }
```

Used to identify users across requests.

---

# 2. Create Cookies in Node.js (Express)

Install:

```
npm install cookie-parser
```

Code:

```js
const express = require('express');
const cookieParser = require('cookie-parser');

const app = express();
app.use(cookieParser());

// Set cookie
app.get('/set-cookie', (req, res) => {
    res.cookie('username', 'akki', {
        maxAge: 60000,
        httpOnly: true
    });
    res.send("Cookie set");
});

// Read cookie
app.get('/get-cookie', (req, res) => {
    res.send(req.cookies);
});
```

---

# 3. What is Session?

Session is server-side storage of user data.

- Data stored on server
    
- Client stores only session ID (in cookie)
    

Example:

Server:

```
sessionId: {
   userId: 123,
   role: "admin"
}
```

Browser:

```
sessionId=abc123
```

---

# 4. Create Session in Node.js

Install:

```
npm install express-session
```

Code:

```js
const express = require('express');
const session = require('express-session');

const app = express();

app.use(session({
    secret: 'mysecretkey',
    resave: false,
    saveUninitialized: true,
}));

// Set session
app.get('/login', (req, res) => {
    req.session.user = "Akki";
    res.send("Session created");
});

// Read session
app.get('/profile', (req, res) => {
    if (req.session.user) {
        res.send(`Welcome ${req.session.user}`);
    } else {
        res.send("Not logged in");
    }
});

// Destroy session
app.get('/logout', (req, res) => {
    req.session.destroy();
    res.send("Logged out");
});
```

---

# 5. Cookies vs Sessions (Difference)

|Feature|Cookies|Sessions|
|---|---|---|
|Storage|Browser|Server|
|Size limit|~4KB|Large|
|Security|Less secure|More secure|
|Data stored|Directly in cookie|Session ID only|
|Speed|Faster|Slightly slower|

---

# 6. Cookie Parameters (Attributes)

There is no fixed number, but around 8–10 commonly used.

Important ones:

1. name & value
    

```js
res.cookie("user", "akki");
```

2. maxAge
    

```js
maxAge: 60000
```

3. expires
    

```js
expires: new Date(Date.now() + 86400000)
```

4. httpOnly
    

```js
httpOnly: true
```

5. secure
    

```js
secure: true
```

6. sameSite
    

```js
sameSite: 'strict'
```

7. path
    

```js
path: '/'
```

8. domain
    

```js
domain: '.example.com'
```

9. signed
    

```js
signed: true
```

---

# 7. Cookie Use Cases

- Authentication token
    
- Theme (dark/light)
    
- Language settings
    
- Shopping cart
    

---

# 8. Ways to End Cookies

Method 1:

```js
res.clearCookie("username");
```

Method 2:

```js
res.cookie("username", "", { expires: new Date(0) });
```

Method 3:

```js
res.cookie("username", "", { maxAge: 0 });
```

Important: path/domain must match original cookie.

---

# 9. Ways to End Sessions

Destroy session:

```js
req.session.destroy();
```

Remove specific data:

```js
delete req.session.user;
```

Regenerate session:

```js
req.session.regenerate(() => {});
```

Auto expiry:

```js
cookie: { maxAge: 60000 }
```

---

# 10. Proper Logout (Best Practice)

```js
app.get('/logout', (req, res) => {
    req.session.destroy(() => {
        res.clearCookie('connect.sid');
        res.send("Logged out");
    });
});
```

---

# 11. How Cookies + Sessions Work Together

1. User logs in
    
2. Server creates session
    
3. Server sends session ID in cookie
    
4. Browser stores cookie
    
5. Every request sends cookie → server verifies session
    

---

# 12. When to Use What?

Use Cookies:

- Preferences
    
- Small non-sensitive data
    

Use Sessions:

- Authentication
    
- Secure user data
    

---

# 13. Common Mistakes

- Storing passwords in cookies
    
- Not using httpOnly
    
- Not using secure in production
    
- Not clearing both session and cookie
    

---

# 14. Interview One-Liner

Cookies store small data in the browser, while sessions store user data on the server and use cookies only to maintain a session ID.

---

# 15. Advanced Topics

- Redis for session storage
    
- JWT vs Sessions
    
- Cookie + JWT authentication
    

---

# Final Summary

- Cookies → client-side
    
- Sessions → server-side
    
- Used together for authentication
    
- Always clear both during logout
    

---