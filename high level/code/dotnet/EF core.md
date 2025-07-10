The **Object-Relational Mapper (ORM)** of the [[dotnet]] environment. EF Core lets you **interact with databases using C# objects**, eliminating most raw SQL.


#  Getting Started

First, add the appropriate provider package for your database engine:
```sh
dotnet add package Microsoft.EntityFrameworkCore.Sqlite
```

> Other common providers:
> - `Microsoft.EntityFrameworkCore.SqlServer`
> - `Npgsql.EntityFrameworkCore.PostgreSQL`
> - `Pomelo.EntityFrameworkCore.MySql`

You may also want the **tools** package for CLI commands:

```sh
dotnet tool install --global dotnet-ef
```


#  Defining the Model

## Example Entity

```cs
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```

## DbContext
`DbContext` is the **core class** in Entity Framework Core that **manages database operations**.

It acts as a **bridge between your C# code and the database**, providing methods to:
- Query and save data (`SaveChanges()`)
- Manage entity tracking and state
- Configure models and relationships

A typical `DbContext` includes:
- `DbSet<T>` properties — which represent tables
- A constructor with `DbContextOptions<T>`
- Optionally: override `OnModelCreating` to configure entities
```cs
public class AppDbContext : DbContext
{
    public DbSet<Product> Products { get; set; }

    public AppDbContext(DbContextOptions<AppDbContext> options)
        : base(options)
    { }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        // Fluent API goes here
    }
}
```
### Registering DbContext

In `Program.cs`:

```cs
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlite("Data Source=app.db"));
```
## Fluent API
Fluent API is a **code-based configuration style** for defining how your entities map to the database schema. It uses method chaining and is called from `OnModelCreating`.

It’s an **alternative to data annotations**, and **more powerful** for configuring:
- Relationships
- Table names and column types
- Composite keys
- Indexes
- Default values, constraints, etc.

### Example: Fluent API for a One-to-Many Relationship
```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .HasMany(b => b.Posts)
        .WithOne(p => p.Blog)
        .HasForeignKey(p => p.BlogId);
}
```

### Fluent API vs Data Annotations

| Feature          | Data Annotations | Fluent API    |
| ---------------- | ---------------- | ------------- |
| Readability      | Simple           | More verbose  |
| Flexibility      | Limited          | Full control  |
| Complex mappings | ❌ Hard           | ✅ Recommended |
| External config  | ❌ No             | ✅ Yes         |

>[!important]
> Use Fluent API when you need **fine-grained control** or when attributes aren't expressive enough.

# Migrations

EF Core supports **code-first migrations**, allowing you to version and evolve your schema through code.

## Creating a Migration
```sh
dotnet ef migrations add InitialCreate
```
This generates a migration file under `Migrations/`, describing schema changes.

## Applying the Migration
```sh
dotnet ef database update
```
This updates the actual database to reflect the current model.

# Relationships in EF Core

EF Core allows you to model **real-world relationships** between entities. Relationships can be defined via **navigation properties** and optionally configured using **Fluent API** or **data annotations**.


##  One-to-One
Each entity has exactly one related entity.

```cs
public class Blog
{
    public int Id { get; set; }
    public string Name { get; set; }

    public List<Post> Posts { get; set; } = new();
}

public class Post
{
    public int Id { get; set; }
    public string Title { get; set; }

    public int BlogId { get; set; }           // foreign key
    public Blog Blog { get; set; }            // navigation
}
```

### Fluent API 

```cs
modelBuilder.Entity<Blog>()
    .HasMany(b => b.Posts)
    .WithOne(p => p.Blog)
    .HasForeignKey(p => p.BlogId);
```


##  One-to-Many

One entity has many related entities.

```cs
public class Student
{
    public int Id { get; set; }
    public string Name { get; set; }

    public List<Course> Courses { get; set; } = new();
}

public class Course
{
    public int Id { get; set; }
    public string Title { get; set; }

    public List<Student> Students { get; set; } = new();
}
```

### Fluent API 

```cs
modelBuilder.Entity<Blog>()
    .HasMany(b => b.Posts)
    .WithOne(p => p.Blog)
    .HasForeignKey(p => p.BlogId);
```

---

##  Many-to-Many

Each entity can relate to many instances of the other.

```cs
public class Student
{
    public int Id { get; set; }
    public string Name { get; set; }

    public List<Course> Courses { get; set; } = new();
}

public class Course
{
    public int Id { get; set; }
    public string Title { get; set; }

    public List<Student> Students { get; set; } = new();
}
```

Since EF Core 5.0, **no join entity is required**, unless you want to **store additional data** in the relationship.

### Fluent API
```cs
modelBuilder.Entity<Student>()
    .HasMany(s => s.Courses)
    .WithMany(c => c.Students);
```

###  Using a Join Entity (Enriched Many-to-Many)

If you need **extra fields** in the relationship:

```cs
public class Enrollment
{
    public int StudentId { get; set; }
    public Student Student { get; set; }

    public int CourseId { get; set; }
    public Course Course { get; set; }

    public DateTime EnrolledOn { get; set; }
}
```

Then configure:

```cs
modelBuilder.Entity<Enrollment>()
    .HasKey(e => new { e.StudentId, e.CourseId });

modelBuilder.Entity<Enrollment>()
    .HasOne(e => e.Student)
    .WithMany(s => s.Enrollments)
    .HasForeignKey(e => e.StudentId);

modelBuilder.Entity<Enrollment>()
    .HasOne(e => e.Course)
    .WithMany(c => c.Enrollments)
    .HasForeignKey(e => e.CourseId);
```


## Tips and Notes

- EF infers relationships from navigation + foreign keys.
- Always **initialize collections** to avoid nulls.
- Use `Include()` in LINQ to load related data:
    
```cs
var blogWithPosts = context.Blogs
    .Include(b => b.Posts)
    .FirstOrDefault();
```

- Without `Include()`, navigation properties are not loaded by default (lazy loading must be explicitly enabled).
# Common Errors

##  The process cannot access the file because it is being used by another process

- This typically happens if you're **running the app** while also trying to run a migration.
- Make sure to **stop the app** (or kill the process) before executing `dotnet ef`.

##  No `DbContext` Found

Make sure:
- The `DbContext` is in the same project or explicitly referenced.
- `dotnet ef` is run from the **startup project directory**.
- The context is properly registered in DI.

#  Useful EF Core Commands

| Command                           | Description                           |
| --------------------------------- | ------------------------------------- |
| `dotnet ef migrations add <Name>` | Create a new migration                |
| `dotnet ef database update`       | Apply latest migration to DB          |
| `dotnet ef migrations remove`     | Remove last migration (if un-applied) |
| `dotnet ef dbcontext list`        | Show available `DbContext` types      |
| `dotnet ef migrations list`       | Show applied and pending migrations   |
