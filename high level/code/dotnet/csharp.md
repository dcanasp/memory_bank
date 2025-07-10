C# is a **strongly typed**, **object-oriented** programming language developed by Microsoft. It is part of the .NET ecosystem and is widely used for building desktop, web, and cloud-based applications.

## Data Types

C# categorizes types into **value types** and **reference types**.

### Value Types

Stored directly on the **stack**, value types hold actual data. They are copied by value.
- `int` — 32-bit integer
- `float` — 32-bit floating point
- `bool` — Boolean (true/false)
- `char` — A single Unicode character
- `struct` — Custom value types

### Reference Types
Stored on the **heap**, reference types store references (pointers) to their data. They are copied by reference.
- `string` — A sequence of characters (immutable)
- `object` — Base type of all other types
- `dynamic` — Type resolved at runtime
### Note on `string` vs `String`
- `string` is an **alias** for `System.String`. They are functionally the same.
- `String` refers to the .NET class and exposes a rich API:
    - Iteration
    - String manipulation
    - LINQ extensions

Use `string` for declarations and `String` for static methods (e.g., `String.Format()`).

## Namespaces
Namespaces organize code and avoid naming conflicts.
Common examples:
- `System` — Base types like `Console`, `String`, `Math`
- `System.Collections.Generic` — Generic collections like `List<T>`, `Dictionary<TKey, TValue>`

```cs
using System;
using System.Collections.Generic;
```
# Access Modifiers
Control the **visibility** and **accessibility** of types and members.

>[!info]
> If no modifier is applied, the **default** is:
> - `private` for class members
> - `internal` for top-level classes

### `public`
Accessible from **anywhere** in the solution or other assemblies (if referenced).

### `private`
Accessible **only within the same class**.
### `protected`
Accessible from the **same class and its derived types**.
### `internal`
Accessible from **within the same assembly** (project or DLL).
### `protected internal`
Accessible from **derived classes** or **within the same assembly**.
# OOP
## Virtual Methods
- Only methods can be `virtual`, not classes.
- Virtual methods have a default implementation.
- Can be **overridden** in derived classes.
- You cannot override non-virtual methods.

## Abstract Methods
- Do **not** have an implementation.
- Must be overridden by any non-abstract derived class (eventually, an abstract class can override an abstract method, but as they don't have implementation, it won't do anything).
- Can **only** exist inside abstract classes.
- Abstract classes cannot be instantiated.
- Abstract classes can contain:
    - Abstract methods.
    - Concrete methods.
    - Properties (usable by derived classes).

In other words, if an abstract class does not have any abstract methods it will behave as a regular class

## Interfaces
Define a **contract** for a group of related functions — no implementation allowed.

- Essential for mocking and testability.
- A class or struct can implement multiple interfaces.

## Delegates
C# treats methods as first-class citizens. Delegates are type-safe references to methods.
```cs
public class Program
{
    public delegate string Reverse(string s);

    static string ReverseString(string s)
    {
        return new string(s.Reverse().ToArray());
    }

    static void Main(string[] args)
    {
        Reverse rev = ReverseString;
        Console.WriteLine(rev("a string"));
    }
}
```
### Using `Func<>`
```cs
Func<string, string> rev = ReverseString;
Console.WriteLine(rev("a string"));
```

### Anonymous Delegate
```cs
List<int> result = list.FindAll(
    delegate (int number)
    {
        return number % 2 == 0;
    }
);
```

### Lambda Expression (Preferred)
```cs
List<int> result = list.FindAll(i => i % 2 == 0);
```

Lambdas are simply shorthand for anonymous delegates.




# Events

Events represent **notifiable changes** or **user interactions**.
- Events are built on **delegates**, which define the **method signature** that responds to the event.
- Used in UI interactions, logging, lifecycle hooks, etc.

```cs
public event EventHandler SomethingHappened;
```


# Modifiers
### `static`
Indicates that a method or member belongs to the **type itself**, not an instance.
- Static members persist for the lifetime of the application.
- Cannot be garbage collected (unless the entire AppDomain is unloaded).
- Cannot use instance variables/methods.
    
`public static int Counter = 0;`
- This means that you don't have to instance the a static class to use it's members

---

# Error Handling

## `throw` vs `throw ex`

### `throw`
Re-throws the **original exception** and **preserves the original stack trace**.
```cs
catch (Exception ex)
{
    throw; // best practice
}
```

### `throw ex`

Throws a **new instance** of the same exception and **resets the stack trace** (bad for debugging).

```cs
catch (Exception ex)
{
    throw ex; // use with caution
}
```
