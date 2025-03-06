interpreted languages like Python, Ruby, and [[JavaScript]], an interpreter executes the program line-by-line, translating each line into a series of machine-code instructions that are executed immediately.

##### Advantages

- Easier to debug, as you can stop at any point and inspect the program state.
- Generally more portable, as the interpreter handles the specifics of the target architecture.

##### Disadvantages

- Slower execution speed, as interpretation happens at runtime.
---
### Basic Workflow

1. **Source Code**: You start with the source code written in a high-level language like Python or JavaScript.
    
2. **Reading the Source Code**: The interpreter reads the source code line-by-line or statement-by-statement.
    
3. **Lexical Analysis**: Each line or statement is then broken down into tokens, which are the smallest units in a program, such as variables, operators, and keywords.
    
4. **Parsing**: The tokens are analyzed in the context of the language grammar to ensure they form a syntactically correct expression or statement. This often produces an intermediate representation like a parse tree or abstract syntax tree (AST).
    
5. **Semantic Analysis**: The interpreter checks if the parsed statement adheres to the rules and constraints of the language, such as type checking or scope resolution.
    
6. **Execution**: Finally, the interpreter executes the line of code, which often involves translating it into a series of lower-level machine code or bytecode instructions. These instructions are then executed immediately.
    
7. **State Management**: The interpreter manages the program state in memory, keeping track of variables, data structures, and the call stack.
    
8. **Loop**: The interpreter then moves to the next line of source code and repeats the process.
    

### Features and Characteristics

- **Dynamic Typing**: Interpreted languages often support dynamic typing, which means that variable types are determined at runtime. This offers flexibility but can lead to runtime errors.
    
- **Reflection**: Many interpreted languages offer rich reflection capabilities, allowing programs to modify themselves or generate code dynamically.
    
- **Portability**: Interpreted languages are usually more portable than compiled languages because they don't generate machine-specific code. However, you still need the interpreter to be available on the target system.
    
- **Debugging and Development**: Interpreted languages generally offer excellent debugging capabilities. You can pause execution, inspect the state, modify variables, and even change the code— all while the program is running.
    
- **Performance**: The primary drawback is usually slower performance compared to natively compiled languages. However, many modern interpreters employ techniques like Just-In-Time (JIT) compilation to improve performance.
    

### Examples

- **Python**: Python's interpreter, often called CPython, is written in C and interprets Python code at runtime. It has a very rich standard library and supports dynamic typing and reflection.
    
- **JavaScript**: JavaScript was initially only interpreted, primarily within web browsers. However, with the advent of [[Node.js]] and Just-In-Time (JIT) compilers like V8, it can also be considered a compiled language for certain use-cases.
    
- **Ruby**: The Matz's Ruby Interpreter (MRI) is the reference interpreter for Ruby. Like Python, it offers dynamic typing and an extensive standard library.
    
- **Shell Scripting**: Bash, sh, and other shell languages are also interpreted. They are designed for quick scripting tasks and automate system-level tasks.