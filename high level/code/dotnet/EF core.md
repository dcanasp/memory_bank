the orm of the [[dotnet]] environment
first you have to add the package with the database you desire
`dotnet add package Microsoft.EntityFrameworkCore.Sqlite`



# migrations

```sh
dotnet ef migrations add InitialCreate
dotnet ef database update
```

# common errors
If you are executing a program, you can't migrate at the same time