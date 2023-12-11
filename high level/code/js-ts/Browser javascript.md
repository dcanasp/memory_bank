browser JavaScript is a programming language used to add interactivity and dynamic behavior to [[web pages]]. It is a lightweight, [[interpreted languages||interpreted language]] that runs directly within the [[web browser]], without the need for any additional software.

**Why is it important?**

Browser JavaScript is essential for creating modern web experiences. It change the way things worked ([[php]] forms and submit actions) It allows you to:

- Add interactivity to web pages, such as forms, animations, and dynamic content.
- Manipulate the [[DOM]] (Document Object Model) to create and update the content of a web page.
- Communicate with web servers using AJAX (Asynchronous JavaScript and XML).
- Build complex web applications that run entirely within the browser.

**Key concepts:**

- **The DOM:** The Document Object Model (DOM) represents the structure of a web page. It is a tree-like structure that contains nodes for elements, attributes, and text. JavaScript allows you to access and manipulate the DOM to change the content and appearance of a web page.
- **Events:** Events are actions that occur on a web page, such as clicking a button or moving the mouse. JavaScript can react to events and perform actions in response.
- **Functions:** Functions are blocks of code that can be reused. They allow you to organize your code and make it more efficient.
- **Objects:** Objects are collections of properties and methods. They are used to represent real-world entities, such as users, products, and orders.
- **The JavaScript API:** The JavaScript API is a set of objects and methods that provide access to the browser's features, such as the DOM, networking, and storage.

There are multiple **Different JavaScript Engines**, depending on the browser


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