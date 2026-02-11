# Node.js File System & Data Reading – Complete Notes

These notes combine **all previous explanations**: file reading methods, chunks, lines, words, characters, streams, and best practices. Suitable for **exams, interviews, and real-world usage**.

---

## 1️ Node.js File System (fs) Module

### What is `fs`?

- Built-in Node.js module
    
- Used to interact with the **file system**
    
- Supports **sync**, **async**, and **stream-based** operations
    

const fs = require('fs');

---

## 2️ Ways to Read a File in Node.js

### A. Read Complete File at Once

fs.readFile('data.txt', 'utf8', (err, data) => {

if (err) throw err;

console.log(data);

});

**Characteristics**

- Reads entire file into memory
    
- Preserves **actual file content & new lines**
    
- Not suitable for very large files
    

---

### B. Read File Line by Line (Best Practice)

const readline = require('readline');

  

const rl = readline.createInterface({

input: fs.createReadStream('data.txt'),

crlfDelay: Infinity

});

  

rl.on('line', (line) => {

console.log(line);

});

**Use cases**

- Log files
    
- CSV files
    
- Large text files
    

---

### C. Read File Using Streams (Chunk by Chunk)

const stream = fs.createReadStream('data.txt', {

encoding: 'utf8',

highWaterMark: 16

});

  

stream.on('data', (chunk) => {

console.log(chunk);

});

---

## 3️ What is a Chunk?

### Definition

A **chunk** is a small piece of **raw data (bytes)** read from a file or stream at a time.

### Key Points

- Chunk size controlled by `highWaterMark`
    
- Chunk does **not care about**:
    
    - lines
        
    - words
        
    - characters
        
- Comes directly from **OS buffer → Node.js**
    

 Chunks may break words, lines, or characters.

---

## 4️ Why Node.js Uses Chunks

- Non-blocking I/O
    
- Low memory usage
    
- Fast processing of large files
    
- Enables real-time streaming
    

---

## 5️ What is a Line?

### Definition

A **line** is a logical unit of text ending with:

- `\n` (Linux/Mac)
    
- `\r\n` (Windows)
    

### Notes

- Lines are **not native** to Node.js
    
- Created using `readline`
    
- Built on top of streams
    

---

## 6️ What is a Word?

### Definition

A **word** is a group of characters separated by:

- space
    
- tab
    
- newline
    

const words = data.split(/\s+/);

### Notes

- Words are **developer-defined**
    
- Node.js has no built-in word reader
    

---

## 7️ What is a Character?

### Definition

A **character** is a single letter, digit, or symbol.

### Notes

- Node.js reads **bytes**, not characters
    
- UTF-8 characters may span multiple bytes
    

for (let ch of data) {

console.log(ch);

}

---

## 8️ Chunk vs Line vs Word vs Character

| Feature           | Chunk        | Line      | Word      | Character |
| ----------------- | ------------ | --------- | --------- | --------- |
| Controlled by     | OS / Node.js | Developer | Developer | Developer |
| Memory efficient  | yes          | yes       | no        | no        |
| Human readable    | no           | yes       | yes       | yes       |
| Can break meaning | yes          | no        | no        | no        |
| Streaming support | yes          | yes       | no        | no        |

---

## 9️ Important Concept: `highWaterMark`

- Defines **chunk size**
    
- Default values:
    
    - 64 KB (text streams)
        
    - 16 KB (binary streams)
        

 Smaller chunks → more events  Larger chunks → more memory

---

##  How New Lines Are Preserved

- `fs.readFile` → preserves new lines automatically
    
- `readline` → emits one line at a time
    
- Streams → do **not** preserve new lines unless processed
    

---

## 1️1️ Real-World Analogy

- **Chunk** → Parcel delivered by courier
    
- **Line** → Row on a page
    
- **Word** → Group of letters
    
- **Character** → Single letter
    

Courier delivers parcels; **you decide how to organize them**.

---

## 1️2️ Interview One-Liners

- **Chunk**: Raw bytes read by Node.js streams
    
- **Line**: Text separated by newline characters
    
- **Word**: Group of characters separated by spaces
    
- **Character**: Single textual unit
    
- **Best for large files**: Streams + readline
    

---

##  Final Note

> Node.js always reads data as **chunks first**. Lines, words, and characters are **logical structures built on top of chunks**.

---

###  Ideal For

- Backend interviews
    
- B.Tech / MCA exams
    
- Real-world Node.js development
    

---

 _You can export these notes to PDF or print them directly._

I’ve created **one complete, consolidated set of notes** in the canvas that includes **everything from earlier**:

- File system (`fs`) basics
    
- Reading file **at once**, **line by line**, **chunk by chunk**
    
- Detailed explanation of **chunk vs line vs word vs character**
    
- `highWaterMark`, streams, new lines
    
- Interview one-liners + real-world analogies

1 4  17 21 23 27 35 36 50 53 56 58 60 63  66 68 70  33 62 69 10  29 