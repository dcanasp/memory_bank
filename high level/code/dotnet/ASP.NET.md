#todo
part of the [[dotnet]] framework

main parts


all starts on the `program.cs` file. it will do most for you when you create using a template

`var builder = WebApplication.CreateBuilder(args);` is the creation of the server, on the builder you will register all of the services, controllers, and any other thing you define (custom error handling, swagger, dependency injection)


## dependency injection types
Singleton vs transient vs scoped 
```cs
builder.Services.AddSingleton(jwtSettings);
builder.Services.AddTransient<JwtService>();
builder.Services.AddScoped<IDbConnection>((sp) => new OracleConnection(connectionString));
```

## IServiceCollection
`builder.Services.AddErrorHandlers()`

## web api