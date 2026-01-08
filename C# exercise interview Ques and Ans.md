# C# Core & Advanced Exercises – Interview Q&A

## 1. Collections & LINQ

### 1. Remove duplicate objects from a list based on multiple properties
**Answer:**
```csharp
var uniqueList = list.GroupBy(x => new { x.Prop1, x.Prop2 })
                     .Select(g => g.First())
                     .ToList();
```

### 2. Group employees by department and calculate average salary per department
**Answer:**
```csharp
var avgSalaries = employees
    .GroupBy(e => e.Department)
    .Select(g => new { Department = g.Key, AvgSalary = g.Average(e => e.Salary) });
```

### 3. Find top 3 customers by total purchase value
**Answer:**
```csharp
var topCustomers = orders
    .GroupBy(o => o.CustomerId)
    .Select(g => new { CustomerId = g.Key, Total = g.Sum(o => o.Value) })
    .OrderByDescending(x => x.Total)
    .Take(3);
```

### 4. Find missing numbers in a sequence from 1 to N
**Answer:**
```csharp
var missing = Enumerable.Range(1, N).Except(numbers);
```

### 5. Convert a list to a dictionary with composite key (Country + City)
**Answer:**
```csharp
var dict = list.ToDictionary(x => (x.Country, x.City));
```

## 2. Asynchronous Programming

### 6. Read multiple files concurrently and return total line count
**Answer:**
```csharp
async Task<int> TotalLinesAsync(IEnumerable<string> files)
{
    var tasks = files.Select(async f => (await File.ReadAllLinesAsync(f)).Length);
    var results = await Task.WhenAll(tasks);
    return results.Sum();
}
```

### 7. Convert a synchronous method to async/await without changing signature
**Answer:**
```csharp
public async Task<int> GetDataAsync()
{
    return await Task.Run(() => GetData());
}
```

### 8. Demonstrate a deadlock scenario using Task.Result or .Wait()
**Answer:**
```csharp
// UI thread calls:
var result = SomeAsync().Result; // Deadlock if SomeAsync awaits
```

### 9. Retry logic with exponential backoff using async/await
**Answer:**
```csharp
async Task<T> RetryAsync<T>(Func<Task<T>> action, int maxAttempts)
{
    int delay = 1000;
    for (int i = 0; i < maxAttempts; i++)
    {
        try { return await action(); }
        catch when (i < maxAttempts - 1) { await Task.Delay(delay); delay *= 2; }
    }
    throw new Exception("Failed after retries");
}
```

### 10. Cancel a long-running task using CancellationToken
**Answer:**
```csharp
async Task LongTask(CancellationToken token)
{
    for (int i = 0; i < 1000; i++)
    {
        token.ThrowIfCancellationRequested();
        await Task.Delay(100, token);
    }
}
```

## 3. OOP & Design

### 11. Class structure for payment system with multiple providers
**Answer:**
```csharp
interface IPaymentProvider { void Pay(decimal amount); }
class Paypal : IPaymentProvider { public void Pay(decimal a) { /*...*/ } }
class Stripe : IPaymentProvider { public void Pay(decimal a) { /*...*/ } }
class PaymentService { public void Process(IPaymentProvider p, decimal a) => p.Pay(a); }
```

### 12. Refactor class violating Single Responsibility Principle
**Answer:**
```csharp
// Before: class handles data and logging
class Order { void Save() { /*...*/ } void Log() { /*...*/ } }
// After: separate classes
class Order { void Save() { /*...*/ } }
class Logger { void Log(string msg) { /*...*/ } }
```

### 13. Factory pattern for notification types
**Answer:**
```csharp
interface INotification { void Send(); }
class Email : INotification { public void Send() { /*...*/ } }
class Sms : INotification { public void Send() { /*...*/ } }
class NotificationFactory {
    public static INotification Create(string type) => type switch {
        "email" => new Email(),
        "sms" => new Sms(),
        _ => throw new NotImplementedException()
    };
}
```

### 14. Method overloading vs overriding
**Answer:**
```csharp
class Base { public virtual void Foo() { } }
class Derived : Base { public override void Foo() { } }
class Overload { public void Bar(int x) { } public void Bar(string y) { } }
```

### 15. Immutable class with validation
**Answer:**
```csharp
class Person {
    public string Name { get; }
    public int Age { get; }
    public Person(string name, int age) {
        if (age < 0) throw new ArgumentException();
        Name = name; Age = age;
    }
}
```

## 4. Memory & Performance

### 16. Program causing memory leak and fix
**Answer:**
```csharp
// Leak: static event handler prevents GC
static event EventHandler MyEvent;
// Fix: Unsubscribe when done
MyEvent -= handler;
```

### 17. Difference between struct and class
**Answer:**
- Struct: value type, stored on stack, no inheritance.
- Class: reference type, stored on heap, supports inheritance.

### 18. Optimize loop processing 1 million records
**Answer:**
- Use parallelism: `Parallel.ForEach(records, r => Process(r));`
- Avoid unnecessary allocations.

### 19. Span<T> or ReadOnlySpan<T> for performance
**Answer:**
```csharp
ReadOnlySpan<byte> span = new ReadOnlySpan<byte>(data);
// No allocations, fast slicing
```

### 20. Boxing and unboxing example
**Answer:**
```csharp
object boxed = 123; // boxing
int unboxed = (int)boxed; // unboxing
```

## 5. Exception Handling & Logging

### 21. Global exception handler for console/web app
**Answer:**
- Console: `AppDomain.CurrentDomain.UnhandledException += ...`
- Web: Use middleware for exception handling.

### 22. Custom exceptions and usage
**Answer:**
```csharp
class MyException : Exception { }
throw new MyException();
```

### 23. Handle multiple exceptions in single catch
**Answer:**
```csharp
catch (Exception ex) when (ex is IOException || ex is SocketException) { }
```

### 24. Log exceptions asynchronously
**Answer:**
```csharp
async Task LogAsync(Exception ex) => await File.WriteAllTextAsync("log.txt", ex.ToString());
```

### 25. Improper exception handling can crash app
**Answer:**
- Swallowing exceptions or not handling them at all can terminate the process.

## 6. Web API Fundamentals

### 26. REST API with CRUD for Product
**Answer:**
- Use ASP.NET Core Controller with [HttpGet], [HttpPost], [HttpPut], [HttpDelete] actions.

### 27. API versioning without breaking clients
**Answer:**
- Use URL versioning: `/api/v1/products`
- Use Microsoft.AspNetCore.Mvc.Versioning package.

### 28. Return proper HTTP status codes
**Answer:**
- 404 for not found, 400 for bad request, 500 for server error, 200 for success, 201 for created.

### 29. API endpoint with filtering, sorting, pagination
**Answer:**
- Accept query params: `?filter=...&sort=...&page=...&size=...`
- Use LINQ to filter, sort, and paginate.

### 30. Secure endpoint for authenticated users
**Answer:**
- Use `[Authorize]` attribute in ASP.NET Core.

## 7. Middleware & Filters

### 31. Custom middleware to log request/response time
**Answer:**
```csharp
public async Task Invoke(HttpContext ctx) {
    var sw = Stopwatch.StartNew();
    await _next(ctx);
    sw.Stop();
    Console.WriteLine($"Time: {sw.Elapsed}");
}
```

### 32. Action filter to validate request headers
**Answer:**
```csharp
public class HeaderValidation : ActionFilterAttribute {
    public override void OnActionExecuting(ActionExecutingContext ctx) {
        if (!ctx.HttpContext.Request.Headers.ContainsKey("X-MyHeader"))
            ctx.Result = new BadRequestResult();
    }
}
```

### 33. Global exception handling using middleware
**Answer:**
- Use `app.UseMiddleware<ExceptionMiddleware>()` in Startup.

### 34. Block requests from specific IP using middleware
**Answer:**
```csharp
public async Task Invoke(HttpContext ctx) {
    if (ctx.Connection.RemoteIpAddress.ToString() == "1.2.3.4")
        ctx.Response.StatusCode = 403;
    else
        await _next(ctx);
}
```

### 35. Middleware vs filters real use case
**Answer:**
- Middleware: cross-cutting concerns (logging, auth)
- Filters: action/controller-specific logic (validation)

## 8. Dependency Injection

### 36. Register services with different lifetimes
**Answer:**
- Singleton: `services.AddSingleton<T>()`
- Scoped: `services.AddScoped<T>()`
- Transient: `services.AddTransient<T>()`

### 37. Fix circular dependency issue
**Answer:**
- Refactor to remove direct dependency, use interfaces or events.

### 38. Inject service conditionally by environment
**Answer:**
```csharp
if (env.IsDevelopment()) services.AddSingleton<IMy, DevMy>();
else services.AddSingleton<IMy, ProdMy>();
```

### 39. Replace concrete class with interface
**Answer:**
- Register interface: `services.AddScoped<IMy, MyImpl>()`
- Use `IMy` in constructor.

### 40. Mock dependency for unit testing
**Answer:**
- Use Moq: `var mock = new Mock<IMy>();`

## 9. Authentication & Authorization

### 41. JWT-based authentication
**Answer:**
- Use Microsoft.AspNetCore.Authentication.JwtBearer
- Configure in Startup, add `[Authorize]`.

### 42. Restrict access using roles/policies
**Answer:**
- Use `[Authorize(Roles = "Admin")]` or policies.

### 43. Refresh JWT tokens securely
**Answer:**
- Use refresh tokens, validate and issue new JWT.

### 44. Protect APIs from CSRF
**Answer:**
- Use anti-forgery tokens, validate on POST/PUT/DELETE.

### 45. Role-based access for admin/user endpoints
**Answer:**
- Use `[Authorize(Roles = "Admin")]` for admin, `[Authorize(Roles = "User")]` for users.

## 10. Database & EF Core

### 46. EF Core entities for blog system
**Answer:**
```csharp
class Blog { public int Id; public string Title; public List<Post> Posts; }
class Post { public int Id; public string Content; public int BlogId; public Blog Blog; }
```

### 47. LINQ query that translates efficiently to SQL
**Answer:**
- Use only supported LINQ methods, avoid client-side evaluation.

### 48. Handle concurrency conflicts in EF Core
**Answer:**
- Use RowVersion property, catch DbUpdateConcurrencyException.

### 49. Soft delete using global query filters
**Answer:**
- Add `IsDeleted` property, use `modelBuilder.Entity<T>().HasQueryFilter(x => !x.IsDeleted)`.

### 50. Optimize N+1 query issues
**Answer:**
- Use `.Include()` to eager load related data.

## 11. Testing & Dev Practices

### 51. Unit tests for a service using xUnit
**Answer:**
```csharp
[Fact]
public void TestMethod() { Assert.Equal(4, 2+2); }
```

### 52. Mock database calls using in-memory provider
**Answer:**
- Use `UseInMemoryDatabase` with EF Core.

### 53. Integration test for a controller
**Answer:**
- Use TestServer/WebApplicationFactory in ASP.NET Core.

### 54. Test async methods correctly
**Answer:**
- Use `await` in test, mark test as `async Task`.

### 55. What should NOT be unit tested
**Answer:**
- External dependencies, framework code, trivial getters/setters.

## 12. System Design (ASP.NET Core Focus)

### 56. Design a high-traffic API (1M req/day)
**Answer:**
- Use load balancers, stateless services, caching, horizontal scaling.

### 57. Handle rate limiting for public APIs
**Answer:**
- Use middleware or API gateway for rate limiting.

### 58. Caching using MemoryCache or Redis
**Answer:**
- Use IMemoryCache for in-memory, StackExchange.Redis for distributed.

### 59. Background job using IHostedService
**Answer:**
- Implement IHostedService, register in DI.

### 60. Scale ASP.NET Core app horizontally
**Answer:**
- Deploy multiple instances, use shared cache/db, stateless design.

## 13. Real-World Scenarios

### 61. Debugging a slow deployed API
**Answer:**
- Use logging, profiling, Application Insights, check DB, analyze bottlenecks.

### 62. Handling update conflicts
**Answer:**
- Use optimistic concurrency, RowVersion, handle DbUpdateConcurrencyException.

### 63. API works locally but fails in production
**Answer:**
- Check config, environment variables, connection strings, logs.

### 64. Large file upload fails intermittently
**Answer:**
- Increase request size limits, check network, use streaming upload.

### 65. Database is down – API behavior
**Answer:**
- Return 503 Service Unavailable, log error, retry or fallback if possible.
