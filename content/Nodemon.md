## Nodemon and Hot Reloading (Backend)

**Nodemon** is a utility tool used in **Node.js backend development** to enable **hot reloading**.

### What is Hot Reloading?

Hot reloading means the application **automatically restarts or refreshes** when source files change, so developers **don’t need to manually stop and run the server again** after every change.

---

## Frontend vs Backend Hot Reloading

### Frontend Frameworks

Many frontend frameworks already support hot reloading:

- **React**: Uses **Reconciliation**
    
    - Reconciliation is React’s process of updating only the changed parts of the DOM using the Virtual DOM.
        
    - React Fast Refresh enables hot reloading during development.
        
- **Angular**:
    
    - Supports **Hot Module Replacement (HMR)**.
        
- **Lazy Loading (Important clarification)**
    
    - Lazy loading is **NOT hot reloading**.
        
    - Lazy loading means loading modules/components **only when required** to improve performance.
        

---

## Why Nodemon is Needed in Backend

In backend development (Node.js):

- By default, the server **does not restart automatically** when files change.
    
- This creates a problem similar to early HTML/CSS learning, where we had to **refresh manually** to see changes.
    

### Nodemon solves this problem:

- Watches project files for changes
    
- Automatically **restarts the server**
    
- Applies the latest code changes instantly
    

This helps in:

- Faster development
    
- Better productivity
    
- Continuous execution without manual restarts
    

---

## How Nodemon Works

- Monitors `.js`, `.json`, or configured file extensions
    
- When a file is modified:
    
    - Server automatically restarts
        
    - Changes are reflected immediately
        

---

## Installation

### Local Installation (Recommended)

`npm install nodemon --save-dev`

Run using:

`npx nodemon app.js`

### Global Installation

`npm install -g nodemon`

Run using:

`nodemon app.js`

---

## Windows PowerShell Execution Policy Issue

On Windows, you may face permission issues.

### Steps to Fix:

1. Open **PowerShell as Administrator**
    
2. Check current policy:
    
    `get-executionpolicy`
    
3. If it shows `Restricted`, run:
    
    `set-executionpolicy unrestricted`
    
4. Confirm by typing `Y`
    

**Note:** You can later reset it to `Restricted` for security if needed.

---

## Summary

- Nodemon provides **hot reloading for backend Node.js applications**
    
- Eliminates the need to restart the server manually
    
- Frontend frameworks already support hot reload internally
    
- Lazy loading ≠ hot reloading
    
- Nodemon improves development speed and efficiency


## Hot Reloading (Development Feature)

### What it is

Hot Reloading automatically **updates the application when code changes**, without restarting everything manually.

### How it works

- A file watcher detects code changes
    
- Only the changed part is reloaded
    
- Application state is usually preserved
    

### Where it is used

- **Frontend**: React (Fast Refresh), Angular (HMR), Vue
    
- **Backend**: Node.js using **Nodemon**
    

### Purpose

👉 Improves **developer productivity**

### Example

`// Change code → Save file → App updates automatically`

---

## 2️  Reconciliation (React Internal Mechanism)

### What it is

Reconciliation is **React’s internal algorithm** used to **efficiently update the UI**.

### How it works

1. React creates a **Virtual DOM**
    
2. Compares old Virtual DOM with new one (**diffing**)
    
3. Updates only the changed nodes in the real DOM
    

### Where it is used

- **React only**
    

### Purpose

👉 Improves **performance**, not developer workflow

### Important

Reconciliation is **NOT hot reloading**  
 It runs **after state/props change**

### Example

`setCount(count + 1); // React updates only the changed part of the DOM`

---

## 3️ Lazy Loading (Performance Optimization)

### What it is

Lazy Loading loads **resources only when they are needed**, instead of loading everything at once.

### How it works

- Code is split into chunks
    
- Chunks are loaded on demand (route/component level)
    

### Where it is used

- React, Angular, Vue
    
- Images, modules, routes, components
    

### Purpose

Improves **application performance & load time**

### Example (React)

`const Dashboard = React.lazy(() => import('./Dashboard'));`

---

##  Key Differences (Quick Table)

|Feature|Hot Reloading|Reconciliation|Lazy Loading|
|---|---|---|---|
|Type|Dev Tool / Feature|Internal Algorithm|Performance Technique|
|Runs During|Development|Runtime|Runtime|
|Main Goal|Faster development|Efficient UI updates|Faster initial load|
|Affects|Code refresh|DOM updates|Resource loading|
|State Preserved|Usually Yes|Yes|Not applicable|
|Used In|Frontend & Backend|React only|Frontend apps|

---

##  One-Line Memory Trick (Exam Friendly)

- **Hot Reloading** → _Auto refresh during development_
    
- **Reconciliation** → _React updates only what changed_
    
- **Lazy Loading** → _Load only when required_

## Alternate

node --watch filename used under 18.11 first time within node 