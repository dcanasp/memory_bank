Part of the [[dotnet]] framework, **ASP.NET Core** is a **cross-platform, high-performance web framework** for building APIs, web apps, and real-time systems.

---

# Entry Point

All ASP.NET Core apps start in `Program.cs`, which uses a modern, minimal-style setup. Most of the bootstrapping is abstracted for you when using templates.

## Example

```cs
var builder = WebApplication.CreateBuilder(args);
```

- **Creates the web server**
- Configures services via `builder.Services`
- Applies middleware and routing in the next steps

```cs
var app = builder.Build();

app.MapControllers();
app.Run();
```

>[!info]
> ASP.NET Core uses **convention over configuration**: default behaviors are assumed unless explicitly overridden.


# Dependency Injection in ASP.NET

ASP.NET Core has **built-in dependency injection**. All services are registered through `builder.Services`, which is an `IServiceCollection`.

## Lifetimes

| Type          | Description                                                                |
| ------------- | -------------------------------------------------------------------------- |
| **Singleton** | A single instance is created and reused throughout the app lifetime.       |
| **Transient** | A new instance is provided every time it's requested.                      |
| **Scoped**    | A new instance is created **per HTTP request** (shared within that scope). |

### Example
```cs
builder.Services.AddSingleton<JwtSettings>(jwtSettings);           // One instance forever
builder.Services.AddTransient<JwtService>();                        // New each time
builder.Services.AddScoped<IDbConnection>((sp) =>
    new OracleConnection(connectionString));                        // New per request
```
> Use `Scoped` for database connections or unit-of-work patterns.


## `IServiceCollection` Extensions

This is where you register and configure services used by the app.
```cs
builder.Services.AddErrorHandlers();
builder.Services.AddSwaggerGen();
builder.Services.AddControllers();
```

You can define **extension methods** for organizing service registration.

Example:

```cs
public static class ServiceCollectionExtensions
{
    public static IServiceCollection AddErrorHandlers(this IServiceCollection services)
    {
        services.AddSingleton<IErrorHandler, DefaultErrorHandler>();
        return services;
    }
}
```

Then call it in `Program.cs`:

```cs
builder.Services.AddErrorHandlers();
```


# Web API: Controller-Based vs Minimal API

ASP.NET Core supports two approaches for building HTTP APIs.

## Controller-Based API

Follows the **MVC (Model-View-Controller)** or **API Controller** pattern.

- Organizes logic into controllers and actions
- Uses `[ApiController]`, routing attributes, and dependency injection

```cs
[ApiController]
[Route("api/[controller]")]
public class AuthController : ControllerBase
{
    [HttpPost("login")]
    public IActionResult Login(LoginRequest req) { ... }
}
```

>[!info]
>Here `[controller]` auto-resolves to class name (minus "Controller")

Ideal for:
- Complex APIs
- Versioning
- Filters and model binding

## Minimal API

Introduced in .NET 6+ for small, fast, and simple APIs. Uses **function-based routing**.

```cs
var app = builder.Build();

app.MapPost("/login", (LoginRequest req, JwtService jwt) => {
    var token = jwt.GenerateToken(req.Username);
    return Results.Ok(token);
});
```

Ideal for:
- Lightweight microservices
- Internal tools or quick prototypes
- No need for full controller setup

# Middlewares
Middlewares are added in `Program.cs` using the `app.UseXyz()` pattern.

Each one:
- Receives the `HttpContext`
- Can pass control to the next middleware
- Can terminate the pipeline

## Example Pipeline

```cs
var app = builder.Build();

app.UseHttpsRedirection();         // Enforce HTTPS
app.UseRouting();                  // Enables routing
app.UseAuthentication();           // Check credentials (who are you?)
app.UseAuthorization();            // Check permissions (can you?)
app.UseEndpoints(endpoints =>
{
    endpoints.MapControllers();
});

app.Run();
```

## Custom Middleware 
```cs
public class LoggingMiddleware
{
    private readonly RequestDelegate _next;

    public LoggingMiddleware(RequestDelegate next) => _next = next;

    public async Task InvokeAsync(HttpContext context)
    {
        Console.WriteLine($"Request: {context.Request.Method} {context.Request.Path}");
        await _next(context); // pass to the next middleware
    }
}
```

And remember to register it:
```cs
app.UseMiddleware<LoggingMiddleware>();
```
# Auth

| Term               | Description                                                      |
| ------------------ | ---------------------------------------------------------------- |
| **Authentication** | Verifies **who** the user is (identity)                          |
| **Authorization**  | Determines **what** the user can do (permissions/roles/policies) |

These two features are handled via **middleware**:


## `app.UseAuthentication()`

- Validates credentials (e.g., JWT, cookies).
- Populates `HttpContext.User`.
- Required **before** `UseAuthorization()`.

### Example

```cs
builder.Services.AddAuthentication("Bearer")
    .AddJwtBearer("Bearer", options => {
        options.TokenValidationParameters = new TokenValidationParameters {
            ValidateIssuer = true,
            ValidateAudience = true,
            ValidateLifetime = true,
            ValidIssuer = "yourissuer",
            ValidAudience = "youraudience",
            IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes("yourkey"))
        };
    });

app.UseAuthentication();
```

## `app.UseAuthorization()`

- Uses `HttpContext.User` (populated by authentication)
- Enforces access based on policies, roles, or claims

### Protecting Controllers

```cs
[Authorize] // restricts to authenticated users
public class UserController : ControllerBase
{
    [Authorize(Roles = "Admin")]
    [HttpGet("admin")]
    public IActionResult GetAdminOnlyData() => Ok("Secret");
}
```

### Minimal API Protection
```cs
app.MapGet("/secure-data", [Authorize] () =>
{
    return Results.Ok("You are authorized!");
});
```
