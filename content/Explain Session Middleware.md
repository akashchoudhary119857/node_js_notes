# PART 1: Session Middleware

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

---

## What this line does

app.use(session(...))

 Registers **session middleware** in your Express app.

This middleware:

- Creates `req.session` object
- Manages session ID
- Handles cookies automatically

Without this, `req.session` will not exist.

---

## Step-by-Step Internal Working

### Step 1: Incoming Request

User sends request:

GET /home

---

### Step 2: Middleware Checks Cookie

Browser sends:

Cookie: connect.sid=abc123

---

### Step 3: Session Lookup

Server checks memory:

abc123 → { user: "Akki" }

If found:

req.session = { user: "Akki" }

If not found:

req.session = {}

---

## Now Understand Each Parameter

---

### 1. secret

secret: "mySecretKey"

Purpose:

- Used to **sign and secure session ID cookie**

Why needed:

- Prevents tampering with cookie
- Adds hash to session ID

Without it:

- Session middleware will not work

---

### 2. resave

resave: false

Meaning:

- Do NOT save session again if nothing changed

If true:

- Session saved on every request (wasteful)

Best practice:

- Keep false

---

### 3. saveUninitialized

saveUninitialized: false

Meaning:

- Do NOT create session until something is stored

Example:

Before login:

req.session = {}

 No session stored

After login:

req.session.user = "Akki"

 Now session is saved

---

### 4. cookie.maxAge

maxAge: 5 * 60 * 1000

Meaning:

- Session expires after 5 minutes

Internally:

- Cookie gets expiry time
- After that:
    - Cookie invalid
    - Session ignored

---

## Summary of Part 1

This middleware:

- Creates session system
- Links cookie with server data
- Controls session lifetime

---

# PART 2: Login Route

app.post("/login", (req, res) => {  
  const { username } = req.body;  
  
  req.session.user = username;  
  
  res.redirect("/home");  
});

---

## Step-by-Step Working

---

### Step 1: Form Submission

User submits form:

POST /login

Body:

{ username: "Akki" }

---

### Step 2: Extract Data

const { username } = req.body;

 Reads form data

---

### Step 3: Create Session

req.session.user = username;

This is the **most important line**

---

## What Happens Internally Here

1. If session does not exist:
    - New session created
2. Server generates session ID:

abc123xyz

3. Stores data in memory:

{  
  "abc123xyz": {  
    user: "Akki"  
  }  
}

4. Sends cookie to browser:

Set-Cookie: connect.sid=abc123xyz

---

### Step 4: Redirect

res.redirect("/home");

Now browser sends:

Cookie: connect.sid=abc123xyz

Server reads session:

req.session.user → "Akki"

---

# Full Flow (Combined)

1. Session middleware initializes system
2. User logs in
3. `req.session.user` is set
4. Session stored in server memory
5. Session ID sent as cookie
6. Browser sends cookie on every request
7. Server identifies user using session ID

---

# Key Concept

req.session.user = username;

 This line converts:

- Anonymous user → Authenticated user

---

# Common Mistake Students Make

They think:

Session stored in browser

Wrong

Correct:

- Browser → stores only session ID
- Server → stores actual data

---

# One-Line note

The session middleware initializes and manages sessions, while assigning a value to req.session during login creates a session, stores user data on the server, and links it with a session ID sent to the client via cookies.