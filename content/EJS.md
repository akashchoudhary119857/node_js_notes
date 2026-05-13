EJS (Embedded JavaScript) – Template Engine in Node.js

EJS is a popular template engine for Node.js that allows developers to generate HTML markup using plain JavaScript. It is particularly useful for creating dynamic web pages because it enables embedding JavaScript logic directly within HTML templates.

A template engine helps in creating HTML templates with minimal code. It also allows injecting data into an HTML template on the server side and producing the final HTML that is sent to the client browser.

EJS is widely used with the Express.js framework to build server-side rendered web applications.

---

Purpose of Using EJS

1. To generate dynamic HTML pages.
    
2. To embed JavaScript code inside HTML templates.
    
3. To separate application logic from presentation.
    
4. To reuse HTML components easily.
    
5. To reduce repetitive HTML code.
    

---

Key Features of EJS

• Simple and easy syntax  
• Allows embedding JavaScript inside HTML  
• Works smoothly with Express.js  
• Supports loops and conditional statements  
• Allows passing dynamic data from server to view  
• Helps maintain clean and organized code structure

---

Steps to Create and Setup an EJS Project

Step 1: Create a New Node.js Project

Create a new folder and initialize the Node.js project.

mkdir ejs-project  
cd ejs-project  
npm init -y

This command creates a package.json file for the project.

---

Step 2: Install Express and EJS

Install the required dependencies.

npm install express ejs

Express → Web framework for Node.js  
EJS → Template engine used to render HTML pages.

---

Step 3: Create Project Structure

Create the following folder structure:

ejs-project  
|  
|-- node_modules  
|-- views  
|    |-- index.ejs  
|    |-- about.ejs  
|  
|-- app.js  
|-- package.json

The **views folder** stores all EJS template files.

---

Step 4: Configure EJS as Template Engine

Create the main server file app.js.

const express = require('express');  
const app = express();  
  
app.set('view engine', 'ejs');  
  
app.listen(3000, () => {  
    console.log("Server running on port 3000");  
});

The following line sets EJS as the template engine:

app.set('view engine', 'ejs');

---

Step 5: Create EJS Template Pages

Inside the views folder create a file named:

index.ejs

Example template:

<!DOCTYPE html>  
<html>  
<head>  
<title>EJS Example</title>  
</head>  
  
<body>  
  
<h1>Welcome to EJS Template Engine</h1>  
<p>This page is rendered using EJS.</p>  
  
</body>  
</html>

---

Step 6: Render EJS Page Using render() Function

To display the EJS page, use the render() function.

Example:

app.get('/', (req, res) => {  
    res.render('index');  
});

The render() function loads the EJS template from the views folder and converts it into HTML before sending it to the browser.

---

Passing Data from Server to EJS Template

Data can be sent from the Express server to the EJS template.

Example:

app.get('/', (req, res) => {  
    res.render('index', {name: "Akki"});  
});

Inside index.ejs:

<h1>Hello <%= name %></h1>

Output:

Hello Akki

---

Important EJS Syntax

1. Output Escaped Value
    

<%= variable %>

Example

<h1>Welcome <%= username %></h1>

Used to display dynamic values safely.

---

2. Output Unescaped HTML
    

<%- variable %>

Example

Server Code

res.render("index", {content: "<b>Hello Students</b>"});

EJS Code

<%- content %>

This renders HTML tags directly in the browser.

---

3. Execute JavaScript Code
    

<% code %>

Example

<% if(user){ %>  
<h2>Welcome <%= user %></h2>  
<% } %>

Used for conditions and loops.

---

Loop Example in EJS

<ul>  
<% students.forEach(function(student){ %>  
<li><%= student %></li>  
<% }) %>  
</ul>

---

4. EJS Comment
    

<%# This is a comment %>

Comments written with this syntax are not displayed in the final HTML output.

Example

<%# Student Information Section %>

---

5. Print Literal `<%`
    

<%% 

Used when you want to display `<%` in the output rather than executing it.

---

Example Complete Application

app.js

const express = require('express');  
const app = express();  
  
app.set('view engine','ejs');  
  
app.get('/', (req,res)=>{  
    const students = ["Rahul","Aman","Priya"];  
    res.render('index',{students:students});  
});  
  
app.listen(3000);

index.ejs

<h1>Student List</h1>  
  
<ul>  
<% students.forEach(function(student){ %>  
<li><%= student %></li>  
<% }) %>  
</ul>

---

Advantages of EJS

• Easy to learn and use  
• Lightweight template engine  
• Works efficiently with Express.js  
• Supports dynamic content rendering  
• Allows separation of logic and presentation

---

Limitations of EJS

• Not suitable for very large front-end applications  
• Less powerful compared to modern frameworks like React or Angular  
• Mainly used for server-side rendering

## 1. What is EJS

EJS is a popular template engine for Node.js that allows you to generate HTML markup using plain JavaScript.

It helps create **dynamic web pages** by embedding JavaScript inside HTML.

---

## 2. Why Use EJS

- To create dynamic content
- To reuse HTML templates
- To inject data into HTML
- To reduce repetitive code

---

## 3. What is a Template Engine

A template engine:

- Creates HTML templates
- Injects data into templates
- Produces final HTML output

---

## 4. Steps to Use EJS

1. Create a new project
2. Install dependencies
3. Set EJS as template engine
4. Create a views folder
5. Create .ejs files
6. Use `res.render()` to display pages

---

## 5. Project Structure

expressejsproject/  
│  
├── node_modules/  
├── package.json  
├── package-lock.json  
├── index.js  
└── views/  
     └── home.ejs

---

## 6. Installation

npm init -y  
npm install express ejs

---

## 7. Setup Code (index.js)

const express = require('express');  
const app = express();  
  
// Set EJS as template engine  
app.set('view engine','ejs');  
  
app.get('/', (req, res) => {  
  
  let Student = {  
    name: 'Rohan',  
    age: 22,  
    marks: 72,  
    email: 'rohan@1.com',  
    hobbies: ['coding','cricket','photography','solo traveler']  
  };  
  
  res.render('home', { stu: Student });  
});  
  
app.listen(3000);

---

## 8. home.ejs Example

<h2>Name is <%= stu.name %></h2>  
  
<ul>  
  <% stu.hobbies.forEach((hob)=>{ %>  
    <li><%= hob %></li>  
  <% }) %>  
</ul>

---

## 9. EJS Tags Explanation

---

### 1. `<% %>`

- Used for JavaScript logic
- Does NOT display output

<% if(true){ %>

---

### 2. `<%= %>`

- Used to display data
- Outputs value to HTML

<%= stu.name %>

---

### 3. `<%- %>`

- Used to include HTML or partials
- Does NOT escape HTML

<%- include('common/header') %>

---

### 4. `<%# %>`

- Used for comments
- Not visible in output

<%# This is a comment %>

---

## 10. Include Example (Header)

<body>  
  <%- include('common/header') %>  
</body>

---

## 11. Loop Example

<ul>  
  <% stu.hobbies.forEach((hob)=>{ %>  
    <li><%= hob %></li>  
  <% }) %>  
</ul>

---

## 12. How render() Works

res.render('home', { stu: Student });

Explanation:

- Looks inside views folder
- Finds home.ejs
- Sends data (stu object)
- Renders final HTML

---

## 13. Key Points for Exams

- EJS is a template engine
- Used with Express
- Views folder stores .ejs files
- `res.render()` is used to display pages
- `<%= %>` is used to print values
- `<% %>` is used for logic

---

## 14. Common Mistakes

- Forgetting to set view engine
- Wrong path in include
- Using `<% %>` instead of `<%= %>` for output




