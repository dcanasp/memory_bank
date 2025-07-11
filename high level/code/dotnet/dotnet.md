NET is a free, cross-platform, open-source developer platform for building Web [[API]]s, [[microservices]], serverless apps. Cloud native code, mobile applications, desktop applications, games, Machine learning programs and IoT projects.

It uses the [[csharp|C#]], f# and VB languages and is maintained by Microsoft. It is a **garbage-collected**, **object-oriented** platform where methods and classes are treated as **first-class citizens**.

## Design Philosophies
- Do less, accomplish more.
- Trust Microsoft’s ecosystem.
- Rich out-of-the-box functionality.
- You rarely need to implement plumbing code yourself.
- Focus on **business logic**.
- Strongly **object-oriented**.
- **Dependency Injection** is a fundamental architectural principle.

# Project Structure
In .NET, a solution typically consists of multiple projects, each with its own configuration, dependencies, and files. 

## `.sln` — Solution File

The `.sln` (solution) file is a **Visual Studio solution file**. It is a plain text file that organizes and references one or more `.csproj` (C# project) files.

- Contains metadata about the IDE layout (e.g., open documents, build configurations).
- Enables management of multi-project solutions.
- Can include projects in **different languages** (C#, F#, VB.NET).

## `.csproj` — C# Project File

The `.csproj` file is an **XML configuration file** that defines:

- Target framework
- Project type
- Dependencies (NuGet packages, project references)
- Build options
- File inclusions/exclusions

### Example

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
  <PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.EntityFrameworkCore" Version="8.0.0" />
  </ItemGroup>
</Project>
```

### Key Element: `Sdk` attribute

The line:
`<Project Sdk="Microsoft.NET.Sdk.Web">`

Defines the **type of SDK** the project uses. Common SDKs include:
- `Microsoft.NET.Sdk` — Console apps, class libraries, etc.
- `Microsoft.NET.Sdk.Web` — Web apps using ASP.NET Core
- `Microsoft.NET.Sdk.Razor` — Razor Class Libraries (UI components)
- `Microsoft.NET.Sdk.Worker` — Background services (workers)
- `Microsoft.NET.Sdk.BlazorWebAssembly` — Client-side Blazor apps

Changing the SDK type changes the available project templates, defaults, and tools.

## NuGet — Package Manager

[NuGet](https://www.nuget.org/) is the **package manager** for .NET.

- Stores and distributes **third-party** and **internal** libraries.
- Packages are added via CLI (`dotnet add package`) or directly in `.csproj`.

Example:

`<PackageReference Include="Newtonsoft.Json" Version="13.0.1" />`

NuGet stores downloaded packages in a global cache (usually under `~/.nuget`), and each project has a `obj` and `bin` folder that gets updated on restore/build.


## `Properties` Folder

This folder usually contains the following:
- `launchSettings.json` — Configures how the app runs during development
    - Profiles for IIS Express, Kestrel, Docker, etc.
    - Environment variables, application URLs

Example:

```json
{
  "profiles": {
    "MyApp": {
      "commandName": "Project",
      "launchBrowser": true,
      "applicationUrl": "https://localhost:5001",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

This file is mostly relevant for **development tooling** and is not used in production builds.

# F# in .NET

F# is a **functional-first** programming language in the .NET ecosystem.

- Fully interoperable with C# and VB.NET.
- Often used in domains requiring immutability, mathematical computation, or data analysis.
- Project files use `.fsproj`.
- Syntax is concise, and the language encourages **immutability**, **pattern matching**, and **type inference**.

Example:

```fsharp
let square x = x * x
```

.NET allows mixing F# with C# projects within the same solution.

# .NET vs .NET Framework

| Aspect              | .NET (Core/5+/Modern)            | .NET Framework (Legacy)    |
| ------------------- | -------------------------------- | -------------------------- |
| Cross-platform      | ✅ Yes (Windows, Linux, macOS)    | ❌ Windows-only             |
| Open-source         | ✅ Yes                            | ❌ No (partially open)      |
| Current status      | ✅ Actively developed             | ❌ Legacy, maintenance mode |
| CLI tooling         | ✅ `dotnet` CLI                   | ❌ Visual Studio only       |
| Performance         | ✅ Better performance             | ❌ Slower                   |
| App types supported | Web, APIs, Console, Mobile, etc. | Web, Windows Forms, WPF    |
| Versioning          | Side-by-side installs            | Machine-wide install only  |
- **.NET Framework** is the old Windows-only runtime (up to version 4.8).
- **.NET Core / .NET 5+** (rebranded as just “.NET”) is the modern, cross-platform, open-source version.
- For **new development**, always use the modern .NET unless you are tied to legacy Windows APIs.

## Main Components of .NET
- **[[ASP.NET Core]]** — Framework for building web APIs.
- **[[Entity Framework Core]]** — ORM for database interaction.
- **Blazor** — Build interactive web UIs using C# (some [[JavaScript]] interop may be used).

---
# LINQ (Language Integrated Query)

Allows you to query, filter, group, and order data from various sources (in-memory, databases, XML, etc.).

### Example:

```cs
int[] scores = { 97, 92, 81, 60 };

IEnumerable<int> scoreQuery =
    from score in scores
    where score > 80
    select score;
```
With Entity Framework, LINQ can be translated into SQL queries.

_Tool recommendation: [LINQPad](https://www.linqpad.net/) for exploring and testing queries interactively._

---

# Compilation

## Just-In-Time (JIT)
- Compiles Intermediate Language (IL) to native code **at runtime**.
- Compilation happens **per method** on first execution.
- Enables runtime optimizations like tiered compilation and method inlining.
    
### Trade-offs
- **Startup penalty** (cold start).
- **Higher memory usage** (due to cached IL and metadata).
- **.NET runtime required** on the host machine, although it can be bundled in a binary with the `SelfContained` and `PublishSingleFile` flags on the `.csproj`
### JIT compilation flow
C# source code → IL (via Roslyn) → Native code (via RyuJIT on method call at runtime)
![[JitCompilation.png]]
### Tiered Compilation
1. **Tier 0**: Fast, unoptimized compilation. it's the first one done
2. **Tier 1**: Optimized version after **PGO** (Profile-Guided Optimization) identifies hot paths, frequently used branches, and common data types. 

This explains why performance improves after a few minutes of execution.

## Ahead-of-Time (AOT)
- Compiles IL to native code **before runtime**.
- Produces a platform-specific binary.
- No need for .NET runtime on the target system.
### Limitations
- No dynamic assembly loading.
- No runtime code generation.
- Reflection and `System.Reflection.Emit` APIs are heavily restricted.
- When working with web APIs. Minimal API is the only option.

### Compilation Steps
1. C# → IL (via `Roslyn`)
2. `crossgen2` analyzes and creates a dependency graph with the help of some heuristics.
3. IL → Native binary (via `RyuJIT`)
    

The crossgen2 step is incredibly important, as there is no way to optimize the code after this, if the dependency graphs are created incorrectly it will produce slow code.