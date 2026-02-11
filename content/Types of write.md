# Node.js File Writing Methods (fs Module)


## 1️ `fs.writeSync()`

###  Definition

- Synchronously writes data to a file using a **file descriptor (fd)**.
    
- **Low-level API**
    

### Key Points

- Blocks the **event loop**
    
- Requires manual:
    
    - `fs.openSync()`
        
    - `fs.closeSync()`
        
- Allows **partial writes**
    

###  Syntax

`fs.writeSync(fd, data)`

###  Use Case

- Writing chunks of data
    
- Low-level file operations
    
-  Not suitable for servers
    

---

## 2️ `fs.writeFileSync()`

###  Definition

- Synchronously writes data to a file using **file path**
    
- **High-level API**
    

###  Key Points

- Blocks the **event loop**
    
- Automatically opens & closes file
    
- Overwrites file by default
    

###  Syntax

`fs.writeFileSync(path, data, options)`

###  Use Case

- Small scripts
    
- Configuration files
    
- CLI tools
    
-  Avoid in production servers
    

---

## 3️ `fs.writeFile()`

###  Definition

- Asynchronously writes data to a file
    
- **Non-blocking API**
    

###  Key Points

- Does **not block** event loop
    
- Recommended for **servers & APIs**
    
- Supports callback & Promise
    

###  Syntax

`fs.writeFile(path, data, callback)`

###  Promise Version

`await fs.promises.writeFile(path, data)`

###  Use Case

- Backend servers
    
- Microservices
    
- Production applications
    

---

##  Comparison Table

| Feature                | writeSync | writeFileSync | writeFile |
| ---------------------- | --------- | ------------- | --------- |
| API Level              | Low       | High          | High      |
| Blocking               | Yes       | Yes           | No        |
| Async                  | No        | No            | Yes       |
| File Descriptor Needed | Yes       | No            | No        |
| Auto Open/Close        | No        | Yes           | Yes       |
| Server Usage           | No        | No            | Yes       |

---

##  Important Notes

- **Default behavior** → Overwrites existing file
    
- Use `{ flag: 'a' }` to **append**
    
- Avoid synchronous methods in **HTTP servers**
    

---

##  Interview One-Liners

- `writeSync()` → Low-level, fd-based, blocking
    
- `writeFileSync()` → High-level, blocking
    
- `writeFile()` → High-level, async, best for servers
    

---

##  Best Practice

 Use **`fs.writeFile()` or Streams** in production  
 Avoid **Sync methods** inside APIs or servers