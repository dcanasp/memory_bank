Object oriented programing language, single core, weakly typed. Used primarily on the browser, but with the use of different runtimes like [[Node.js]] it can work on the server. 

The browser [[JavaScript]] is a programming language used to add interactivity and dynamic behavior to [[web pages]]. It is a lightweight, [[interpreted languages|interpreted language]] that runs directly within the [[web browser]], without the need for any additional software.

**Why is it important?**

Browser JavaScript is essential for creating modern web experiences. It change the way things worked ([[php]] forms and submit actions) It allows you to:

- Add interactivity to web pages, such as forms, animations, and dynamic content.
- Manipulate the [[DOM]] (Document Object Model) to create and update the content of a web page.
- Communicate with web servers using AJAX (Asynchronous JavaScript and XML).
- Build complex web applications that run entirely within the browser.

# Key concepts

- **The DOM:** The Document Object Model (DOM) represents the structure of a web page. It is a tree-like structure that contains nodes for elements, attributes, and text. JavaScript allows you to access and manipulate the DOM to change the content and appearance of a web page.
- **Events:** Events are actions that occur on a web page, such as clicking a button or moving the mouse. JavaScript can react to events and perform actions in response.
- **Functions:** Functions are blocks of code that can be reused. They allow you to organize your code and make it more efficient.
- **Objects:** Objects are collections of properties and methods. They are used to represent real-world entities, such as users, products, and orders.
- **The JavaScript API:** The JavaScript API is a set of objects and methods that provide access to the browser's features, such as the DOM, networking, and storage.

There are multiple **JavaScript Engines**, depending on the browser


- **V8:** developed by google, runs on all [[Chromium]]-based browsers like Chrome, Edge, brave. Most importantly, it's the Engine that runs [[Node.js]]
- **SpiderMonkey:**  Firefox's JavaScript engine, developed by Mozilla. It's the first-ever JavaScript engine, created alongside the language
- **JavaScriptCore (Nitro):** used by safari, known for its speed and performance, is the engine that runs [[Bun]]
- **Opera:** Presto (formerly, now Blink)
- **Internet Explorer:** Chakra

While these engines share a common foundation and implement the ECMAScript standard, they have their own quirks and optimization techniques. This can lead to subtle differences in how JavaScript code behaves across different browsers.

**Additional notes:**

- Browser JavaScript is a single-threaded language, which means that it can only execute one task at a time.
- Browser JavaScript is also a sandboxed environment, which means that it has limited access to the user's system resources.
- There are different versions of JavaScript, and the latest version is ECMAScript 2023.

# JS runtime 
how JS works
![[JavascriptRuntime.png]]
## JS engine
The one that actually runs the code, the single threaded one
### Heap
the same as the heap in any program
### Call stack
The same as any program Call Stack. But it's important to understand that the call stack is not the only one who manages functions, the next elements also manage non syncronous events

For example the Web API `navigation. geolocation.getCurrentPosition` function gets send to the Web Browser for it to handled with some **callback functions**
## Event Loop
The event loop job is to move functions from the Task Queue and microtask queue to the Call Stack when the Call stack is empty (all synchronous code finished).

It's important to note that it prioritizes the **microtask queue**
## Task Queue / Callback Queue
It's job is simple, it will store all of the callback functions that may be created By the stack or the Web APIs
## Microtask Queue
These Is where the **Promise** based functions reside after the promise is fulfilled. this includes:
- async function fun(){
	  await ...
  }
- .then(() => { })
- .catch(() => { })
- .finally(() => { })
- queueMicrotask( () => { })
- new MutationObserver(callback);
## Web APIs for [[Browser javascript]]
These are APIs that the [[Web Browser]] provides, examples are the fetch, document, Timeout, navigation. These APIs calls will be handled **OUTSIDE** of your JS engine, making them non-blocking and asynchronous. 

When the APIs result are finished (most of the times) a **callback function** will get requested and sended to the *Task Queue* / *Callback Queue*. If that function returns a promise instead of using a callback it will go to the *Microtask Queue* 

# Classes
JavaScript does **NOT** Use classes. JavaScript is **NOT** a class-based language like java or c#. it's a **Prototype-based** language. The **class** keyword actually creates a prototype.

The main difference between classes and prototypes is how strict do we follow rules. in Js, **Any object** can **inherit** properties and methods from another prototype object. any object can then modify those properties it inherited at **runtime**, and most importantly, Js supports multiple inheritances using object composition or *mixins*


# var vs let
| var                | let                        |
| ------------------ | -------------------------- |
| Hoisted            | No hoisting                |
| is scoped globally | is scoped to nearest block |

# hoisting
Hoisting on JavaScript is behaivour where a variable decalration is moved to the top of it's current scope. This is a unique behaivour to the *var* keyword

```js
x = 5;
var x;
console.log(x)//5
```
meanwhile both *const* and *let* **DON'T** hoist.
```js
x = 5;//ReferenceError
let x;
```
It is important that the hoisting only moves the declaration of the variable, not the asignation, for example.
```js
console.log(x);//undefined
var x = 5;
```
is the same as this code:

```js
var x;
console.log(x);//undefined
x = 5;
```
