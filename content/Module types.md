# Types of Modules in Node.js

## Classification of Modules

Node.js modules are broadly classified into:

1. **Local Modules**
    
2. **Core Modules**
    
    - Global Core Modules
        
    - Non-Global Core Modules
        
3. **Third-Party Modules**
    

---

## 1️Local Modules

- **Local modules** are modules **created by developers** for a specific project requirement.
    
- These modules are used to:
    
    - Organize application code
        
    - Improve reusability
        
- Local modules can be:
    
    - Required **with or without file extension**
        
    - Required using **relative path** if present in another directory
        

### Example:

`require('./moduleName'); require('./folder/moduleName');`

 Used earlier in the project  
Developer-defined  
Specific to an application

---

## 2️ Core Modules

- **Core modules** are modules that:
    
    - Come **built-in with Node.js**
        
    - Are available by default
        
- No need to download or install them separately.
    

### Popular Core Modules:

- `fs` → File System
    
- `os` → Operating System
    
- `path`
    
- `http`
    

---

### Global Core Modules

- Global core modules can be used **without importing or requiring them**.
    
- Example:
    
    - `console`
        

`console.log("Hello");`

✔ Works without `require()` or `import`

---

###  Non-Global Core Modules

- These modules **must be imported before use**.
    
- Examples:
    
    - `fs`
        
    - `http`
        
    - `path`
        

`const fs = require("fs");`

 Need explicit import  
 Not available globally

---

## 3️Third-Party Modules

- **Third-party modules** are modules:
    
    - Created by external developers
        
    - Downloaded using a **package manager** like `npm`
        
- These modules are stored in the:
    
    - `node_modules` folder
        

### Examples:

- `uuid`
    
- `nodemon`
    
- `express`
    
- `mongoose`
    

---

## Installation of Third-Party Modules

- Third-party modules can be installed:
    
    - **Locally** → Available only for that project
        
    - **Globally** → Available across the system
        

`npm install express        # Local npm install -g nodemon     # Global`

 Local installation is project-specific  
 Global installation is system-wide

---

## Key Exam Points

- Local modules are developer-created
    
- Core modules come with Node.js by default
    
- Global core modules do not need import
    
- Non-global core modules must be imported
    
- Third-party modules are installed using npm
    
- `node_modules` stores third-party packages