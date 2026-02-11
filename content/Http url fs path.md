## HTTP Server using `http`, `url`, `fs`, and `path` Modules

---

## 1. Objective of the Program

The objective of this program is to demonstrate real-world usage of Node.js core modules by creating a basic backend server that:

- Handles HTTP requests and responses
    
- Parses URLs and query parameters
    
- Serves static HTML files
    
- Logs each request
    
- Stores user data in a file
    
- Handles errors and 404 responses
    

---

## 2. Modules Used

### 2.1 http Module

Used to create an HTTP server and handle client requests.

`const http = require("http");`

Responsibilities:

- Create server
    
- Listen on a port
    
- Handle request–response lifecycle
    

---

### 2.2 url Module

Used to parse request URLs and extract routing and query parameters.

`const url = require("url");`

Responsibilities:

- Extract pathname
    
- Extract query parameters
    

---

### 2.3 fs Module

Used for file system operations such as reading and writing files.

`const fs = require("fs");`

Responsibilities:

- Read HTML files
    
- Append logs
    
- Store user data persistently
    

---

### 2.4 path Module

Used to construct safe and platform-independent file paths.

`const path = require("path");`

Why needed:

- Prevents path errors
    
- Works across Windows, Linux, macOS
    
- Avoids Internal Server Error
    

---

## 3. Server Configuration

`const PORT = 8000;`

- Server runs on port 8000
    
- Access URL: `http://localhost:8000`
    

---

## 4. Request Logging Function

``function logRequest(url, method) {     const log = `${new Date().toISOString()} | ${method} | ${url}\n`;     fs.appendFile("server.log", log, () => {}); }``

Purpose:

- Logs date, time, HTTP method, and URL
    
- Stores logs in `server.log`
    
- Used for monitoring and debugging
    

---

## 5. Creating the HTTP Server

`const server = http.createServer((req, res) => {`

Explanation:

- `req` → request object (client data)
    
- `res` → response object (server reply)
    
- Callback runs for every request
    

---

## 6. URL Parsing

`const parsedUrl = url.parse(req.url, true); const pathname = parsedUrl.pathname;`

Purpose:

- Separates route and query parameters
    

Example Request:

`/save-user?name=Akki&role=Backend`

Parsed Output:

- pathname → `/save-user`
    
- query → `{ name: "Akki", role: "Backend" }`
    

---

## 7. Logging Each Request

`logRequest(pathname, req.method);`

- Logs every incoming request automatically
    
- Helps track API usage and access patterns
    

---

## 8. File Path Construction Using __dirname

`const homePath = path.join(__dirname, "pages", "home.html"); const aboutPath = path.join(__dirname, "pages", "about.html");`

Reason:

- Ensures correct file location
    
- Prevents file-not-found errors
    
- Recommended industry practice
    

---

## 9. Routing Using Switch Case

`switch (pathname) {`

Purpose:

- Routes requests based on URL path
    
- Similar to Express routing but manual
    

---

## 10. Home Page Route

`case "/":`

Functionality:

- Reads `home.html`
    
- Sends HTML response
    
- Handles file read errors
    

Response Type:

`Content-Type: text/html`

---

## 11. About Page Route

`case "/about":`

Functionality:

- Reads `about.html`
    
- Sends HTML response
    
- Uses same logic as home page
    

---

## 12. Save User API

`case "/save-user":`

Example URL:

`/save-user?name=Akki&role=Backend`

---

### 12.1 Query Validation

`if (!name || !role) {     res.writeHead(400);     return res.end("Missing name or role"); }`

Purpose:

- Prevents invalid requests
    
- Returns HTTP 400 Bad Request
    

---

### 12.2 Saving User Data

`fs.appendFile("users.txt", userData, (err) => {`

Purpose:

- Stores user data persistently
    
- Acts as file-based database
    
- Creates file automatically if missing
    

---

## 13. 404 Error Handling

`default:     res.writeHead(404);     res.end("404 - Page Not Found");`

Purpose:

- Handles invalid URLs
    
- Prevents server crash
    
- Improves user experience
    

---

## 14. Starting the Server

``server.listen(PORT, () => {     console.log(`Server running at http://localhost:${PORT}`); });``

Function:

- Starts server
    
- Confirms successful execution
    

---

## 15. Project Folder Structure

`project/ │── server.js │── server.log │── users.txt │ └── pages/     ├── home.html     └── about.html`

---

## 16. Key Learning Outcomes

- Understanding HTTP server creation
    
- URL parsing and routing
    
- File system operations
    
- Error handling in Node.js
    
- Backend fundamentals without frameworks
    

---

## 17. Interview-Oriented Points

- Always use `__dirname` with fs
    
- Node.js is asynchronous by default
    
- Core modules can build backend without Express
    
- Logging is essential in production systems