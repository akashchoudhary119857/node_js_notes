## What is the Events Module in Node.js?

Node.js follows an event-driven architecture. Instead of waiting for tasks to complete, Node emits events and executes functions (listeners) when those events occur.

This behavior is implemented using the built-in `events` module.

In simple terms: you listen for something to happen, and when it happens, your code runs.

---

## Importing the Events Module

`const EventEmitter = require('events');`

This gives access to the `EventEmitter` class.

---

## Creating an Event Emitter Object

`const EventEmitter = require('events'); const emitter = new EventEmitter();`

The `emitter` object can now emit events and listen to them.

---

## Listening to Events with `on()`

`emitter.on('greet', () => {     console.log('Hello'); });`

- `'greet'` is the event name
    
- The function is the listener
    

---

## Emitting Events with `emit()`

`emitter.emit('greet');`

This triggers the listener attached to `'greet'`.

---

## Passing Data with Events

``emitter.on('orderPlaced', (orderId, user) => {     console.log(`Order ${orderId} placed by ${user}`); });  emitter.emit('orderPlaced', 101, 'Akki');``

Events can carry data to listeners.

---

## Multiple Listeners for the Same Event

`emitter.on('login', () => console.log('Log login time')); emitter.on('login', () => console.log('Send welcome email'));  emitter.emit('login');`

All listeners attached to the same event will execute.

---

## Using `once()` for One-Time Listeners

`emitter.once('start', () => {     console.log('This runs only once'); });`

Even if the event is emitted multiple times, the listener runs only once.

---

## Removing a Listener with `off()` or `removeListener()`

`function handler() {     console.log('Handled'); }  emitter.on('test', handler); emitter.off('test', handler);`

---

## Viewing All Listeners for an Event

`console.log(emitter.listeners('login'));`

---

## Why the Events Module is Important in Node.js

Node.js is:

- Non-blocking
    
- Asynchronous
    
- Single-threaded
    

To manage this efficiently, Node relies on events, callbacks, and the event loop. Many core Node features are built using EventEmitter internally, such as:

- HTTP module
    
- File system
    
- Streams
    
- Sockets
    
- Process signals
    

---

## Real-World Use Cases

### Logging System

`emitter.on('userRegistered', (user) => {     logToFile(user); });`

### Sending Emails After Registration

`emitter.on('userRegistered', sendWelcomeEmail);`

### Decoupling Modules in Applications

Instead of directly calling functions in another module, emit an event.

### Order Processing in E-commerce

An `orderPlaced` event can trigger:

- Inventory update
    
- Invoice generation
    
- User notification
    

### Chat Applications and Real-Time Systems

Socket events are based on EventEmitter.

### Streams

Streams emit events such as:

- `data`
    
- `end`
    
- `error`
    

---

## Extending EventEmitter in Custom Classes

`const EventEmitter = require('events');  class MyLogger extends EventEmitter {     log(message) {         console.log(message);         this.emit('messageLogged', message);     } }  const logger = new MyLogger();  logger.on('messageLogged', (msg) => {     console.log('Saved to DB:', msg); });  logger.log('Server started');`

This pattern is used in large-scale applications.

---

## Handling Errors with Events

Node has a special `error` event.

`emitter.on('error', (err) => {     console.error('Error occurred:', err); });  emitter.emit('error', new Error('Something broke'));`

If the `error` event is not handled, Node.js will crash.

---

## How Events Work with the Event Loop

1. An event occurs.
    
2. It is placed in the event queue.
    
3. The event loop picks it up.
    
4. The corresponding listener runs.
    

---

## Common Interview Questions

- What is EventEmitter?
    
- Difference between `on()` and `once()`?
    
- Why is Node.js called event-driven?
    
- How do streams use events?
    
- What happens if the `error` event is not handled?
    

---

## Summary Table

|Method|Purpose|
|---|---|
|`on()`|Listen to an event|
|`emit()`|Trigger an event|
|`once()`|Listen only once|
|`off()`|Remove a listener|
|`listeners()`|Get all listeners|

---

## Key Takeaway

Events allow loose coupling, asynchronous behavior, and scalable design in Node.js. Many core features of Node rely on the Events module internally.

## What is Loose Coupling?

**Loose coupling** means:

> Two parts of a system know **as little as possible** about each other.

They can work together **without depending on each other’s internal code**.

---

## Simple Idea

Instead of:

> Module A directly calling Module B’s function

You do:

> Module A emits an event, and whoever is interested can listen.

Module A does **not** know:

- Who will respond
    
- How many will respond
    
- What they will do
    

That is loose coupling.

---

## Tight Coupling (Bad Design)

`// order.js const email = require('./email'); const invoice = require('./invoice');  function placeOrder(order) {     email.sendEmail(order);     invoice.generateInvoice(order); }`

Problems:

- If email module changes, order breaks
    
- If you add SMS later, you must edit this file
    
- Modules are dependent on each other
    

This is tight coupling.

---

## Loose Coupling with Events (Good Design)

`// order.js const EventEmitter = require('events'); const emitter = new EventEmitter();  function placeOrder(order) {     emitter.emit('orderPlaced', order); }  module.exports = emitter;`

`// email.js const emitter = require('./order');  emitter.on('orderPlaced', (order) => {     console.log('Send email'); });`

`// invoice.js const emitter = require('./order');  emitter.on('orderPlaced', (order) => {     console.log('Generate invoice'); });`

Now:

- Order module does not know email exists
    
- Order module does not know invoice exists
    
- You can add SMS without touching order.js
    

This is loose coupling.

---

## Key Characteristics of Loose Coupling

- Modules are independent
    
- Easy to add new features
    
- Easy to maintain
    
- Easy to test
    
- Fewer side effects when changing code
    

---

## Real-World Example

Think of a news channel.

The reporter broadcasts news.  
Anyone with a TV can watch.

The reporter does not know:

- Who is watching
    
- How many are watching
    

That is loose coupling.

---

## Why Loose Coupling is Important in Node.js

Node applications are event-driven. Events help:

- Separate responsibilities
    
- Build scalable systems
    
- Avoid complex dependencies
    
- Make code modular
    

---

## One-Line Definition for Interviews

Loose coupling is a design principle where components interact with minimal knowledge of each other, usually through events, messages, or interfaces, making the system flexible and maintainable.