## 1. HTTP Module (Node.js)

- Built-in module to create HTTP servers
    
- Handles requests & responses
    
- Low-level (no routing, no middleware)
    

`const http = require("http");`

---

## 2. Why Do We Need a Server?

- Clients cannot access database directly
    
- Server provides:
    
    - Security
        
    - Authentication & authorization
        
    - Business logic
        
    - Validation
        
- Acts as **middle layer** between client & data
    

---

## 3. Why Create Server in Node.js?

- Event-driven
    
- Non-blocking I/O
    
- Best for APIs & real-time apps
    

`http.createServer((req, res) => {});`

---

## 4. Creating HTTP Server

`const server = http.createServer((req, res) => {   res.writeHead(200, { "Content-Type": "text/plain" });   res.end("Hello World"); }); server.listen(3000);`

---

## 5. Request Object (`req`)

|Property|Purpose|
|---|---|
|`req.method`|HTTP method|
|`req.url`|Endpoint|
|`req.headers`|Request headers|
|`req.socket`|Client info|

---

## 6. Response Object (`res`)

|Method|Purpose|
|---|---|
|`res.write()`|Write body|
|`res.end()`|End response|
|`res.setHeader()`|Set header|
|`res.writeHead()`|Status + headers|
|`res.statusCode`|Set status|

---

## 7. HTTP Methods – Meaning

|Method|Task|
|---|---|
|GET|Read data|
|POST|Create data|
|PUT|Update full|
|PATCH|Update partial|
|DELETE|Remove data|
|HEAD|Metadata only|
|OPTIONS|Allowed methods / CORS|

---

## 8. CRUD → HTTP Mapping

|CRUD|Method|
|---|---|
|Create|POST|
|Read|GET|
|Update|PUT / PATCH|
|Delete|DELETE|

---

## 9. HTTP Status Codes

### 2xx – Success

|Code|Meaning|
|---|---|
|200|OK|
|201|Created|
|202|Accepted|
|204|No Content|

### 4xx – Client Error

|Code|Meaning|
|---|---|
|400|Bad Request|
|401|Unauthorized|
|403|Forbidden|
|404|Not Found|
|405|Method Not Allowed|
|409|Conflict|
|422|Validation Error|

### 5xx – Server Error

|Code|Meaning|
|---|---|
|500|Internal Error|
|502|Bad Gateway|
|503|Service Down|
|504|Timeout|

---

## 10. Status Codes for CRUD

### CREATE (POST)

- 201 → Created
    
- 400 → Bad input
    
- 409 → Duplicate
    

### READ (GET)

- 200 → Success
    
- 404 → Not found
    

### UPDATE (PUT / PATCH)

- 200 → Updated
    
- 204 → No content
    
- 400 → Invalid data
    

### DELETE (DELETE)

- 204 → Deleted
    
- 404 → Not found
    

---

## 11. Request Headers (Client → Server)

|Header|Use|
|---|---|
|Content-Type|Body type|
|Authorization|Token|
|Accept|Expected response|
|User-Agent|Client info|
|Cookie|Client cookies|

**Common Types**

- application/json
    
- application/x-www-form-urlencoded
    
- multipart/form-data
    

---

## 12. Response Headers (Server → Client)

|Header|Use|
|---|---|
|Content-Type|Response format|
|Set-Cookie|Set cookies|
|Cache-Control|Cache rules|
|Location|Redirect|
|Access-Control-Allow-Origin|CORS|

---

## 13. Sending JSON Response

`res.writeHead(200, { "Content-Type": "application/json" }); res.end(JSON.stringify({ message: "OK" }));`

---

## 14. Reading JSON Body

`let body = ""; req.on("data", chunk => body += chunk); req.on("end", () => JSON.parse(body));`

---

## 15. What Are Web Servers?

- Software that handles HTTP requests & responses
    

### Examples

|Server|Platform|
|---|---|
|Apache|Cross-platform|
|Nginx|High performance|
|IIS|Microsoft|
|Node.js|JS runtime|
|Tomcat|Java|

---

## 16. IIS / Apache vs Node.js

|Feature|Apache / IIS|Node.js|
|---|---|---|
|Language|C/C++|JavaScript|
|Model|Multi-threaded|Event-driven|
|Best for|Static apps|APIs, real-time|

---

## 17. Port Number

- Logical endpoint for applications
    
- IP → machine
    
- Port → application
    

---

## 18. Why Ports Are Needed?

- Multiple apps on same machine
    
- OS routes request using port
    

---

## 19. Common Ports

|Port|Use|
|---|---|
|80|HTTP|
|443|HTTPS|
|3000|Node.js|
|8080|Alternate HTTP|
|3306|MySQL|
|5432|PostgreSQL|
|27017|MongoDB|

---

## 20. Server Binding to Port

`server.listen(3000);`

- OS binds Node process to port
    

---

## 21. One-Line Interview Answers

- HTTP module → built-in Node.js server module
    
- 201 → resource created
    
- 204 → success, no body
    
- Server → listens & responds
    
- Port → identifies application
    

---

## 22. Quick Revision

- CRUD → POST / GET / PUT / PATCH / DELETE
    
- Success → 2xx
    
- Client error → 4xx
    
- Server error → 5xx
    
- Headers = metadata