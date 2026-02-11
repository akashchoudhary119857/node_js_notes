   n## Uniform Resource Locator (URL)

A **Uniform Resource Locator (URL)** is the address of a unique resource on the Internet. It is one of the key mechanisms used by browsers to retrieve published resources such as **HTML pages, CSS files, documents, images**, and more.

In theory, each valid URL points to a **unique resource** available on the Internet.

**Examples:**

- [https://www.google.com](https://www.google.com/)
    
- [https://www.facebook.com](https://www.facebook.com/)
    

Each URL accesses only its **own resources**.

---

## Structure of a URL

A URL is made up of different **segments (portions)**. Consider the following example:

```
https://www.example.com/
```

### 1. Protocol (Scheme)

```
https://
```

- Specifies how data is transferred.
    
- `https` stands for **HyperText Transfer Protocol Secure**.
    
- The `s` indicates that the data is encrypted and transferred securely.
    
- If `http` is used instead of `https`, the connection is **less secure**.
    

### 2. Domain / Hostname

```
www.example.com
```

- A **user-friendly name** that maps to an IP address.
    
- Identifies the server where the resource is hosted.
    

### 3. Root Path (Absolute Path)

```
/
```

- Represents the **root or home directory** of the website.
    
- Accessing this usually loads the **index page or home page**.
    

---

## Path in a URL

Paths specify the **location of a resource** on the server.

**Examples:**

```
https://www.example.com/home
https://www.example.com/about
https://www.example.com/contact
```

- `home`, `about`, `contact`, `products`, `categories` are known as **paths**.
    

### Nested Paths

Paths can also be nested:

```
https://www.example.com/category/shirts
```

- `category` is the parent path
    
- `shirts` is a child (nested) path
    

---

## Query String

Sometimes URLs contain additional data:

```
https://www.example.com/category/search?name=akash&age=29
```

### Components:

- `?` → **Query string separator**
    
- Data after `?` → **Query string**
    
- Query strings are written as **key–value pairs**
    
- Multiple values are separated using `&`
    

**Example:**

- `name=akash`
    
- `age=29`
    

---

## Fragment Identifier

```
#section4
```

- The `#` symbol represents a **fragment**.
    
- Fragments are used to **automatically scroll** the browser to a specific location on a web page.
    
- If a URL refers to a document, the fragment refers to a **specific subsection** of that document.
    

---

## URL Module in Node.js

Node.js provides a built-in **URL module** to work with web addresses.

### Features of the URL Module

- Splits a URL into **readable and structured parts**
    
- Provides utilities for **parsing** and **resolving** URLs
    

### What is Parsing?

**Parsing** is the process of transforming:

- **Unstructured data** → into **structured data**
    
- Usually represented as an object or tree structure
    

A URL is a structured string containing multiple segments, which can be easily accessed after parsing.

---

## Practical Example (Node.js)

```js
const url = require('url');

let address = 'https://www.example.com/category/search?name=akash&age=21#section4';

const myURL = url.parse(address, true);

console.log(myURL);
```

### Explanation:

- `url.parse()` converts the static URL string into a **structured object**.
    
- The second parameter `true` parses the query string into an object.
    
- `myURL` becomes an object of the URL class containing all URL components.
    

### Accessing Specific Properties

```js
console.log(myURL.protocol); // https:
console.log(myURL.hostname); // www.example.com
console.log(myURL.pathname); // /category/search
console.log(myURL.search);   // ?name=akash&age=21
console.log(myURL.query);    // { name: 'akash', age: '21' }
console.log(myURL.hash);     // #section4
```

Using these properties, we can perform **validations, routing, filtering, and logic implementation** based on URL data.

---

## Note

- In real-world applications, URLs are often parsed dynamically using **HTTP requests** instead of static strings.
    
- URL parsing is commonly used in **backend development** for routing, API handling, and request validation.