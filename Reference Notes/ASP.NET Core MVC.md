- .NET 9
- File Explanation
- Main Concepts
- MVC
- EF Core
- CRUD
- Database Relationships

# MVC (Model-View-Controller)

- Separating responsibilities so it is more testable and modular.
- If UI logic changes often and is combined with business logic. Both the UI and the business logic need to be retest and modify both every time the UI changes.

## Model

- App's data
- App for managing books in a library: The model represents data about books and its rules for adding, updating, or removing books from the collection.

## View

- Part of the application that displays the data to the user.

## Controller

- Manages user input and interaction.
- Determining which model types to work with.
- Determining which view to render.

# File Explanation

- Program.cs is the entry point for the application.
	- `var builder = WebApplication.CreateBuilder(args);` initializes a new instance of the web application builder class which sets up the configuration services and the web server.
	- `builder.Services.AddControllerWithViews();` adds services to the dependency injection container. In this case, MVC services are added to the container.
	- `var app = builder.Build();` compiles the app, creating a web application instance which can be configured.
	- `if (!app.Environment.IsDevelopment()) {...}` configures the HTTP request pipeline which determines how requests are processed by the app. If the app is not in the development environment, exception handler will redirect users to the /Home/Error page. In addition, HTTP Strict Transport Security is enabled to enforce secure HTTPS connections.
	- `app.UseHttpsRedirection();` ensures HTTP requests are redirected to HTTPS.
	- `app.UseRouting();` enables routing which allows the app to match incoming requests to the appropriate endpoint.
	- `app.UseAuthorization();` authorizing users to access secured resources.
	- `app.MapStaticAssets();` enables serving static files (i.e., images, CSS, JS) from the /wwwroot folder
	- `app.MapControllerRoute(...);` sets up the default route pattern.
	- `app.Run();` starts the web application and begins listening for HTTP requests.
- Controllers handles the incoming HTTP requests, process user's input, and interact with the model to return the appropriate view.
- Models represents the data of the application
	- ErrorViewModel.cs is used for error handling.
- Views contains Razor View used to render HTML to the client.
	- \_ViewImports.cshtml contains directives (i.e., tag helpers) that are imported into every View.
	- \_ViewStart.cshtml specifies common View configurations (i.e., layout).
	- /Shared subfolders contains shared View.
		- \_Layout.cshtml used as the default design for all pages.
		- \_ValidationScriptsPartial.cshtml contains client side validation scripts
- appsettings.json file is the main configuration file for the application. It contains settings such as the ConnectionStrings and other app specific configurations.
- Properties/launchSettings.json file contains settings related to how the application is launched during development. Can be modified to the specific requirements of the project or different development environments.

# Main Concepts

- Create Models
	- Models represents tables in database.
	- Each property represents different columns the table will contain.
- Create Controllers
	- To access the data from the Model in the specific URL pattern /\<ModelName>s/\<ActionName>, the handling is defined in the controller.
	- Method in controller is called Action.
- Create Views
	- Object that is passed to the `View()` method as an argument is accessed inside View through `@Model`.
- IActionResult
	- Interface that defines contract to return different kinds of result to the user based on specific requirements.
	- `View()` is a helper method that is inherited from the `Controller` class which is the short for the `new ViewResult()`.
	- List of classes that implements `IActionResult` interface:
		- `ViewResult`
			- Returns an HTML view.
			- Example: `return View();`.
		- `JsonResult`
			- Returns JSON-formatted data.
			- Example: `return Json(data);`.
		- `ContentResult`
			- Returns plain text content.
			- Example: `return Content("plain text");`.
		- `RedirectResult`
			- Redirects to a URL.
			- Example: `return Redirect("url");`.
		- `RedirectToActionResult`
			- Returns to another action.
			- Example: `return RedirectToAction("ActionName");`.
		- `StatusCodeResult`
			- Returns a specific HTTP status code.
			- Example: `return StatusCode(404);`.
- Action Parameters
	- URL Segments.
	- Query Strings.
	- Form Submissions.
- Razor Syntax
	- `@{var message = "Hello, World!";}` --> `<p>@message</p>`
	- Directives are special instructions.
		- @page
		- @model
		- @using
	- Tag helpers allows for add dynamic behaviors and attributes to HTML elements. It makes Razor views cleaner and more maintainable.
		- `asp-for` ensures correct value is posted back to the server when the form is submitted.

# Entity Framework Core

- .NET developers toolset to simplify database access using .NET objects.
- Eliminates the need to write complex SQL queries by abstracting Data Query Language and Data Manipulation Language using C# code.
- Supports database operations: Create, Read, Update, Delete.
- Two Main Approaches
	- Code-First
		- Start without existing database.
			- Full control over data model through code.
	- Database-First
		- Generating C# classes and a DbContext from an existing database schema.
		- Suitable for working with legacy database or database design is managed outside of the application development process to integrate the existing database into the application.
			- Package Manager Console > Write Command `Scaffold-DbContext "..."`
- Project > Dependencies > Right Click > Manage NuGet Packages > Install Microsoft.EntityFrameworkCore > Install Microsoft.EntityFrameworkCore.Tools > Install Microsoft.EntityFrameworkCore.SqlServer
- To store Model inside database, create `Context` class which inherits from EF Core's `DbContext` class inside the Data directory.
	- `Context` is the main bridge that connects the project with the database.
- After inheriting the `DbContext`, create `Context` class constructor that contains few generic parameters to enable the needed configurations for the context.
- Store an instance for each model in the project with `DbSet` instance.
- View > Server Explorer > Data Connections > Right Click > Create New SQL Server Database > Connect
	- Connection String in Properties tells where the database is located.
- appsettings.json > Write `"ConnectionStrings"` 
- Program.cs > Add service in the services container to connect database with context.
	- `builder.Services.AddDbContext<...>(...);`
- Add migrations to the database: Tools > NuGet Package Manager > Package Manager Console > Write command `Add-Migration "..."` > Write command `Update-Database "..."`

# CRUD (Create Read Update Delete)

- To access database, context need to be injected to the controller class.
- When querying data from the database, make the Action method to be asynchronous. It will await data from the database, meaning the method will not continue until all the necessary data are retrieved.

## Create

### Controller

```c#
public IActionResult Create()
{
	return View();
}

[HttpPost]
public async Task<IActionResult> Create([Bind("Id, Name, Price")] Item item)
{
	if (ModelState.IsValid)
	{
		_context.Add(item);
		await _context.SaveChangesAsync();
		return RedirectToAction(nameof(Index));
	}
	return View(item);
}
```

### View

```c#
@model MyApp.Models.Item
@{
	ViewData["Title"] = "Create";
}

<h3>Create</h3>

<form asp-action="Create" method="post">
	<div class="form-group">
		<label class="form-label" asp-for="Name">Name</label>
		<input type="text"
			 class="form-control"
			 asp-for="Name" />
	</div>
	<div class="form-group">
		<label class="form-label" asp-for="Price">Price</label>
		<input type="text"
			 class="form-control"
			 asp-for="Price" />
	</div>
	<button class="btn btn-primary" type="submit">Submit</button>
</form>
```

## Read

### Controller

```c#
public IActionResult Create()
{
	return View();
}

[HttpPost]
public async Task<IActionResult> Create([Bind("Id, Name, Price")] Item item)
{
	if (ModelState.IsValid)
	{
		_context.Add(item);
		await _context.SaveChangesAsync();
		return RedirectToAction(nameof(Index));
	}
	return View(item);
}
```

### View

```c#
@model List<MyApp.Models.Item>
@{
	ViewData["Title"] = "Index";
}

<h3>Index</h3>

<table class="table">
    <thead>
        <tr>
            <th scope="col">Name</th>
            <th scope="col">Price</th>
        </tr>
    </thead>
    <tbody>
        @foreach (var item in Model)
        {
            <tr>
                <td>@item.Name</td>
                <td>@item.Price.ToString("N2") $</td>
                <td>
                    <a asp-action="Edit" asp-route-id="@item.Id">Edit</a>
                    <a asp-action="Delete" asp-route-id="@item.Id">Delete</a>
                </td>
            </tr>
		}
    </tbody>
</table>
```

## Update

### Controller

```c#
 public async Task<IActionResult> Edit(int id)
 {
     var item = await _context.Items.FindAsync(id);
     return View(item);
 }

 [HttpPost]
 public async Task<IActionResult> Edit([Bind("Id, Name, Price")] Item item)
 {
     if (ModelState.IsValid)
     {
         var i = await _context.Items.FindAsync(item.Id);
         if (i == null)
         {
             return NotFound();
         }
         i.Name = item.Name;
         i.Price = item.Price;

         await _context.SaveChangesAsync();
         return RedirectToAction(nameof(Index));
     }
     return View(item);
 }

```

### View

```c#
@model MyApp.Models.Item
@{
	ViewData["Title"] = "Edit";
}

<h3>Edit</h3>

<form asp-action="Edit" method="post">
	<input type="hidden" asp-for="Id" />
	<div class="form-group">
		<label class="form-label" asp-for="Name">Name</label>
		<input type="text"
			class="form-control"
			asp-for="Name" />
	</div>
	<div class="form-group">
		<label class="form-label" asp-for="Price">Price</label>
		<input type="text"
			class="form-control"
			asp-for="Price" />
	</div>
	<button class="btn btn-primary" type="submit">Submit</button>
</form>
```

## Delete

### Controller

```c#
public async Task<IActionResult> Delete(int id)
{
	var item = await _context.Items.FindAsync(id);
	return View(item);
}

[HttpPost, ActionName("Delete")]
public async Task<IActionResult> DeleteConfirmed(int id)
{
	var item = await _context.Items.FindAsync(id);
	if (item != null)
	{
		_context.Items.Remove(item);
		await _context.SaveChangesAsync();
	}
   return RedirectToAction(nameof(Index));
}
```

### View

```c#
@model MyApp.Models.Item
@{
	ViewData["Title"] = "Delete";
}

<h3>Are you sure you want to delete this item?</h3>

<p>@Model.Name</p>
<p>@Model.Price $</p>

<form asp-action="Delete" method="post">
	<input type="hidden" asp-for="Id" />
	<button class="btn btn-danger" type="submit">Delete</button>
</form>
```

# Database Relationships

## 1:1 (One-To-One)

### 1 (One, Principal)

```c#
using System.ComponentModel.DataAnnotations;

namespace MyApp.Models
{
    public class Item
    {
        public int Id { get; set; }
        public string Name { get; set; } = null!;
        public double Price { get; set; }
        public SerialNumber? SerialNumber { get; set; }
    }
}
```

### 1 (One, Dependent)

```c#

using System.ComponentModel.DataAnnotations.Schema;

namespace MyApp.Models
{
    public class SerialNumber
    {
        public int Id { get; set; }
        public string Name { get; set; } = null!;
        public int ItemId { get; set; }
        public Item? Item { get; set; }
    }
}

```

- Eager Loading: `var item = await _context.Items.Include(item => item.SerialNumber).ToListAsync();`
	- `.Include(item => item.SerialNumber)`: For each `item`, return its `SerialNumber` property.

## 1:N (One-To-Many)

1. Connect the models
2. Change the actions
3. Frontend

### 1 (One)
```c#
namespace MyApp.Models
{
    public class Category
    {
        public int Id { get; set; }
        public string Name { get; set; } = null!;
        public ICollection<Item>? Items { get; set; }
    }
}
```

### N (Many)
```c#
using System.ComponentModel.DataAnnotations;

namespace MyApp.Models
{
    public class Item
    {
        public int Id { get; set; }
        public string Name { get; set; } = null!;
        public double Price { get; set; }
        public SerialNumber? SerialNumber { get; set; }
        public int? CategoryId { get; set; }
        public Category? Category { get; set; }
    }
}
```

## M:N (Many-To-Many)

- Setting up models
- Configuring database
- Adjust app

> [!NOTE] 
> Require helper model

### M (Many)

- 

### N (Many)