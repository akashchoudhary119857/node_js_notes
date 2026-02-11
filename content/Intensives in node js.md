 
## 1. What is I/O (Input / Output)?

**I/O = Input / Output**

Any operation where a program communicates with the outside world.

### Input Examples

- Reading files from disk
    
- Reading data from databases
    
- Receiving network requests (API calls)
    
- User input (keyboard, forms)
    

### Output Examples

- Writing to files
    
- Writing to databases
    
- Sending HTTP responses
    
- Printing to console
    

### Common I/O in Node.js

- File I/O → `fs.readFile()`
    
- Database I/O → `db.find()`
    
- Network I/O → HTTP requests, APIs
    
- Response Output → `res.send()`
    

---

## 2. What is I/O-Intensive?

**Definition:**

> An application that spends most of its time _waiting for I/O operations_ rather than performing CPU calculations.

### Simple Meaning

- Waiting → I/O-intensive
    
- Calculating → CPU-intensive
    

### I/O-Intensive Application Examples

- Web servers
    
- REST APIs
    
- Chat applications
    
- File upload / download systems
    
- Database-heavy systems
    

```js
app.get('/users', async (req, res) => {
  const users = await db.find(); // waiting for DB
  res.json(users);
});
```

Here:

- CPU work → very little
    
- Waiting for DB/network → most time
    

---

## 3. What is NOT I/O-Intensive?

**CPU-Intensive Tasks**

- Image processing
    
- Video encoding
    
- Cryptographic loops
    
- Large mathematical calculations
    
- Machine learning training
    

```js
for (let i = 0; i < 1e9; i++) {}
```

note : Node.js is **not ideal** for heavy CPU work on the main thread.

---

## 4. Why Node.js is Great for I/O-Intensive Apps

- Non-blocking I/O
    
- Event-driven architecture
    
- Single thread handles many requests
    
- Uses callbacks, promises, async/await
    

Note : While one request waits for I/O, Node.js processes other requests.

---

## 5. What is libuv?

**libuv is a C library that provides:**

- Asynchronous I/O
    
- Event loop
    
- Thread pool
    

Node.js is written in JavaScript, but **real async power comes from libuv**.

---

## 6. Why libuv Exists

Operating systems differ:

- Linux, Windows, macOS have different async APIs
    

libuv provides:

- A unified async API
    
- High performance
    
- Cross-platform support
    

---

## 7. Responsibilities of libuv

### libuv Handles

- Event loop
    
- Thread pool
    
- File system I/O
    
- Network I/O
    
- Timers
    
- DNS lookups
    
- Child processes
    

### libuv Does NOT Handle

- JavaScript execution
    
- Call stack
    
- Heap memory
    

(Handled by **V8 engine**)

---

## 8. Node.js Architecture

```
JavaScript Code
      ↓
Node.js APIs (fs, http, timers)
      ↓
libuv (C library)
      ↓
Operating System
```

---

## 9. How Async I/O Works Internally

```js
fs.readFile('data.txt', callback);
```

Steps:

1. JS calls Node API
    
2. Node forwards request to libuv
    
3. libuv uses:
    
    - OS async APIs OR
        
    - Thread pool (if needed)
        
4. I/O completes
    
5. Callback queued
    
6. Event loop executes callback
    

---

## 10. libuv Thread Pool

- Default size: **4 threads**
    

### Used for:

- File system (`fs`)
    
- DNS (`dns.lookup`)
    
- Crypto
    
- Compression
    

Note : Network I/O does **not** use thread pool (handled by OS async APIs).

### Example

```js
fs.readFile('a.txt', cb);
fs.readFile('b.txt', cb);
fs.readFile('c.txt', cb);
fs.readFile('d.txt', cb);
fs.readFile('e.txt', cb);
```

- First 4 → thread pool
    
- 5th → waits
    

### Increase Thread Pool Size

```bash
UV_THREADPOOL_SIZE=8 node app.js
```

---

## 11. libuv vs V8

| Feature              | V8  | libuv |
| -------------------- | --- | ----- |
| JavaScript execution | Yes | No    |
| Event loop           | No  | Yes   |
| Thread pool          | No  | Yes   |
| Async I/O            | No  | Yes   |
| Memory management    | Yes | No    |

---

## 12. Event Loop (Core of Node.js)

**Definition:**

> The event loop decides when and which callback is executed.

Runs continuously while the Node.js process is alive.

---

## 13. Event Loop Phases (In Order)

1. **Timers Phase**
    
    - `setTimeout`, `setInterval`
        
2. **Pending Callbacks**
    
    - Deferred system callbacks
        
3. **Idle / Prepare**
    
    - Internal use
        
4. **Poll Phase (MOST IMPORTANT)**
    
    - I/O callbacks
        
    - File, DB, network responses
        
5. **Check Phase**
    
    - `setImmediate`
        
6. **Close Callbacks**
    
    - `socket.close()`
        

---

## 14. Event Loop Mental Diagram

```
Timers
Pending Callbacks
Idle / Prepare
Poll  
Check
Close Callbacks
(repeat)
```

---

## 15. Microtasks Queue (Very Important)

Runs **after every phase**.

Includes:

- `process.nextTick()` (highest priority)
    
- `Promise.then()`
    
- `queueMicrotask()`
    

Note: Too many microtasks can starve the event loop.

---

## 16. Priority Order

1. `process.nextTick()`
    
2. `Promise.then()`
    
3. Timers / I/O / `setImmediate`
    

---

## 17. Classic Interview Output Example

```js
setTimeout(() => console.log('timeout'), 0);
setImmediate(() => console.log('immediate'));
Promise.resolve().then(() => console.log('promise'));
process.nextTick(() => console.log('nextTick'));
console.log('start');
```

Output:

```
start
nextTick
promise
timeout OR immediate
```

---

## 18. Why CPU Blocking is Dangerous

```js
while (true) {}
```

- Event loop blocked
    
- No callbacks executed
    
- Server freezes
    

---

## 19. Handling CPU-Heavy Work

Solutions:

- Worker Threads
    
- Child Processes
    
- Microservices
    

---

## 20. One-Line Interview Answers

- **I/O-intensive:** Applications that spend most time waiting for I/O operations.
    
- **libuv:** C library providing async I/O, event loop, and thread pool.
    
- **Event loop:** Mechanism that executes async callbacks in defined phases.
    
- **Node.js threading:** Single-threaded JS with multi-threaded I/O via libuv.
    

---

## 21. When to Use Node.js

 APIs  
 Real-time apps  
 Chat systems  
 Streaming apps  
 Heavy CPU computation

---
