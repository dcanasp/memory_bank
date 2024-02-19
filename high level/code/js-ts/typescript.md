TypeScript is a superset of JavaScript that adds optional static typing and powerful features to the language. It builds upon familiar JavaScript syntax, making it easy to learn for existing JavaScript developers.

Typescript is a [[transpiled languages|Transpiled language]] so it transpiles to javascript. Bellow i tell how to add typescript

TypeScript offers several advantages, including:

- **Improved code clarity and maintainability:** Static typing helps to catch errors early in development and makes code easier to understand and refactor.
- **Increased developer productivity:** Type checking and autocompletion features speed up development by catching errors and suggesting code completion.
- **Enhanced tooling:** TypeScript integrates seamlessly with popular development tools, providing features like code analysis and refactoring.
- **Better libraries and frameworks:** Many popular libraries and frameworks are written in TypeScript, offering better type safety and interoperability.

**Key Features:**

- **Static typing:** Assigns types to variables and functions, enforcing type safety and preventing runtime errors.
- **Classes and interfaces:** Enable object-oriented programming with strong type checking.
- **Generics:** Allow writing reusable code that works with different types.
- **Decorators:** Add metadata to code for various purposes, like dependency injection.
- **JSX:** Enables writing HTML-like syntax directly within JavaScript files.

**Benefits:**

- **Reduced runtime errors:** Static typing helps to catch errors early in development, improving code quality and stability.
- **Improved code understanding:** Type annotations make code more readable and easier to maintain, especially for large projects.
- **Enhanced development experience:** Features like type checking and autocompletion speed up development and reduce frustration.
- **Better interoperability:** TypeScript plays well with existing JavaScript code and libraries, easing integration into existing projects.

**Use Cases:**

- **Large-scale applications:** TypeScript's strong typing helps manage complexity and ensure code quality in large projects.
- **API development:** Static typing improves API clarity and interoperability, leading to better communication between developers.
- **Front-end development:** Frameworks like React and Angular leverage TypeScript for improved performance and developer experience.
- **Shared libraries:** TypeScript libraries benefit from type safety and enhanced maintainability, making them more reliable and reusable.

## how to use typescript

install using npm `npm install typescript --save-dev`, 

the docs say that install globally but this is a great mistake, **don't do**, always local

With that you have typescript and can call it with `tsc`, specifically `npx tsc`, But to work you must create a `tsconfig.json` file, but instead of doing it manually, run `npx tsc --init`

with that you have the `tsconfig.json`, it has these main parts:
- **Compiler options**
- **File inclusion and exclusion**
- **Compiler plugins**
- **Custom compiler options**
- **Linting options**

All are important but the one you will really use is **Compiler options**, the rest will be used only on extreme cases (configuring jest ...)

the basics are
`"target": "ESNext"` what should the code transpile to, what ES?
`"module": "commonjs"` how you define modules? in old or new ways?
`"rootDir": "./src"` where is the ts code?
`"outDir": "./build"` where goes the js code?
`"strict": true` should everting have types?
`"types": ["node"]` want some types to always be included without setting them?
