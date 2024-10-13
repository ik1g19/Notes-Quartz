# Concepts

#c-sharp #dotnet #databases #udemy-course

# Introduction

Walking skeleton is a small implementation of a system that performs a small end-to-end function

It should link together the main architectural elements

![[notes/Courses/Udemy Courses/Complete guide to building an app with DotNet Core and React/Images/Pasted image 20230920235245.png]]

![[notes/Courses/Udemy Courses/Complete guide to building an app with DotNet Core and React/Images/Pasted image 20230920235352.png]]

# Creating DotNet Projects and References


`dotnet --info` to see installed versions

`dotnet new list` - a list of things we can create using the `dotnet` command line utility
- We are going to create a `webapi` project
- 3 class libraries
- Solution file
- Add our projects to the solution file which acts as a container for the projects

Creation script for the previous bullet points

## Linux

```bash
#!/usr/bin/env bash
green="\033[1;32m"
reset="\033[m"

echo "About to create the directory"
mkdir Reactivities
cd Reactivities

echo -e "${green}Creating solution and projects${reset}"
dotnet new sln
dotnet new webapi -n API
dotnet new classlib -n Application
dotnet new classlib -n Domain
dotnet new classlib -n Persistence

echo -e "${green}Adding projects to the solution${reset}"
dotnet sln add API/API.csproj
dotnet sln add Application/Application.csproj
dotnet sln add Domain/Domain.csproj
dotnet sln add Persistence/Persistence.csproj

echo -e "${green}Setting up project dependancies${reset}"
cd API
dotnet add reference ../Application/Application.csproj
cd ../Application
dotnet add reference ../Domain/Domain.csproj
dotnet add reference ../Persistence/Persistence.csproj
cd ../Persistence
dotnet add reference ../Domain/Domain.csproj
cd ..

echo -e "${green}Executing dotnet restore${reset}"
dotnet restore

echo -e "${green}Finished!${reset}"
```

## Windows Powershell

```powershell
Write-Host "About to Create the directory" -ForegroundColor Green

mkdir Reactivities
cd Reactivities

Write-Host "About to create the solution and projects" -ForegroundColor Green
dotnet new sln
dotnet new webapi -n API --use-controllers
dotnet new classlib -n Application
dotnet new classlib -n Domain
dotnet new classlib -n Persistence

Write-Host "Adding projects to the solution" -ForegroundColor Green
dotnet sln add API/API.csproj
dotnet sln add Application/Application.csproj
dotnet sln add Domain/Domain.csproj
dotnet sln add Persistence/Persistence.csproj

Write-Host "Adding project references" -ForegroundColor Green
cd API
dotnet add reference ../Application/Application.csproj
cd ../Application
dotnet add reference ../Domain/Domain.csproj
dotnet add reference ../Persistence/Persistence.csproj
cd ../Persistence
dotnet add reference ../Domain/Domain.csproj
cd ..

Write-Host "Executing dotnet restore" -ForegroundColor Green
dotnet restore

Write-Host "Finished!" -ForegroundColor Green

```


`dotnet restore` registers all the dependencies with the solution

# Reviewing Project Files and Startup

![[notes/Courses/Udemy Courses/Complete guide to building an app with DotNet Core and React/Introduction#VSCode Shortcuts]]

Run command `Generate Assets for Build and Debug` to create `.vscode` folder

cd to API and run `dotnet run` to start the application

`API>Propeties>launchSettings.json` contains the launch settings

We will use

```json
{
  "$schema": "http://json.schemastore.org/launchsettings.json",
  "profiles": {
    "http": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": false,
      "launchUrl": "swagger",
      "applicationUrl": "http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
  }
}
```

Change `launchBrowser` to `false` since we will be using Postman to interact with the API

We have chosen to use port 5000 in

```
"applicationUrl": "http://localhost:5000"
```

`Program.cs` is the entry point for any dotnet application

The configuration files are `appsettings.json` and `appsettings.Development.json`

When running in development `appsettings.Development.json` takes priority

We will change `appsettings.Development.json` to

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Information"
    }
  },
  "AllowedHosts": "*"
}
```

In `Program.cs`

```cs
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllers();
// Learn more about configuring Swagger/OpenAPI at https://aka.ms/aspnetcore/swashbuckle
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseAuthorization();

app.MapControllers();

app.Run();
```

Services are added at this point:

```cs
// Add services to the container.
builder.Services.AddControllers();
// Learn more about configuring Swagger/OpenAPI at https://aka.ms/aspnetcore/swashbuckle
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();
```

This section handles HTTP requests on their way in and out:

```cs
// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}
```

Any middleware will go in this section

`app.MapControllers();` is used to tell requests which controllers under `API>Controllers` they should be sent to

`app.Run()` starts the application

The server is now listening on `localhost:5000/swagger/index.html`
- This loads a page that tells us about our API endpoints and allows us to make requests

# The API Controller and using Postman

`app.MapControllers();` references the controllers under `API>Controllers`

Under `Controllers` is `WeatherForecastController.cs`

```cs
using Microsoft.AspNetCore.Mvc;

namespace API.Controllers;

[ApiController]
[Route("[controller]")]

public class WeatherForecastController : ControllerBase
{
    private static readonly string[] Summaries = new[]
    {
        "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
    };

    private readonly ILogger<WeatherForecastController> _logger;

    public WeatherForecastController(ILogger<WeatherForecastController> logger)
    {
        _logger = logger;
    }

    [HttpGet(Name = "GetWeatherForecast")]
    public IEnumerable<WeatherForecast> Get()
    {
        return Enumerable.Range(1, 5).Select(index => new WeatherForecast
        {
            Date = DateOnly.FromDateTime(DateTime.Now.AddDays(index)),
            TemperatureC = Random.Shared.Next(-20, 55),
            Summary = Summaries[Random.Shared.Next(Summaries.Length)]
        })
        .ToArray();
    }
}
```

Lines like these are attributes:

```cs
[ApiController]
```

This indicates that its a type of API Controller used to serve HTTP API responses

Each controller has a route:

```cs
[Route("[controller]")]
```

So that the application knows where to redirect the http request to

`[controller]` is a placeholder name for the actual name of the controller
- The controller gets its name from the name of the class (`WeatherForecastController`) minus the `Controller` at the end of the name

Each API controller derives from a base class `ControllerBase`

`[HttpGet(Name = "GetWeatherForecast")]` is an endpoint - which specifies which HTTP method is going to be used

Our CSharp project file is under `API>API.csproj`

```cs
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
    <Nullable>disable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
    <InvariantGlobalization>true</InvariantGlobalization>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Swashbuckle.AspNetCore" Version="6.4.0" />
  </ItemGroup>

  <ItemGroup>
    <ProjectReference Include="..\Application\Application.csproj" />
  </ItemGroup>

</Project>
```

`<ImplicitUsings>enable</ImplicitUsings>` enables the file `API>obj>Debugnet8.0>API.Globalusings.g.cs`, which implicitly enables a bunch of commonly used using statements for the program ^implicit-usings

`<Nullable>disable</Nullable>` means that datatypes like strings don't have to be set with the nullable `?` flag
- After dotnet 6.0 strings have to be declared with the nullable flag if you want them to be able to have a null value

We have to disable nullable in the project file for `API`, `Application`, `Domain` and `Persistence`

## Postman Requests

![[notes/Courses/Udemy Courses/Complete guide to building an app with DotNet Core and React/Images/Pasted image 20240420010417.png]]

We can import postman requests to test the API at different points



# Creating a Domain Entity

Our `Domain` project is going to contain our domain entities

We delete the default class under `Domain` and create a new C# class `Activity` (using the C# extension)

We can remove the unnecessary `using`s since we have [[#^implicit-usings|implicit usings]] enabled

To create properties for the class you can start writing `prop` and then vscode will autosuggest a property template with getters and setters

```cs
namespace Domain
{
    public class Activity
    {
        public Guid Id { get; set; }
        public string Title { get; set; }
        public DateTime Date { get; set; }
        public string Description { get; set; }
        public string Category { get; set; }
        public string City { get; set; }
        public string Venue { get; set; }
    }
}
```

Our ID property will be a `Guid`, it must specifically be called `Id` so that it is recognised by entity framework
- Entity framework also needs them all to be public and to have getters and setters

> [!info]
> In C# a GUID (Globally Unique Identifier) is a data type representing a 128-bit unique identifier. GUIDs are often used to uniquely identify entities such as objects, components, or resources in distributed systems where uniqueness across space and time is necessary

# Adding an Entity Framework Db Context

We need to start thinking about how we are going to create, store and interact with our database

An **Entity** is something that we are going to store and use inside our database

We are going to be using an Object Relational Mapper (ORM) - in this case, Entity framework, which will provide us with an abstraction away from our database - so we don't need to write queries directly against the database itself

An advantage of using an ORM is that later on we can swap our database technologies (e.g. from SQLite to something better) with minimal changes to our code

We open NuGet Gallery and look for `microsoft.entityframeworkcore` and then select `Microsoft.EntityFrameworkCore.Sqlite`
- We select `Persistence.csproj`
- We match the version to our dotnet version

>[!info]
>The NuGet Gallery is a central repository for discovering, installing, and publishing packages for the Microsoft development platform, particularly for .NET technologies. It's an online platform where developers can share reusable libraries, tools, frameworks, and other components packaged as NuGet packages


Delete the default class from `Persistence`

We create a new class called `DataContext`

We make the `DataContext` class inherit from `DbContext`, which is a part of the sqlite framework

We can then use the quick fix suggestion on the `DataContext` class to generate an empty constructor with the options parameter

![[notes/Courses/Udemy Courses/Complete guide to building an app with DotNet Core and React/Images/Pasted image 20240420205141.png]]

`DbSet`s represent the tables that we are going to create

```cs
using Domain;
using Microsoft.EntityFrameworkCore;

namespace Persistence
{
    public class DataContext : DbContext
    {
        public DataContext(DbContextOptions options) : base(options)
        {
        }
        public DbSet<Activity> Activities { get; set; }
    }
}
```

We now need to tell our application about the `DbContext` class

We specify in `Program.cs` that we want to add this as a service

>[!info]
>If vscode can't find `DbContext` then run `dotnet restore` in the terminal to make the package visible


```cs
// Add services to the container.

builder.Services.AddControllers();
// Learn more about configuring Swagger/OpenAPI at https://aka.ms/aspnetcore/swashbuckle
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();
builder.Services.AddDbContext<DataContext>(opt => {
 opt.UseSqlite(builder.Configuration.GetConnectionString("DefaultConnection" ));
});
```

We pass the options as a lambda expression, which contains the databases connection string

We then need to add the connection string to `appsettings.Development.json`

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Information"
    }
  },
  "ConnectionStrings": {
    "DefaultConnection": "Data Source=reactivities.db"
  }
}
```

>[!info]
>A `connection string` refers to a string that contains information necessary for establishing a connection to a data source, typically a database
>By configuring the connection string in the `appsettings.Development.json` file, you can easily change the database configuration without modifying the application code. This separation of configuration from code promotes flexibility and maintainability in your application.




# Creating an Entity Framework Code First Migration

We now create an Entity Framework Code First Migration

Since we've written the code first we are now going to create something that will generate the schema for the database

We can install `dotnet-ef` with

```powershell
dotnet tool install --global dotnet-ef --version 8.0.1
```

We need to install `Microsoft.EntityFrameworkCore.Design` to the `API` project to create migrations with `dotnet ef`

We then create our initial migration with

```
dotnet ef migrations add InitialCreate -s API -p Persistence
```

- `-s` is the startup project
- `-p` is the project where our data context resides

Inside the `Persistence` project we now have a folder called 📁`Migrations`

The `InitialCreate.cs` class is the class that was created by entity framework

It has two methods for moving up and moving down, the `CreateTable` method will create the database and use the field `Id` as the primary key

```cs
using System;
using Microsoft.EntityFrameworkCore.Migrations;

#nullable disable

namespace Persistence.Migrations
{
    /// <inheritdoc />
    public partial class InitialCreate : Migration
    {
        /// <inheritdoc />
        protected override void Up(MigrationBuilder migrationBuilder)
        {
            migrationBuilder.CreateTable(
                name: "Activities",
                columns: table => new
                {
                    Id = table.Column<Guid>(type: "TEXT", nullable: false),
                    Title = table.Column<string>(type: "TEXT", nullable: true),
                    Date = table.Column<DateTime>(type: "TEXT", nullable: false),
                    Description = table.Column<string>(type: "TEXT", nullable: true),
                    Category = table.Column<string>(type: "TEXT", nullable: true),
                    City = table.Column<string>(type: "TEXT", nullable: true),
                    Venue = table.Column<string>(type: "TEXT", nullable: true)
                },
                constraints: table =>
                {
                    table.PrimaryKey("PK_Activities", x => x.Id);
                });
        }

        /// <inheritdoc />
        protected override void Down(MigrationBuilder migrationBuilder)
        {
            migrationBuilder.DropTable(
                name: "Activities");
        }
    }
}

```

>[!info]
>In the context of Entity Framework Core migrations, "moving up" and "moving down" refer to the process of applying or reverting a database schema change.
>- **Moving Up (Upgrading):** When you apply a migration, you are "moving up" in the migration history. This means that you are applying the changes defined in the migration to the database schema. The `Up` method in the migration class contains the code necessary to apply these changes. It typically includes creating or altering database tables, columns, indexes, etc.
>- **Moving Down (Downgrading):** When you revert a migration, you are "moving down" in the migration history. This means that you are undoing the changes made by a specific migration. The `Down` method in the migration class contains the code necessary to revert the changes made in the `Up` method. It typically includes dropping tables, columns, indexes, etc.




# Creating the Database

We need to create a scope so that we have access to one of the services within the HTTP request scope

We use `using` since we want to control the lifetime of this variable, it would be garbage collected anyway but since we know we only want to use the variable temporarily we will use `using` so that the memory is freed after

```cs
using var scope = app.Services.CreateScope();
var services = scope.ServiceProvider;
```

We will now create the database using the initial migration in a try-catch block

```cs
try {
	var context = services.GetRequiredService<DataContext>();
	context.Database.Migrate();
}
catch (Exception ex) {
	var logger = services.GetRequiredService<ILogger<Program>>();
	logger.LogErrror(ex, "An error occured during migration");
}
```

`context.Database.Migrate();` is what updates the database to the latest migration

>[!info]
>`ILogger` is an interface in the .NET Core logging framework used for logging messages within an application. It's a generic interface, meaning you can specify the category of the logger, typically based on the class or component it's associated with


>[!info]
>- `app.Services.CreateScope()`: This creates a new scope within the application's dependency injection container. Scopes are used to manage the lifetime of objects and dependencies within a specific context, such as a request in a web application.
>- `scope.ServiceProvider`: This retrieves the service provider associated with the created scope. The service provider is responsible for resolving and providing instances of services when they are requested


Then running `dotnet run` inside the `API` folder will create the initial database and log to the migration table

# Seeding Data to the Database

Create a new class in 📁`Persistence` called `Seed.cs`

## Seed Data

`SeedData.txt` has seed data for the database

```
using Domain;
namespace Persistence
{
    public class Seed
    {
        public static async Task SeedData(DataContext context)
        {
            if (context.Activities.Any()) return;
            
            var activities = new List<Activity>
            {
                new Activity
                {
                    Title = "Past Activity 1",
                    Date = DateTime.UtcNow.AddMonths(-2),
                    Description = "Activity 2 months ago",
                    Category = "drinks",
                    City = "London",
                    Venue = "Pub",
                },
                new Activity
                {
                    Title = "Past Activity 2",
                    Date = DateTime.UtcNow.AddMonths(-1),
                    Description = "Activity 1 month ago",
                    Category = "culture",
                    City = "Paris",
                    Venue = "Louvre",
                },
                new Activity
                {
                    Title = "Future Activity 1",
                    Date = DateTime.UtcNow.AddMonths(1),
                    Description = "Activity 1 month in future",
                    Category = "culture",
                    City = "London",
                    Venue = "Natural History Museum",
                },
                new Activity
                {
                    Title = "Future Activity 2",
                    Date = DateTime.UtcNow.AddMonths(2),
                    Description = "Activity 2 months in future",
                    Category = "music",
                    City = "London",
                    Venue = "O2 Arena",
                },
                new Activity
                {
                    Title = "Future Activity 3",
                    Date = DateTime.UtcNow.AddMonths(3),
                    Description = "Activity 3 months in future",
                    Category = "drinks",
                    City = "London",
                    Venue = "Another pub",
                },
                new Activity
                {
                    Title = "Future Activity 4",
                    Date = DateTime.UtcNow.AddMonths(4),
                    Description = "Activity 4 months in future",
                    Category = "drinks",
                    City = "London",
                    Venue = "Yet another pub",
                },
                new Activity
                {
                    Title = "Future Activity 5",
                    Date = DateTime.UtcNow.AddMonths(5),
                    Description = "Activity 5 months in future",
                    Category = "drinks",
                    City = "London",
                    Venue = "Just another pub",
                },
                new Activity
                {
                    Title = "Future Activity 6",
                    Date = DateTime.UtcNow.AddMonths(6),
                    Description = "Activity 6 months in future",
                    Category = "music",
                    City = "London",
                    Venue = "Roundhouse Camden",
                },
                new Activity
                {
                    Title = "Future Activity 7",
                    Date = DateTime.UtcNow.AddMonths(7),
                    Description = "Activity 2 months ago",
                    Category = "travel",
                    City = "London",
                    Venue = "Somewhere on the Thames",
                },
                new Activity
                {
                    Title = "Future Activity 8",
                    Date = DateTime.UtcNow.AddMonths(8),
                    Description = "Activity 8 months in future",
                    Category = "film",
                    City = "London",
                    Venue = "Cinema",
                }
            };

            await context.Activities.AddRangeAsync(activities);
            await context.SaveChangesAsync();
        }
    }
}

```

## Using Seed Data

We then seed the data in `Program.cs`

`Seed` returns an asynchronous task, so to use the method in our `Program` class we have to use `await`
- We will receive a notification from a delegate once it has updated the database
- We will use the asynchronous version of Migrate as well

```cs
try {
    var context = services.GetRequiredService<DataContext>();
    await context.Database.MigrateAsync(); //seeds here
    await Seed.SeedData(context);
}

catch (Exception ex) {
    var logger = services.GetRequiredService<ILogger<Program>>();
    logger.LogError(ex, "An error occured during migration");
}
```

The activities will now be visible in the activities db when the app is started

# Adding an API Controller

Now we have data in the database we need to create a controller so that we can query the database and return data inside a HTTP response

We create a new controller under 📁`Controllers` called `BaseApiController.cs`

```cs
using Microsoft.AspNetCore.Mvc;

namespace API.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class BaseApiController : ControllerBase
    {

    }
}
```

It derives from `ControllerBase`

`[Route("api/[controller]")]` means that to reach this controller you have to use 
`/api/"controller-name"
`
>[!info]
> The text between the square brackets `[api/controller]` is an attribute used in C# and ASP.NET Core for routing. In this case, it's defining that the controller will be accessible under the API endpoint `/api/{controller}` (where {controller} is the name of the controller class)
> `[ApiController]` is a convenient attribute that sets up various features for building RESTful APIs with ASP.NET Core, including automatic model state validation, response formatting, and error handling

We create another new controller under 📁`Controllers` called `ActivitiesController`

```cs
using Domain;
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;
using Persistence;

namespace API.Controllers
{
    public class ActivitiesController : BaseApiController
    {
        private readonly DataContext _context;

        public ActivitiesController(DataContext context)
        {
            _context = context;
        }

        [HttpGet] //api/activities
        public async Task<ActionResult<List<Activity>>> GetActivities()
        {
            return await _context.Activities.ToListAsync();
        }

        [HttpGet("{id}")] //api/activities/given-id
        public async Task<ActionResult<Activity>> GetActivity(Guid id)
        {
            return await _context.Activities.FindAsync(id);
        }
    }
}
```

The controller has two endpoints

1. The first endpoint is for the HTTP GET method with no route parameters. This endpoint is mapped to the URL path `/api/activities`. When this endpoint is called, it returns a list of all activities from the database

2. The second endpoint is for the HTTP GET method with a route parameter named "id". This endpoint is mapped to the URL path `/api/activities/{id}`, where {id} is a placeholder for a specific activity identifier. When this endpoint is called, it returns the activity with the given id from the database

>[!info]
>`[HttpGet]` is a C# attribute that is part of the `Microsoft.AspNetCore.Mvc` namespace in .NET. It's used to mark an action method as handling HTTP GET requests

## In Postman

![[notes/Courses/Udemy Courses/Complete guide to building an app with DotNet Core and React/Images/Pasted image 20240421232319.png]]

![[notes/Courses/Udemy Courses/Complete guide to building an app with DotNet Core and React/Images/Pasted image 20240421232334.png]]