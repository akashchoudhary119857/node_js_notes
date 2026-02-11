# Node.js File Handling & Terminal Input – Complete Notes

---

## 1️ File System (`fs`) Module – Overview

- Built-in Node.js module
    
- Used to **read/write files**
    
- Supports:
    
    - Async
        
    - Sync
        
    - Streams (chunks)
        

`const fs = require("fs");`

---

## 2️ Writing Data to File (Whole Data)

`fs.writeFile("dummy.txt", "Hello Here is section FC", (err) => {   if (err) console.log(err);   else console.log("File written"); });`

### Characteristics

- Writes **entire content at once**
    
- Overwrites existing file
    
- Async & non-blocking
    

---

## 3️ Reading Data from File (Whole File)

`fs.readFile("dummy.txt", "utf8", (err, data) => {   if (err) console.log(err);   else console.log(data); });`

### Characteristics

- Reads **entire file into memory**
    
- Not suitable for large files
    

---

## 4️ What Is POSSIBLE With `fs.readFile`?

| Mode                   | Possible? | How           |
| ---------------------- | --------- | ------------- |
| Character by character | yes       | Loop string   |
| Word by word           | yes       | `split(" ")`  |
| Line by line           | yes       | `split("\n")` |
| Chunk by chunk         | no        | Needs streams |

---

## 5️ Character-by-Character Reading

`fs.readFile("dummy.txt", "utf8", (err, data) => {   for (let ch of data) {     console.log(ch);   } });`

 Logical processing, not OS-level

---

## 6️ Word-by-Word Reading

`fs.readFile("dummy.txt", "utf8", (err, data) => {   data.split(" ").forEach(word => console.log(word)); });`

---

## 7️ Line-by-Line Reading

`fs.readFile("dummy.txt", "utf8", (err, data) => {   data.split("\n").forEach(line => console.log(line)); });`

---

## 8️ Chunk-by-Chunk Reading (STREAMS) 

`const stream = fs.createReadStream("dummy.txt", {   encoding: "utf8",   highWaterMark: 8 });  stream.on("data", chunk => {   console.log(chunk); });`

### Used for:

- Large files
    
- Memory-efficient processing
    

---

## 9️ Character-by-Character Writing 

- Not efficient
    
- Possible logically but **not recommended**
    

`for (let ch of "Hello") {   fs.appendFileSync("dummy.txt", ch); }`

---

##  Word-by-Word Writing

`["Hello", "Node", "JS"].forEach(word => {   fs.appendFile("dummy.txt", word + " ", () => {}); });`

---

## 1️1️ Line-by-Line Writing

`["Line 1", "Line 2"].forEach(line => {   fs.appendFile("dummy.txt", line + "\n", () => {}); });`

---

## 1️2️ Chunk-by-Chunk Writing (BEST)

`const ws = fs.createWriteStream("dummy.txt");  ws.write("Hello "); ws.write("Node "); ws.write("Stream"); ws.end();`

---

## 1️3️ Reading Input from Terminal (User Input)

### Best Module: `readline`

---

## 1️4️ Single Line Input → File

`const readline = require("readline");  const rl = readline.createInterface({   input: process.stdin,   output: process.stdout });  rl.question("Enter text: ", (input) => {   fs.writeFile("input.txt", input, () => {     console.log("Saved");     rl.close();   }); });`

---

## 1️5️ Multiple Lines Input → File (Continuous)

`const readline = require("readline"); const stream = fs.createWriteStream("input.txt");  const rl = readline.createInterface({   input: process.stdin,   output: process.stdout });  rl.on("line", line => {   stream.write(line + "\n"); });`

Stop with `Ctrl + C`

---

## 1️6️ Using `process.stdin` (Low-Level)

`process.stdin.on("data", data => {   fs.appendFileSync("input.txt", data); });`

---

## 1️7️ Comparison of Methods

|Task|Best API|
|---|---|
|Small file|`fs.readFile`|
|Large file|Streams|
|Chunk processing|Streams|
|Terminal input|`readline`|
|Continuous input|`stdin`|

---

## 1️8️ What Is NOT Possible Directly

- OS-level character-by-character read
    
- Chunk reading using `fs.readFile`
    

---

## 1️9️ Important Concepts

- `fs.readFile` → loads full file
    
- Streams → read/write in parts
    
- Terminal input → stream based
    
- String splitting ≠ real file streaming
    

---

## 2️0️ Interview One-Line Answers

- `fs.readFile` reads entire file into memory
    
- Streams are memory-efficient
    
- Character/word/line reading is logical processing
    
- Terminal input is a stream (`stdin`)
    
- Best for large files → streams
    

---

## 2️1️ Quick Revision Cheat

- Whole file → `fs.readFile`
    
- Chunk → `createReadStream`
    
- Write chunks → `createWriteStream`
    
- Terminal input → `readline`
    
- Large data → streams only
    

---

##  FINAL SUMMARY

 Reading & writing can be done:

- Whole
    
- Character
    
- Word
    
- Line
    
- Chunk
    

 **True chunking** → streams  
 **Terminal input** → `readline` / `stdin`