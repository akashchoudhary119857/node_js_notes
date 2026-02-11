#  Installation of Node.js (Step-by-Step Guide)

---

## 1. What is Node.js?
Node.js is a **JavaScript runtime environment** that allows JavaScript to run **outside the browser** using the **V8 JavaScript engine**.

---

## 2. System Requirements
Before installing Node.js, ensure:
- Internet connection
- Administrator access
- Supported OS:
  - Windows
  - macOS
  - Linux

---

## 3. Step-by-Step Installation on Windows

### Step 1: Download Node.js
1. Open a web browser
2. Visit: https://nodejs.org
3. Download **LTS (Long Term Support)** version

---

### Step 2: Run the Installer
1. Open the downloaded `.msi` file
2. Click **Next**
3. Accept the License Agreement
4. Choose installation path
5. Click **Next**

---

### Step 3: Select Components
Ensure the following options are checked:
- Node.js runtime
- npm package manager
- Add to PATH
- Online documentation shortcuts

Click **Next**

---

### Step 4: Install Node.js
1. Click **Install**
2. Allow administrator permission
3. Wait for installation to complete
4. Click **Finish**

---

### Step 5: Verify Installation
1. Open **Command Prompt**
2. Run:
```bash
node -v
```

3. Check npm version:
    
`npm -v`

---

## 4. Step-by-Step Installation on macOS

### Step 1: Download Node.js

1. Visit: [https://nodejs.org](https://nodejs.org)
    
2. Download **LTS version for macOS**
    

---

### Step 2: Install Node.js

1. Open the downloaded `.pkg` file
    
2. Follow the installation steps
    
3. Accept license and default settings
    

---

### Step 3: Verify Installation

Open **Terminal** and run:

`node -v npm -v`

---

## 5. Step-by-Step Installation on Linux (Ubuntu)

### Step 1: Update Package List

`sudo apt update`

---

### Step 2: Install Node.js

`sudo apt install nodejs`

---

### Step 3: Install npm

`sudo apt install npm`

---

### Step 4: Verify Installation

`node -v npm -v`

---

## 6. Optional: Install Node.js Using Node Version Manager (NVM)

### Step 1: Install NVM

`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash`

---

### Step 2: Install Node.js Using NVM

`nvm install --lts`

---

### Step 3: Verify

`node -v npm -v`

---

## 7. First Node.js Program (Test)

Create a file named `app.js`:

`console.log("Hello, Node.js!");`

Run the program:

`node app.js`

---

## 8. Common Installation Issues

- Node not recognized: Restart terminal or check PATH
    
- Permission issues (Linux/macOS): Use `sudo`
    
- Old version installed: Use NVM to manage versions
    

---

## 9. Summary

- Node.js can be installed on Windows, macOS, and Linux
    
- LTS version is recommended for stability
    
- npm is installed automatically with Node.js
    

---

## 10. Point to be remember

> **Node.js installation involves downloading the LTS version, running the installer, and verifying installation using `node -v` and `npm -v`.**

