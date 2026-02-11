# Express.js

## What is Express.js?

**Express.js** is a **minimal and flexible Node.js web application framework** that provides a robust set of features for building **web applications and APIs**.

It simplifies the process of building web servers and APIs by providing tools and middleware to handle tasks such as:

- Routing
    
- Request handling
    
- Response management
    

---

## What is Middleware?

Middleware is just like a **function** that works **between the request and response** cycle.

Example tasks handled by middleware:

- Authentication
    
- Logging (information storage)
    
- Parsing request bodies (HTTP protocol content handling)
    

---

## Key Features of Express.js

### 1. Middleware Support

Express uses middleware functions to handle requests.

Middleware can perform tasks such as:

- Logging
    
- Authentication
    
- Parsing request bodies
    

---

### 2. Routing

Express provides a powerful routing system to define routes for different HTTP methods:

|HTTP Method|Purpose|Example Use|
|---|---|---|
|GET|Fetch/Search data|Fetch user data|
|POST|Submit data|Signup form|
|PUT|Update data|Update profile|
|DELETE|Delete data|Remove account|
|PATCH|Partial update|Update specific field|

Routing decides which code should execute based on the HTTP request.

---

### 3. Template Engine Support (Dynamic HTML Rendering)

Express can integrate with various template engines to render dynamic HTML pages.

|Technology|Template Engine / Syntax|
|---|---|
|Express.js|EJS, Pug, Handlebars|
|Laravel (PHP)|Blade|
|CodeIgniter (PHP)|Views (PHP templates)|
|ASP.NET MVC / Core MVC|Razor / Razor Syntax|
|Java Spring|JTE, Thymeleaf, JSP|
|Python Django|Jinja|

These engines convert server-side code into HTML.

---

### 4. Error Handling

Express has a built-in error handling mechanism that allows defining custom error-handling middleware.

---

### 5. Static File Serving

Express can serve static files easily, such as:

- HTML
    
- CSS
    
- JavaScript
    
- Images
    

These are essential parts of every web application.

---

### 6. RESTful API Development

Express is widely used to build RESTful APIs, providing a clean and efficient way to handle HTTP requests and responses.

---

## How Express.js Works with Node.js

Node.js is known for its:

- Non-blocking
    
- Event-driven architecture
    

This is excellent for building scalable network applications.

However, coding directly in Node.js can become verbose and complex, especially when handling routing and server logic.

**Express.js acts as a lightweight layer on top of Node.js**, simplifying these complexities while still using all Node.js capabilities.

---

## When to Use Express.js

Use Express.js when building:

- RESTful APIs
    
- Web applications (server-side rendered)
    
- Middleware-heavy applications (authentication, logging, error handling)
    

---

## Conclusion

Express.js simplifies the process of creating robust web applications using Node.js.  
With its middleware support, routing, and flexibility, it is widely used for server-side applications and APIs.

As you gain more experience, you can explore its extensive middleware and routing capabilities to build complex applications.

---

# Installation of Express.js

### Step 1: Create Project Directory

`cd Desktop mkdir myexpressapp cd myexpressapp`

### Step 2: Initialize Node Project

`npm init`

This creates a `package.json` file.

### Step 3: Create Entry Point File

Create `index.js` (set as entry point in `package.json`).

### Step 4: Install Express

`npm install express`

Other commands:

|Command|Purpose|
|---|---|
|npm uninstall express|Remove express|
|npm install express@next|Install latest version|
|npm install express --no-save|Temporary install (not added to dependencies)|

---

## Node.js Version Requirement

|Express Version|Required Node.js Version|
|---|---|
|Express 4.x|Node.js 0.10 or higher|
|Express 5.x|Node.js 18 or higher|

Current Express version: **5.2.1** (Nov 2025)

---

# Getting Started with Express.js

Create a file `index.js` and write:

`const express = require('express');  var app = express();  // Creating route for home page app.get('/', (request, response) => {     response.send('Hello, welcome to our home screen!!'); });  // Start server app.listen(8000);`

### Explanation

- `require('express')` → imports the Express package.
    
- `express()` → works like a class constructor.
    
- `app` → acts like an object containing all Express functionality.
    
- `app.get()` → defines a route for HTTP GET request.
    
- `response.send()` → sends response to client.
    
- `app.listen(8000)` → starts the server on port 8000.