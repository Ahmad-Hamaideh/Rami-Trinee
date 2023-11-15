
# The first download the package



`Microsoft.VisualStudio.Web.CodeGeneration.Design`   
`Microsoft.EntityFrameworkCore.Tools`  
`Microsoft.EntityFrameworkCore.SqlServer`  
`Microsoft.EntityFrameworkCore`


# ✨ Scaffold




```c#
Scaffold-DbContext 'Server=localhost\SQLEXPRESS;
Database=DataBaseEF;TrustServerCertificate=True;Trusted_Connection=True;
MultipleActiveResultSets=true' 
Microsoft.EntityFrameworkCore.SqlServer -ContextDir Models -OutputDir Models
```


## get conniction string

==> appsettings.json
```bash
  "ConnectionStrings": {
    "Index": "Server=(localdb)\\MSSQLLocalDB;Database=Ahmad_trenee;TrustServerCertificate=True;
    Trusted_Connection=True;MultipleActiveResultSets=true"
  }
```

==> Program.cs
```bash
  builder.Services.AddControllersWithViews();
string connection = builder.Configuration.GetConnectionString("Index");
builder.Services.AddDbContext<AhmadTreneeContext>(options => options.UseSqlServer(connection));

```

## 📚 ASP.NET Core Book 

[Donlowed Book](https://www.mediafire.com/download_repair.php?qkey=9slj4xo24sv1pu5&dkey=v4vpekb7iqr&template=51&origin=click_button)
