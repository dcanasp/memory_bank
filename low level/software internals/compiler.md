A **compiler** is a tool that transforms human-readable source code into [[binary]] instructions that a [[CPU]] can understand and execute.

It takes code written in a high-level [[compiled languages]] and turns it into low-level machine code or intermediate code (e.g., bytecode in Java/.NET).

# Compilation Process

In general, these are the typical steps in a compilation pipeline:

1. **Preprocessor**  
    Handles directives like `#include`, `#define`, `using`, `import`, and conditional compilation.  
2. **Compiler**  
    Converts preprocessed code into **assembly** or **intermediate representation** (IR).  
    Performs syntax analysis, semantic checks, optimizations.
3. **Assembler**  
    Converts assembly code to **object code** (machine code in binary format).
4. **Linker-Loader**  
    Combines object files and libraries into a final executable.  
    Resolves external references and prepares code for execution.
# Internals & Concepts

- **AST (Abstract Syntax Tree):** Intermediate structure representing code in a tree form — useful for optimizations and analysis.
- **Intermediate Representations (IR):** Like LLVM IR, used for platform-independent optimizations.
- **Symbol Table:** Keeps track of identifiers and their properties (scope, type, etc.).
- **Optimization:** Can be done at various stages (e.g., loop unrolling, dead code elimination).
# v-tables in Object-Oriented Programming

A **v-table** (virtual method table) is a mechanism used in object-oriented languages (like C++ or C#) to support **dynamic dispatch** — the ability to call the correct method implementation at runtime based on the object's actual type.

- Each class with virtual functions has a **v-table**, which is essentially an array of function pointers.
- Each object has a hidden pointer to the v-table of its class.
- When a virtual method is called on the object, the function pointer from the v-table is used.

This enables polymorphism — allowing you to write code that works with base types but behaves correctly for derived types.