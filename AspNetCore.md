# ASP.NET Core Interview Questions and Answers

Based on the ASP.NET Core Developer Roadmap (roadmap.sh/aspnet-core)

---

## Table of Contents
1. [Fundamentals](#fundamentals)
2. [Middleware](#middleware)
3. [Dependency Injection](#dependency-injection)
4. [Routing](#routing)
5. [Controllers and Actions](#controllers-and-actions)
6. [Model Binding and Validation](#model-binding-and-validation)
7. [Views and Razor Pages](#views-and-razor-pages)
8. [Entity Framework Core](#entity-framework-core)
9. [Web API](#web-api)
10. [Authentication and Authorization](#authentication-and-authorization)
11. [Configuration](#configuration)
12. [Logging](#logging)
13. [Error Handling](#error-handling)
14. [Caching](#caching)
15. [SignalR](#signalr)
16. [gRPC](#grpc)
17. [Docker and Containerization](#docker-and-containerization)
18. [Deployment and DevOps](#deployment-and-devops)
19. [Testing](#testing)
20. [Performance Optimization](#performance-optimization)
21. [Blazor](#blazor)

---

## Fundamentals

### Q1: What is ASP.NET Core?

**Answer:**
ASP.NET Core is an open-source, cross-platform framework developed by Microsoft for building modern, cloud-based, internet-connected applications. It is a complete redesign of the original ASP.NET framework, offering:

- **Cross-platform support**: Runs on Windows, macOS, and Linux
- **High performance**: Built from the ground up for speed and scalability
- **Modular architecture**: Include only the components you need
- **Open-source**: Available on GitHub with active community support
- **Cloud-ready**: Designed for cloud deployment and microservices architecture

### Q2: How does ASP.NET Core differ from the traditional ASP.NET Framework?

**Answer:**
Key differences include:

| Feature | ASP.NET Framework | ASP.NET Core |
|---------|-------------------|--------------|
| **Platform** | Windows only | Cross-platform (Windows, macOS, Linux) |
| **Open Source** | No | Yes |
| **Performance** | Good | Significantly better |
| **Architecture** | Monolithic | Modular and lightweight |
| **Dependency Injection** | Optional (third-party) | Built-in |
| **Hosting** | IIS only | IIS, Kestrel, Nginx, Apache |
| **Package Management** | NuGet | NuGet |
| **.NET Version** | .NET Framework | .NET Core/.NET 5+ |

### Q3: What is the role of the `Program.cs` file in ASP.NET Core?

**Answer:**
The `Program.cs` file is the entry point of an ASP.NET Core application. It contains the `Main` method that:

- Creates and configures the web host
- Sets up the application's infrastructure
- Configures services and middleware
- Builds and runs the application

**Example:**
```csharp
var builder = WebApplication.CreateBuilder(args);

// Add services to the container
builder.Services.AddControllers();

var app = builder.Build();

// Configure the HTTP request pipeline
app.UseAuthorization();
app.MapControllers();

app.Run();
```

### Q4: What is the difference between .NET Core, .NET 5, .NET 6, and .NET 7+?

**Answer:**
- **.NET Core** (1.0-3.1): The initial cross-platform implementation
- **.NET 5**: Unified platform (dropped "Core" from the name)
- **.NET 6**: Long-term support (LTS) release with improved performance
- **.NET 7+**: Latest features with continued performance improvements

All versions support ASP.NET Core, with newer versions offering better performance and more features.

---

## Middleware

### Q5: What is middleware in ASP.NET Core?

**Answer:**
Middleware are software components that are assembled into an application pipeline to handle requests and responses. Each middleware component:

- Can perform operations before and after the next component
- Can short-circuit the pipeline (stop processing)
- Can pass control to the next middleware
- Can modify the request or response

**Example:**
```csharp
app.Use(async (context, next) =>
{
    // Do something before the next middleware
    await next();
    // Do something after the next middleware
});
```

### Q6: What is the difference between `Use`, `Run`, and `Map` in middleware?

**Answer:**

- **`Use`**: Adds middleware to the pipeline that can call the next middleware
  ```csharp
  app.Use(async (context, next) => {
      await next();
  });
  ```

- **`Run`**: Adds terminal middleware that doesn't call the next middleware
  ```csharp
  app.Run(async context => {
      await context.Response.WriteAsync("Hello World");
  });
  ```

- **`Map`**: Branches the pipeline based on the request path
  ```csharp
  app.Map("/api", app => {
      app.UseRouting();
      app.UseEndpoints(endpoints => endpoints.MapControllers());
  });
  ```

### Q7: Explain the middleware execution order and why it matters.

**Answer:**
Middleware executes in the order it's registered. The order is critical because:

1. **Request flows down** through middleware in registration order
2. **Response flows up** through middleware in reverse order

**Common order:**
```csharp
app.UseExceptionHandler();        // Handle exceptions first
app.UseHttpsRedirection();         // Redirect HTTP to HTTPS
app.UseStaticFiles();              // Serve static files
app.UseRouting();                  // Route matching
app.UseAuthentication();          // Authentication before authorization
app.UseAuthorization();            // Authorization
app.MapControllers();              // Map controller routes
```

**Why it matters:** If authentication middleware comes after routing, authentication won't work for routed requests.

### Q8: How do you create custom middleware?

**Answer:**
You can create custom middleware in three ways:

**1. Inline middleware:**
```csharp
app.Use(async (context, next) =>
{
    // Custom logic
    await next();
});
```

**2. Class-based middleware:**
```csharp
public class CustomMiddleware
{
    private readonly RequestDelegate _next;

    public CustomMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        // Custom logic before
        await _next(context);
        // Custom logic after
    }
}

// Usage
app.UseMiddleware<CustomMiddleware>();
```

**3. Extension method:**
```csharp
public static class CustomMiddlewareExtensions
{
    public static IApplicationBuilder UseCustomMiddleware(
        this IApplicationBuilder builder)
    {
        return builder.UseMiddleware<CustomMiddleware>();
    }
}
```

---

## Dependency Injection

### Q9: What is Dependency Injection (DI) and why is it important?

**Answer:**
Dependency Injection is a design pattern that promotes:

- **Loose coupling**: Classes depend on abstractions, not concrete implementations
- **Testability**: Easy to mock dependencies in unit tests
- **Maintainability**: Changes to implementations don't affect dependent classes
- **Flexibility**: Swap implementations without changing dependent code

ASP.NET Core has built-in DI container that manages object lifetimes and resolves dependencies automatically.

### Q10: Explain the three service lifetimes: Singleton, Scoped, and Transient.

**Answer:**

| Lifetime | Description | Use Case | Instance Created |
|----------|-------------|----------|------------------|
| **Singleton** | Single instance for the application lifetime | Logging, configuration, caching | Once at startup |
| **Scoped** | One instance per HTTP request | Database contexts, repositories | Once per request |
| **Transient** | New instance every time it's requested | Lightweight, stateless services | Every time requested |

**Example:**
```csharp
services.AddSingleton<IMyService, MyService>();    // One instance
services.AddScoped<IMyService, MyService>();       // One per request
services.AddTransient<IMyService, MyService>();     // New each time
```

### Q11: What happens if you inject a Scoped service into a Singleton service?

**Answer:**
This creates a **captive dependency** problem. The Scoped service becomes effectively a Singleton because it's captured by the Singleton's lifetime. This can cause:

- **Memory leaks**: Scoped resources aren't disposed properly
- **State issues**: Shared state across requests
- **Database context issues**: EF Core DbContext should be Scoped, not Singleton

**Solution:** Don't inject Scoped services into Singleton services. Use a service locator pattern or refactor the architecture.

### Q12: How do you register services with different interfaces?

**Answer:**
You can register services in multiple ways:

```csharp
// Register with interface
services.AddScoped<IUserService, UserService>();

// Register concrete type
services.AddScoped<UserService>();

// Register with factory
services.AddScoped<IUserService>(sp => 
    new UserService(sp.GetRequiredService<ILogger>()));

// Register multiple implementations
services.AddScoped<IValidator, EmailValidator>();
services.AddScoped<IValidator, PhoneValidator>();
```

---

## Routing

### Q13: What are the two types of routing in ASP.NET Core?

**Answer:**

1. **Convention-based routing**: Defined in `Startup.cs` or `Program.cs`
   ```csharp
   app.MapControllerRoute(
       name: "default",
       pattern: "{controller=Home}/{action=Index}/{id?}");
   ```

2. **Attribute routing**: Defined using attributes on controllers and actions
   ```csharp
   [Route("api/[controller]")]
   public class UsersController : ControllerBase
   {
       [HttpGet("{id}")]
       public IActionResult Get(int id) { }
   }
   ```

**Attribute routing is preferred** in modern ASP.NET Core applications, especially for APIs.

### Q14: How do route constraints work?

**Answer:**
Route constraints restrict the values that can match a route parameter:

```csharp
[Route("api/users/{id:int}")]           // Only integers
[Route("api/users/{id:min(1)}")]        // Minimum value
[Route("api/users/{name:alpha}")]       // Only letters
[Route("api/users/{email:email}")]      // Email format
[Route("api/users/{id:regex(^\\d{{3}}$)}")]  // Regex pattern
```

### Q15: What is route model binding?

**Answer:**
Route model binding automatically maps route parameters, query strings, and form data to action method parameters:

```csharp
[HttpGet("users/{id}")]
public IActionResult GetUser(int id, string name, int? page)
{
    // id comes from route
    // name comes from query string (?name=value)
    // page comes from query string (?page=1)
}
```

---

## Controllers and Actions

### Q16: What is the difference between `Controller` and `ControllerBase`?

**Answer:**

- **`Controller`**: Includes support for views (MVC)
  - Inherits from `ControllerBase`
  - Adds view-related methods like `View()`, `PartialView()`, `RedirectToAction()`

- **`ControllerBase`**: Base class for API controllers
  - Lighter weight
  - No view support
  - Use for Web APIs

**Best Practice:** Use `ControllerBase` for APIs, `Controller` for MVC applications.

### Q17: Explain action method return types.

**Answer:**

| Return Type | Use Case | Example |
|-------------|----------|---------|
| `IActionResult` | Multiple return types | `Ok()`, `NotFound()`, `BadRequest()` |
| `ActionResult<T>` | Strongly-typed with multiple return types | `ActionResult<User>` |
| `T` | Direct return of model | `User GetUser()` |
| `Task<IActionResult>` | Async operations | `async Task<IActionResult> GetUser()` |

**Example:**
```csharp
[HttpGet("{id}")]
public ActionResult<User> GetUser(int id)
{
    var user = _userService.GetUser(id);
    if (user == null) return NotFound();
    return Ok(user);
}
```

### Q18: What are action filters and how do you use them?

**Answer:**
Action filters allow you to run code before or after action methods execute:

**Types:**
- **Authorization filters**: Run first (e.g., `[Authorize]`)
- **Resource filters**: Run after authorization
- **Action filters**: Run before and after action execution
- **Exception filters**: Handle exceptions
- **Result filters**: Run before and after result execution

**Example:**
```csharp
public class LogActionFilter : IActionFilter
{
    public void OnActionExecuting(ActionExecutingContext context)
    {
        // Before action
    }

    public void OnActionExecuted(ActionExecutedContext context)
    {
        // After action
    }
}

// Usage
[ServiceFilter(typeof(LogActionFilter))]
public IActionResult MyAction() { }
```

---

## Model Binding and Validation

### Q19: How does model binding work in ASP.NET Core?

**Answer:**
Model binding automatically maps HTTP request data to action method parameters or model properties. It searches in this order:

1. Form data
2. Route values
3. Query string parameters
4. Request body (for POST/PUT)

**Example:**
```csharp
[HttpPost]
public IActionResult CreateUser([FromBody] User user)
{
    // user is automatically populated from JSON body
}
```

**Binding sources:**
- `[FromBody]` - Request body
- `[FromForm]` - Form data
- `[FromRoute]` - Route parameters
- `[FromQuery]` - Query string
- `[FromHeader]` - HTTP headers

### Q20: How do you implement model validation?

**Answer:**
Use data annotations or FluentValidation:

**Data Annotations:**
```csharp
public class User
{
    [Required]
    [StringLength(100)]
    public string Name { get; set; }

    [EmailAddress]
    public string Email { get; set; }

    [Range(18, 100)]
    public int Age { get; set; }
}

[HttpPost]
public IActionResult CreateUser([FromBody] User user)
{
    if (!ModelState.IsValid)
        return BadRequest(ModelState);
    
    // Process user
}
```

**FluentValidation:**
```csharp
public class UserValidator : AbstractValidator<User>
{
    public UserValidator()
    {
        RuleFor(x => x.Name).NotEmpty().MaximumLength(100);
        RuleFor(x => x.Email).EmailAddress();
    }
}
```

### Q21: What is `ModelState` and how is it used?

**Answer:**
`ModelState` is a dictionary that contains:
- Model binding errors
- Validation errors
- Model property values

**Usage:**
```csharp
if (!ModelState.IsValid)
{
    return BadRequest(ModelState);
}

// Check specific property
if (!ModelState.IsValidField("Email"))
{
    // Handle email validation error
}
```

---

## Views and Razor Pages

### Q22: What is the difference between Razor Pages and MVC?

**Answer:**

| Feature | Razor Pages | MVC |
|---------|-------------|-----|
| **Model** | Page-based | Controller-based |
| **File Structure** | One file per page | Separate controller/view |
| **Use Case** | Simple CRUD, forms | Complex applications |
| **Routing** | File-based | Convention/attribute-based |
| **Code Organization** | PageModel class | Controller + View |

**Razor Pages Example:**
```csharp
// Pages/Users/Index.cshtml.cs
public class IndexModel : PageModel
{
    public void OnGet() { }
    public IActionResult OnPost() { }
}
```

**MVC Example:**
```csharp
// Controllers/UsersController.cs
public class UsersController : Controller
{
    public IActionResult Index() => View();
}
```

### Q23: What are Tag Helpers?

**Answer:**
Tag Helpers enable server-side code to participate in creating and rendering HTML elements in Razor files. They provide a cleaner, more HTML-like syntax.

**Built-in Tag Helpers:**
```html
<!-- Form -->
<form asp-action="Create" asp-controller="Users" method="post">
    <input asp-for="Name" />
    <span asp-validation-for="Name"></span>
    <select asp-for="CategoryId" asp-items="Model.Categories"></select>
</form>

<!-- Links -->
<a asp-controller="Users" asp-action="Details" asp-route-id="@user.Id">View</a>

<!-- Images -->
<img asp-append-version="true" src="~/images/logo.png" />
```

### Q24: How do you create custom Tag Helpers?

**Answer:**
```csharp
[HtmlTargetElement("email")]
public class EmailTagHelper : TagHelper
{
    public string MailTo { get; set; }

    public override void Process(TagHelperContext context, TagHelperOutput output)
    {
        output.TagName = "a";
        output.Attributes.SetAttribute("href", $"mailto:{MailTo}");
        output.Content.SetContent(MailTo);
    }
}

// Usage in Razor
<email mail-to="user@example.com" />
```

---

## Entity Framework Core

### Q25: What is Entity Framework Core?

**Answer:**
Entity Framework Core (EF Core) is a lightweight, extensible, open-source, and cross-platform Object-Relational Mapping (ORM) framework for .NET. It allows developers to work with databases using .NET objects.

**Key Features:**
- Code-first and database-first approaches
- LINQ queries
- Change tracking
- Migrations
- Multiple database providers (SQL Server, PostgreSQL, MySQL, SQLite, etc.)

### Q26: Explain the DbContext and its role.

**Answer:**
`DbContext` represents a session with the database and provides:

- **Querying**: Execute LINQ queries against the database
- **Change Tracking**: Track changes to entities
- **Persistence**: Save changes to the database
- **Configuration**: Configure entity relationships and mappings

**Example:**
```csharp
public class ApplicationDbContext : DbContext
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
        : base(options) { }

    public DbSet<User> Users { get; set; }
    public DbSet<Order> Orders { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        // Configure entities
        modelBuilder.Entity<User>().HasKey(u => u.Id);
    }
}
```

### Q27: What are EF Core migrations and how do you use them?

**Answer:**
Migrations are a way to evolve your database schema over time while keeping it in sync with your entity models.

**Commands:**
```bash
# Add a migration
dotnet ef migrations add InitialCreate

# Update database
dotnet ef database update

# Remove last migration
dotnet ef migrations remove

# Generate SQL script
dotnet ef migrations script
```

**In Code:**
```csharp
// Program.cs
using (var scope = app.Services.CreateScope())
{
    var db = scope.ServiceProvider.GetRequiredService<ApplicationDbContext>();
    db.Database.Migrate();
}
```

### Q28: Explain the difference between `IQueryable` and `IEnumerable` in EF Core.

**Answer:**

| Feature | IQueryable | IEnumerable |
|---------|------------|-------------|
| **Execution** | Deferred (executes on database) | Deferred (executes in memory) |
| **Where** | Database query | In-memory filter |
| **Performance** | Better for large datasets | Better for small, in-memory collections |
| **Use Case** | Database queries | In-memory collections |

**Example:**
```csharp
// IQueryable - executes on database
var users = _context.Users.Where(u => u.Age > 18).ToList();

// IEnumerable - loads all, then filters in memory
var users = _context.Users.ToList().Where(u => u.Age > 18);
```

### Q29: How do you handle database transactions in EF Core?

**Answer:**
```csharp
// Automatic transaction (default)
using var transaction = await _context.Database.BeginTransactionAsync();
try
{
    _context.Users.Add(user);
    _context.Orders.Add(order);
    await _context.SaveChangesAsync();
    await transaction.CommitAsync();
}
catch
{
    await transaction.RollbackAsync();
    throw;
}

// Using TransactionScope
using var scope = new TransactionScope(TransactionScopeAsyncFlowOption.Enabled);
try
{
    // Multiple operations
    await scope.CompleteAsync();
}
```

---

## Web API

### Q30: How do you create a RESTful API in ASP.NET Core?

**Answer:**
```csharp
[ApiController]
[Route("api/[controller]")]
public class UsersController : ControllerBase
{
    [HttpGet]
    public ActionResult<IEnumerable<User>> GetUsers()
    {
        return Ok(_userService.GetAll());
    }

    [HttpGet("{id}")]
    public ActionResult<User> GetUser(int id)
    {
        var user = _userService.GetById(id);
        if (user == null) return NotFound();
        return Ok(user);
    }

    [HttpPost]
    public ActionResult<User> CreateUser([FromBody] User user)
    {
        var created = _userService.Create(user);
        return CreatedAtAction(nameof(GetUser), new { id = created.Id }, created);
    }

    [HttpPut("{id}")]
    public IActionResult UpdateUser(int id, [FromBody] User user)
    {
        _userService.Update(id, user);
        return NoContent();
    }

    [HttpDelete("{id}")]
    public IActionResult DeleteUser(int id)
    {
        _userService.Delete(id);
        return NoContent();
    }
}
```

### Q31: What is content negotiation in Web API?

**Answer:**
Content negotiation allows the API to return data in different formats (JSON, XML, etc.) based on the client's `Accept` header.

**Configuration:**
```csharp
services.AddControllers()
    .AddXmlSerializerFormatters()
    .AddJsonOptions(options =>
    {
        options.JsonSerializerOptions.PropertyNamingPolicy = JsonNamingPolicy.CamelCase;
    });
```

**Client Request:**
```
GET /api/users
Accept: application/xml
```

### Q32: How do you implement API versioning?

**Answer:**
```csharp
// Install: Microsoft.AspNetCore.Mvc.Versioning

services.AddApiVersioning(options =>
{
    options.DefaultApiVersion = new ApiVersion(1, 0);
    options.AssumeDefaultVersionWhenUnspecified = true;
    options.ReportApiVersions = true;
});

// Usage
[ApiVersion("1.0")]
[Route("api/v{version:apiVersion}/[controller]")]
public class UsersController : ControllerBase { }

[ApiVersion("2.0")]
[Route("api/v{version:apiVersion}/[controller]")]
public class UsersV2Controller : ControllerBase { }
```

### Q33: What is Swagger/OpenAPI and how do you integrate it?

**Answer:**
Swagger/OpenAPI provides interactive API documentation and testing.

**Setup:**
```csharp
services.AddEndpointsApiExplorer();
services.AddSwaggerGen(c =>
{
    c.SwaggerDoc("v1", new OpenApiInfo 
    { 
        Title = "My API", 
        Version = "v1" 
    });
});

// In pipeline
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}
```

Access at `/swagger` endpoint.

---

## Authentication and Authorization

### Q34: What authentication schemes are available in ASP.NET Core?

**Answer:**
- **Cookie Authentication**: Traditional web apps
- **JWT (JSON Web Tokens)**: APIs and SPAs
- **OAuth 2.0 / OpenID Connect**: Third-party authentication (Google, Facebook, etc.)
- **Windows Authentication**: Intranet applications
- **Identity**: ASP.NET Core Identity for user management

### Q35: How do you implement JWT authentication?

**Answer:**
```csharp
// Configure services
services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddJwtBearer(options =>
    {
        options.TokenValidationParameters = new TokenValidationParameters
        {
            ValidateIssuer = true,
            ValidateAudience = true,
            ValidateLifetime = true,
            ValidateIssuerSigningKey = true,
            ValidIssuer = Configuration["Jwt:Issuer"],
            ValidAudience = Configuration["Jwt:Audience"],
            IssuerSigningKey = new SymmetricSecurityKey(
                Encoding.UTF8.GetBytes(Configuration["Jwt:Key"]))
        };
    });

// Generate token
var token = new JwtSecurityToken(
    issuer: _configuration["Jwt:Issuer"],
    audience: _configuration["Jwt:Audience"],
    claims: claims,
    expires: DateTime.UtcNow.AddHours(1),
    signingCredentials: credentials
);

// Protect endpoints
[Authorize]
[HttpGet]
public IActionResult GetProtectedData() { }
```

### Q36: Explain the difference between Authentication and Authorization.

**Answer:**

- **Authentication**: Verifying who the user is (login process)
  - "Who are you?"
  - Examples: Username/password, JWT token validation

- **Authorization**: Determining what the user can do (permissions)
  - "What are you allowed to do?"
  - Examples: Role-based access, policy-based authorization

### Q37: How do you implement role-based authorization?

**Answer:**
```csharp
// Configure
services.AddAuthorization(options =>
{
    options.AddPolicy("AdminOnly", policy => policy.RequireRole("Admin"));
    options.AddPolicy("ManagerOrAdmin", policy => 
        policy.RequireRole("Manager", "Admin"));
});

// Usage
[Authorize(Roles = "Admin")]
public IActionResult AdminOnly() { }

[Authorize(Policy = "ManagerOrAdmin")]
public IActionResult ManagerOrAdmin() { }
```

### Q38: What is policy-based authorization?

**Answer:**
Policy-based authorization allows you to define custom authorization logic:

```csharp
services.AddAuthorization(options =>
{
    options.AddPolicy("MinimumAge", policy =>
        policy.Requirements.Add(new MinimumAgeRequirement(18)));
});

public class MinimumAgeRequirement : IAuthorizationRequirement
{
    public int MinimumAge { get; }
    public MinimumAgeRequirement(int minimumAge) => MinimumAge = minimumAge;
}

public class MinimumAgeHandler : AuthorizationHandler<MinimumAgeRequirement>
{
    protected override Task HandleRequirementAsync(
        AuthorizationHandlerContext context,
        MinimumAgeRequirement requirement)
    {
        var age = int.Parse(context.User.FindFirst("Age").Value);
        if (age >= requirement.MinimumAge)
            context.Succeed(requirement);
        return Task.CompletedTask;
    }
}
```

---

## Configuration

### Q39: How does the configuration system work in ASP.NET Core?

**Answer:**
ASP.NET Core uses a hierarchical configuration system that reads from multiple sources:

**Sources (in order of precedence):**
1. Command-line arguments (highest)
2. Environment variables
3. User secrets (development)
4. `appsettings.{Environment}.json`
5. `appsettings.json` (lowest)

**Example:**
```csharp
var builder = WebApplication.CreateBuilder(args);

// Access configuration
var connectionString = builder.Configuration.GetConnectionString("DefaultConnection");
var apiKey = builder.Configuration["ApiSettings:ApiKey"];

// Strongly-typed configuration
var apiSettings = builder.Configuration.GetSection("ApiSettings").Get<ApiSettings>();
```

### Q40: What are Options Pattern and IOptions?

**Answer:**
The Options pattern provides a strongly-typed way to access configuration:

```csharp
// appsettings.json
{
  "ApiSettings": {
    "ApiKey": "12345",
    "BaseUrl": "https://api.example.com"
  }
}

// Class
public class ApiSettings
{
    public string ApiKey { get; set; }
    public string BaseUrl { get; set; }
}

// Register
services.Configure<ApiSettings>(
    Configuration.GetSection("ApiSettings"));

// Inject
public class MyService
{
    private readonly ApiSettings _settings;
    
    public MyService(IOptions<ApiSettings> options)
    {
        _settings = options.Value;
    }
}
```

**IOptions vs IOptionsSnapshot vs IOptionsMonitor:**
- `IOptions`: Singleton, reads once at startup
- `IOptionsSnapshot`: Scoped, reads on each request (supports reload)
- `IOptionsMonitor`: Singleton, supports change notifications

---

## Logging

### Q41: How do you implement logging in ASP.NET Core?

**Answer:**
ASP.NET Core has built-in logging support:

```csharp
public class MyService
{
    private readonly ILogger<MyService> _logger;

    public MyService(ILogger<MyService> logger)
    {
        _logger = logger;
    }

    public void DoWork()
    {
        _logger.LogInformation("Starting work");
        _logger.LogWarning("This is a warning");
        _logger.LogError("This is an error");
        _logger.LogCritical("This is critical");
    }
}
```

**Log Levels:**
- `Trace` (0): Most detailed
- `Debug` (1): Debug information
- `Information` (2): General information
- `Warning` (3): Warnings
- `Error` (4): Errors
- `Critical` (5): Critical failures
- `None` (6): No logging

### Q42: How do you configure logging providers?

**Answer:**
```csharp
builder.Logging.ClearProviders();
builder.Logging.AddConsole();
builder.Logging.AddDebug();
builder.Logging.AddEventLog();
builder.Logging.AddFile("logs/app.log"); // Requires Serilog or NLog

// appsettings.json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  }
}
```

---

## Error Handling

### Q43: How do you handle errors in ASP.NET Core?

**Answer:**
Multiple approaches:

**1. Developer Exception Page (Development):**
```csharp
if (app.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}
```

**2. Exception Handler Middleware:**
```csharp
app.UseExceptionHandler("/Error");
app.UseStatusCodePagesWithReExecute("/Error/{0}");
```

**3. Custom Exception Middleware:**
```csharp
public class ExceptionMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger<ExceptionMiddleware> _logger;

    public async Task InvokeAsync(HttpContext context)
    {
        try
        {
            await _next(context);
        }
        catch (Exception ex)
        {
            _logger.LogError(ex, "An error occurred");
            await HandleExceptionAsync(context, ex);
        }
    }

    private static Task HandleExceptionAsync(HttpContext context, Exception exception)
    {
        context.Response.StatusCode = (int)HttpStatusCode.InternalServerError;
        context.Response.ContentType = "application/json";
        
        var response = new { error = exception.Message };
        return context.Response.WriteAsJsonAsync(response);
    }
}
```

**4. Global Exception Filter:**
```csharp
public class GlobalExceptionFilter : IExceptionFilter
{
    public void OnException(ExceptionContext context)
    {
        // Handle exception
    }
}
```

### Q44: What is the difference between `UseExceptionHandler` and `UseDeveloperExceptionPage`?

**Answer:**

- **`UseDeveloperExceptionPage`**: Shows detailed error information (stack traces, query strings, cookies) - **Only for Development**
- **`UseExceptionHandler`**: Custom error handling for Production - shows user-friendly error pages

**Best Practice:**
```csharp
if (app.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}
else
{
    app.UseExceptionHandler("/Error");
    app.UseHsts();
}
```

---

## Caching

### Q45: What caching options are available in ASP.NET Core?

**Answer:**

1. **In-Memory Caching**: Stores data in server memory
   ```csharp
   services.AddMemoryCache();
   
   public class MyService
   {
       private readonly IMemoryCache _cache;
       
       public string GetData(string key)
       {
           if (!_cache.TryGetValue(key, out string value))
           {
               value = FetchFromDatabase();
               _cache.Set(key, value, TimeSpan.FromMinutes(5));
           }
           return value;
       }
   }
   ```

2. **Distributed Caching**: Redis, SQL Server, NCache
   ```csharp
   services.AddStackExchangeRedisCache(options =>
   {
       options.Configuration = "localhost:6379";
   });
   
   // Usage
   await _distributedCache.SetStringAsync(key, value);
   var cached = await _distributedCache.GetStringAsync(key);
   ```

3. **Response Caching**: Cache HTTP responses
   ```csharp
   services.AddResponseCaching();
   app.UseResponseCaching();
   
   [ResponseCache(Duration = 60)]
   public IActionResult GetData() { }
   ```

### Q46: Explain cache expiration strategies.

**Answer:**

- **Absolute Expiration**: Cache expires at a specific time
  ```csharp
  _cache.Set(key, value, DateTimeOffset.Now.AddMinutes(5));
  ```

- **Sliding Expiration**: Cache expires after period of inactivity
  ```csharp
  _cache.Set(key, value, new MemoryCacheEntryOptions
  {
      SlidingExpiration = TimeSpan.FromMinutes(5)
  });
  ```

- **Combined**: Expires when either condition is met
  ```csharp
  _cache.Set(key, value, new MemoryCacheEntryOptions
  {
      AbsoluteExpirationRelativeToNow = TimeSpan.FromHours(1),
      SlidingExpiration = TimeSpan.FromMinutes(10)
  });
  ```

---

## SignalR

### Q47: What is SignalR and when would you use it?

**Answer:**
SignalR is a library for adding real-time web functionality to ASP.NET Core applications. It enables:

- **Real-time communication**: Push data from server to client
- **WebSockets**: Automatic fallback to other transports
- **Bidirectional communication**: Both client and server can send messages

**Use Cases:**
- Chat applications
- Live notifications
- Real-time dashboards
- Collaborative editing
- Gaming applications

### Q48: How do you implement SignalR?

**Answer:**
```csharp
// Configure
services.AddSignalR();

app.MapHub<ChatHub>("/chathub");

// Hub
public class ChatHub : Hub
{
    public async Task SendMessage(string user, string message)
    {
        await Clients.All.SendAsync("ReceiveMessage", user, message);
    }

    public async Task JoinGroup(string groupName)
    {
        await Groups.AddToGroupAsync(Context.ConnectionId, groupName);
    }
}

// Client (JavaScript)
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/chathub")
    .build();

connection.on("ReceiveMessage", (user, message) => {
    // Handle message
});

connection.start();
```

---

## gRPC

### Q49: What is gRPC and how does it differ from REST?

**Answer:**
gRPC is a high-performance RPC framework using HTTP/2 and Protocol Buffers.

| Feature | REST | gRPC |
|---------|------|------|
| **Protocol** | HTTP/1.1 | HTTP/2 |
| **Data Format** | JSON/XML | Protocol Buffers (binary) |
| **Performance** | Good | Excellent |
| **Streaming** | Limited | Full support |
| **Browser Support** | Full | Limited (needs gRPC-Web) |

### Q50: How do you create a gRPC service in ASP.NET Core?

**Answer:**
```csharp
// Define service (.proto file)
syntax = "proto3";
service Greeter {
  rpc SayHello (HelloRequest) returns (HelloReply);
}

message HelloRequest {
  string name = 1;
}

message HelloReply {
  string message = 1;
}

// Implement service
public class GreeterService : Greeter.GreeterBase
{
    public override Task<HelloReply> SayHello(
        HelloRequest request, 
        ServerCallContext context)
    {
        return Task.FromResult(new HelloReply
        {
            Message = "Hello " + request.Name
        });
    }
}

// Register
app.MapGrpcService<GreeterService>();
```

---

## Docker and Containerization

### Q51: How do you containerize an ASP.NET Core application?

**Answer:**
```dockerfile
# Dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["MyApp.csproj", "./"]
RUN dotnet restore "MyApp.csproj"
COPY . .
RUN dotnet build "MyApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyApp.dll"]
```

**Build and run:**
```bash
docker build -t myapp .
docker run -p 8080:80 myapp
```

### Q52: What is multi-stage Docker build and why use it?

**Answer:**
Multi-stage builds use multiple `FROM` statements to:
- **Reduce image size**: Only include runtime dependencies
- **Separate build and runtime**: Build tools not included in final image
- **Optimize layers**: Better caching and smaller images

**Example:**
```dockerfile
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build  # Build stage
# ... build steps ...

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final  # Runtime stage
COPY --from=build /app/publish .  # Copy only built artifacts
```

---

## Deployment and DevOps

### Q53: How do you deploy ASP.NET Core applications?

**Answer:**
Multiple deployment options:

1. **Azure App Service**
   ```bash
   az webapp up --name myapp --resource-group mygroup
   ```

2. **AWS Elastic Beanstalk**
   - Package as ZIP and deploy

3. **Docker/Kubernetes**
   ```bash
   kubectl apply -f deployment.yaml
   ```

4. **IIS (Windows)**
   - Publish to folder
   - Configure IIS with ASP.NET Core Module

5. **Linux with Nginx**
   ```nginx
   server {
       listen 80;
       location / {
           proxy_pass http://localhost:5000;
       }
   }
   ```

### Q54: What is the difference between Framework-dependent and Self-contained deployments?

**Answer:**

- **Framework-dependent**: Requires .NET runtime on server
  - Smaller deployment package
  - Shared runtime
  - Command: `dotnet publish`

- **Self-contained**: Includes .NET runtime
  - Larger deployment package
  - No runtime required on server
  - Command: `dotnet publish -r win-x64 --self-contained true`

---

## Testing

### Q55: How do you write unit tests for ASP.NET Core applications?

**Answer:**
```csharp
// Using xUnit
public class UserServiceTests
{
    private readonly Mock<IUserRepository> _mockRepo;
    private readonly UserService _service;

    public UserServiceTests()
    {
        _mockRepo = new Mock<IUserRepository>();
        _service = new UserService(_mockRepo.Object);
    }

    [Fact]
    public void GetUser_ReturnsUser_WhenExists()
    {
        // Arrange
        var user = new User { Id = 1, Name = "Test" };
        _mockRepo.Setup(r => r.GetById(1)).Returns(user);

        // Act
        var result = _service.GetUser(1);

        // Assert
        Assert.NotNull(result);
        Assert.Equal("Test", result.Name);
    }
}
```

### Q56: How do you write integration tests?

**Answer:**
```csharp
public class UsersControllerTests : IClassFixture<WebApplicationFactory<Program>>
{
    private readonly WebApplicationFactory<Program> _factory;
    private readonly HttpClient _client;

    public UsersControllerTests(WebApplicationFactory<Program> factory)
    {
        _factory = factory;
        _client = _factory.CreateClient();
    }

    [Fact]
    public async Task GetUsers_ReturnsSuccessStatusCode()
    {
        // Act
        var response = await _client.GetAsync("/api/users");

        // Assert
        response.EnsureSuccessStatusCode();
        var content = await response.Content.ReadAsStringAsync();
        Assert.Contains("users", content);
    }
}
```

---

## Performance Optimization

### Q57: What are common performance optimization techniques?

**Answer:**

1. **Async/Await**: Non-blocking I/O operations
   ```csharp
   public async Task<IActionResult> GetUsers()
   {
       var users = await _userService.GetAllAsync();
       return Ok(users);
   }
   ```

2. **Response Compression**: Reduce payload size
   ```csharp
   services.AddResponseCompression();
   app.UseResponseCompression();
   ```

3. **Response Caching**: Cache responses
   ```csharp
   [ResponseCache(Duration = 60)]
   public IActionResult GetData() { }
   ```

4. **Database Optimization**:
   - Use `AsNoTracking()` for read-only queries
   - Use projections to select only needed fields
   - Implement pagination
   - Use compiled queries

5. **Connection Pooling**: Reuse database connections

6. **Minification and Bundling**: Reduce asset sizes

### Q58: How do you profile and monitor ASP.NET Core applications?

**Answer:**

1. **Application Insights** (Azure)
   ```csharp
   services.AddApplicationInsightsTelemetry();
   ```

2. **Performance Counters**: Built-in metrics

3. **Logging**: Structured logging with correlation IDs

4. **Health Checks**: Monitor application health
   ```csharp
   services.AddHealthChecks()
       .AddDbContextCheck<ApplicationDbContext>();
   
   app.MapHealthChecks("/health");
   ```

5. **MiniProfiler**: Real-time profiling
   ```csharp
   services.AddMiniProfiler();
   app.UseMiniProfiler();
   ```

---

## Blazor

### Q59: What is Blazor and what are its hosting models?

**Answer:**
Blazor is a framework for building interactive client-side web UI with .NET instead of JavaScript.

**Hosting Models:**

1. **Blazor Server**: Runs on server, UI updates via SignalR
   - Fast initial load
   - Requires constant connection
   - Lower client resources

2. **Blazor WebAssembly**: Runs in browser via WebAssembly
   - Works offline
   - Full .NET in browser
   - Larger initial download

3. **Blazor Hybrid**: Native apps (MAUI, WPF, WinForms)
   - Desktop/mobile apps
   - Native performance

### Q60: How do you create a Blazor component?

**Answer:**
```razor
@* Counter.razor *@
@page "/counter"

<h1>Counter</h1>
<p>Current count: @currentCount</p>

<button class="btn btn-primary" @onclick="IncrementCount">Click me</button>

@code {
    private int currentCount = 0;

    private void IncrementCount()
    {
        currentCount++;
    }
}
```

---

## Additional Important Topics

### Q61: What is the difference between `AddControllers()` and `AddMvc()`?

**Answer:**

- **`AddControllers()`**: Adds only controller services (for APIs)
  - Lighter weight
  - No view engine support
  - Use for Web APIs

- **`AddMvc()`**: Adds full MVC stack
  - Includes controllers, views, Razor Pages
  - Heavier
  - Use for MVC applications

### Q62: How do you implement health checks?

**Answer:**
```csharp
// Configure
services.AddHealthChecks()
    .AddDbContextCheck<ApplicationDbContext>()
    .AddCheck<CustomHealthCheck>("custom")
    .AddRedis("connectionString");

// Endpoint
app.MapHealthChecks("/health", new HealthCheckOptions
{
    ResponseWriter = UIResponseWriter.WriteHealthCheckUIResponse
});

// Custom health check
public class CustomHealthCheck : IHealthCheck
{
    public Task<HealthCheckResult> CheckHealthAsync(
        HealthCheckContext context,
        CancellationToken cancellationToken = default)
    {
        // Check logic
        return Task.FromResult(HealthCheckResult.Healthy());
    }
}
```

### Q63: What is the difference between `IHost` and `IWebHost`?

**Answer:**

- **`IHost`**: Generic host (ASP.NET Core 3.0+)
  - Can host any type of application
  - More flexible
  - Recommended for new applications

- **`IWebHost`**: Web-specific host (legacy)
  - Only for web applications
  - Deprecated in favor of `IHost`

### Q64: How do you implement rate limiting?

**Answer:**
```csharp
// Install: Microsoft.AspNetCore.RateLimiting

services.AddRateLimiter(options =>
{
    options.AddFixedWindowLimiter("fixed", opt =>
    {
        opt.Window = TimeSpan.FromSeconds(10);
        opt.PermitLimit = 2;
    });
});

app.UseRateLimiter();

// Apply to endpoint
[EnableRateLimiting("fixed")]
[HttpGet]
public IActionResult GetData() { }
```

### Q65: What is the purpose of `appsettings.json` and `appsettings.{Environment}.json`?

**Answer:**

- **`appsettings.json`**: Base configuration for all environments
- **`appsettings.Development.json`**: Development-specific overrides
- **`appsettings.Production.json`**: Production-specific overrides

Configuration is merged, with environment-specific files taking precedence.

---

## Conclusion

This comprehensive guide covers the essential topics from the ASP.NET Core Developer Roadmap. These questions and answers should help you prepare for ASP.NET Core interviews at various levels, from junior to senior positions.

**Key Areas to Focus On:**
- Middleware pipeline and execution order
- Dependency Injection and service lifetimes
- Entity Framework Core and database operations
- Authentication and Authorization
- Web API development
- Performance optimization
- Testing strategies

**Resources:**
- [Official ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core)
- [ASP.NET Core Roadmap](https://roadmap.sh/aspnet-core)
- [.NET Documentation](https://docs.microsoft.com/dotnet)

---

*Last Updated: 2025*

