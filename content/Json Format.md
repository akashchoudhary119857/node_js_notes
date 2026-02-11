# JSON (JavaScript Object Notation)

**JSON** stands for **JavaScript Object Notation**.

It is a **standard text-based data interchange format** used to exchange data between **web clients (browsers)** and **web servers**.

JSON is:

- **Lightweight**
    
- **Easy to read and understand**
    
- **Self-describing**
    
- Used for **storing and transporting data**
    

Before JSON, **XML (Extensible Markup Language)** was commonly used, but XML is **heavier and more complex** compared to JSON.

JSON is often used when data is sent from a **server to a web page (client)**.

It can also be used to **store user input data**, such as form data, in JSON format.

---

##  Structure of JSON

JSON is a **collection of key–value pairs**.

- **Key** must always be a **string** (in double quotes).
    
- **Value** can be:
    
    - Number
        
    - String
        
    - Boolean
        
    - Array
        
    - Object
        
    - null
        

---

##  Advantages of JSON

- Language independent (supported by almost all programming languages)
    
- Platform independent (works on any OS)
    
- Lightweight compared to XML
    
- Easy to parse and generate
    
- Human readable format
    

---

##  JSON Methods in JavaScript

### `JSON.parse()`

Converts a **JSON string** into a **JavaScript object**.

`const obj = JSON.parse(jsonString);`

### `JSON.stringify()`

Converts a **JavaScript object** into a **JSON string**.

`const jsonString = JSON.stringify(obj);`

---

##  Example JSON

`{   "id": 101,  
`"name": "Akash",  
`"isActive": true,   
`"codingLanguages": ["C", "C++", "Java 24", "MERN", "MEAN"],  
`"techStack": {     "first": "PHP",     "second": ".NET"   }, 
`"phoneNumber": null
`}`

##  Key Points to Remember

- Keys must be in **double quotes**
    
- No trailing commas
    
- JSON is **data format**, not a programming language
    
- Used heavily in **APIs**, **web apps**, and **data exchange**