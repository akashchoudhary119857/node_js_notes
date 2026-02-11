## Why this code WORKS (writeFile + readFile)

fs.writeFile(
  "dummy2.txt",
  "hello class welcome",
  { encoding: "utf-8", flag: "w" },
  (err) => {
    if (err) console.log(err);
    else console.log("file created");
  }
);

fs.readFile("dummy2.txt", "utf", (err, data) => {
  if (err) console.log(err);
  else console.log(data);
});


### Reason:

- `fs.writeFile()`
    
    - Opens the file
        
    - Writes data
        
    - **Closes the file automatically**
        
- `fs.readFile()`
    
    - **Reopens the file from the beginning**
        
    - Reads content normally
        

 These APIs are **high-level**, filename-based APIs  
Node manages file open/close  
 No file pointer issues

---

## 2️ Why `open + flag "w"` DOES NOT allow reading

Example:

const fh = fs.openSync("test.txt", "w");
fs.writeSync(fh, "hello");
fs.readSync(fh, buffer, 0, buffer.length);


### Problem #1: `"w"` means **WRITE ONLY**

`"w"  → write only "w+" → read + write`

So if you open with:

`fs.openSync("test.txt", "w");`

Reading is **not allowed at all**

That’s why read fails.

---

## 3️ Even with `"w+"` reading may fail — WHY?

Example:

const fh = fs.openSync("test.txt", "w+");
fs.writeSync(fh, "hello");
fs.readSync(fh, buffer, 0, buffer.length);

### Problem #2: File pointer is at the END

After writing:

`|hello| ← pointer here`

Reading starts from **current pointer**, so:

`nothing to read 

---

## 4️ Why `writeFile` does NOT have this problem

Because internally Node does this 

`open file write data close file   ← pointer destroyed`

Then `readFile`:

`open file (fresh pointer at 0) read data close file`

 That’s why it reads correctly

---

## 5️ Correct comparison table (VERY IMPORTANT)

| Method             | Uses FD? | Auto Close | Pointer Issue |
| ------------------ | -------- | ---------- | ------------- |
| `writeFile`        | No       | Yes        | No            |
| `readFile`         | No       | Yes        | No            |
| `open + writeSync` | Yes      | No         | Yes           |
| `open + readSync`  | Yes      | No         | Yes           |

---

## 6️ Correct way to read when using `open`

const fs = require("fs");

const fd = fs.openSync("demo.txt", "w+");
fs.writeSync(fd, "hello world");

const buffer = Buffer.alloc(20);

// reset pointer to 0
fs.readSync(fd, buffer, 0, buffer.length, 0);

console.log(buffer.toString());
fs.closeSync(fd);


---

## 7️ Interview-ready one-line answer 

> `writeFile` works because it closes the file after writing, so `readFile` reopens it from the beginning.  
> When using `open`, the file pointer stays at the end after writing, and if opened with `w` it is write-only, so reading is not allowed.

---

If you want, I can:

- Add this to **Node.js file system notes**
    
- Explain all flags (`r`, `r+`, `w`, `w+`, `a`, `a+`)
    
- Give **real-world use cases**

### Node.js `fs` (Sync) – One-Line Cheat Sheet

- `fs.writeFileSync(file, data)` → Write data (create/overwrite file, auto open & close)
    
- `fs.readFileSync(file, enc)` → Read entire file from start
    
- `fs.appendFileSync(file, data)` → Append data to file
    
- `fs.openSync(file, flag)` → Open file and return **file descriptor (fd)**
    
- `fs.writeSync(fd, data)` → Write to file using fd (moves file pointer)
    
- `fs.readSync(fd, buffer, off, len, pos)` → Read from fd (`pos` resets pointer)
    
- `fs.closeSync(fd)` → Close file descriptor
    
- `fs.existsSync(path)` → Check if file/folder exists
    
- `fs.unlinkSync(file)` → Delete file
    
- `fs.renameSync(old, new)` → Rename or move file
    
- `fs.mkdirSync(dir, { recursive:true })` → Create directory
    
- `fs.rmdirSync(dir)` → Remove directory
    
- `fs.statSync(path)` → Get file metadata
    
- `fs.copyFileSync(src, dest)` → Copy file

## Node.js `fs` – **One-Line Cheat Sheet (ASYNC)**

- `fs.writeFile(file, data, cb)` → Write data (auto open & close)
    
- `fs.readFile(file, enc, cb)` → Read entire file from start
    
- `fs.appendFile(file, data, cb)` → Append data to file
    
- `fs.open(file, flag, cb)` → Open file and get **file descriptor (fd)**
    
- `fs.write(fd, data, cb)` → Write using fd (moves file pointer)
    
- `fs.read(fd, buffer, off, len, pos, cb)` → Read using fd (`pos` controls pointer)
    
- `fs.close(fd, cb)` → Close file descriptor
    
- `fs.exists(path, cb)` → Check file/folder existence _(deprecated but asked in interviews)_
    
- `fs.unlink(file, cb)` → Delete file
    
- `fs.rename(old, new, cb)` → Rename / move file
    
- `fs.mkdir(dir, { recursive:true }, cb)` → Create directory
    
- `fs.stat(path, cb)` → File metadata