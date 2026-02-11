#  Web Browsers, JavaScript Engines & Node.js – Notes

---

## 1. What is a Web Browser?
A **web browser** is a software application used to access, retrieve, and display web content from servers using HTTP/HTTPS.

### Examples
- Google Chrome
- Mozilla Firefox
- Apple Safari
- Microsoft Edge

---

## 2. Core Components of a Browser
A browser mainly consists of:
1. **Rendering Engine**
2. **JavaScript Engine**

---

## 3. Rendering Engine
The **Rendering Engine** is responsible for:
- Parsing HTML
- Applying CSS styles
- Constructing DOM and Render Tree
- Displaying content on the screen

### Common Rendering Engines
- Blink
- Gecko
- WebKit
- Trident (Deprecated)

---

## 4. JavaScript Engine
The **JavaScript Engine**:
- Parses JavaScript code
- Converts it into machine code
- Executes JavaScript efficiently

### Common JavaScript Engines
- V8
- SpiderMonkey
- JavaScriptCore
- Chakra(deptreceted)

---

## 5. Browsers with Their Engines

| Browser | JavaScript Engine | Rendering Engine |
|-------|------------------|------------------|
| Google Chrome | V8 | Blink |
| Microsoft Edge | V8 | Blink |
| Mozilla Firefox | SpiderMonkey | Gecko |
| Apple Safari | JavaScriptCore | WebKit |
| Opera | V8 | Blink |
| Brave | V8 | Blink |
| Internet Explorer | Chakra | Trident |

---

## 6. Limitation of JavaScript Before Node.js
Before Node.js:
- JavaScript worked only inside browsers
- No access to file system or OS
- Could not build scalable server-side applications
- Servers used blocking, thread-based models

---

## 7. Who Designed Node.js?
- **Designer:** Ryan Dahl  
- **Year:** 2009  
- **Announcement:** JSConf EU  

---

## 8. Why Node.js Was Created
Traditional servers had issues like:
- Blocking I/O
- Poor scalability
- High memory usage

Node.js was created to:
- Use JavaScript on the server
- Handle high concurrency
- Provide non-blocking I/O

---

## 9. What is Node.js?
> **Node.js is a runtime environment that allows JavaScript to run outside the browser.**

Node.js is:
-  Not a programming language
-  Not a framework
- A runtime environment

---

## 10. Is Node.js Only V8?
No.

### Actual Composition
Node.js = V8 + C++ + libuv + Node APIs

---
## 11. Role of V8 in Node.js
- Written in C++
- Executes JavaScript code
- Uses Just-In-Time (JIT) compilation
- Provides high-performance execution

---

## 12. Why C++ Is Used in Node.js
JavaScript cannot:
- Access OS-level APIs
- Handle file systems directly
- Manage threads

C++ is used to:
- Build Node core modules (fs, http, net)
- Interact with the operating system
- Improve performance

---

## 13. What is libuv?
libuv is a C library that provides:
- Event loop
- Asynchronous I/O
- Thread pool
- Timers and networking

It enables **non-blocking behavior** in Node.js.

---

## 14. Node.js Event Loop (Working Steps)
1. Request arrives
2. Async task registered
3. Task handled by libuv
4. Event loop continues execution
5. Callback executed after task completion

---

## 15. Node.js Internal Architecture
JavaScript Code  
↓  
Node.js APIs (C++)  
↓  
V8 Engine  
↓  
libuv (Event Loop)  
↓  
Operating System

---

## 16. Significance of V8 + C++ in Node.js
- High performance execution
- Non-blocking I/O
- High scalability
- Cross-platform support
- Suitable for real-time applications

---

## 17. Points to be remember
- Browsers use rendering engines to display UI and JavaScript engines to execute logic.
- Node.js allows JavaScript to run outside the browser using V8.
- V8 provides speed, C++ provides system access, and libuv provides scalability.

---

## 18. Summary
> **Node.js combines V8 for fast JavaScript execution, C++ for system-level access, and libuv for non-blocking I/O to build scalable server-side applications.**



