# C# Core & Advanced Exercises – Interview Q&A

## 1. Collections & LINQ

### 1. Remove duplicate objects from a list based on multiple properties
**Answer:**
```csharp
var uniqueList = list.GroupBy(x => new { x.Prop1, x.Prop2 })
                     .Select(g => g.First())
                     .ToList();
```
**Sample Data:**
List of `Person` objects:
- { FirstName = "John", LastName = "Doe", Age = 30 }
- { FirstName = "Jane", LastName = "Smith", Age = 25 }
- { FirstName = "John", LastName = "Doe", Age = 40 }
Remove duplicates where both `FirstName` and `LastName` are the same.

### 2. Group employees by department and calculate average salary per department
**Answer:**
```csharp
var avgSalaries = employees
    .GroupBy(e => e.Department)
    .Select(g => new { Department = g.Key, AvgSalary = g.Average(e => e.Salary) });
```
**Sample Data:**
List of `Employee` objects:
- { Name = "Alice", Department = "HR", Salary = 50000 }
- { Name = "Bob", Department = "IT", Salary = 60000 }
- { Name = "Carol", Department = "HR", Salary = 55000 }
Group by department and show average salary.

### 3. Find top 3 customers by total purchase value
**Answer:**
```csharp
var topCustomers = orders
    .GroupBy(o => o.CustomerId)
    .Select(g => new { CustomerId = g.Key, Total = g.Sum(o => o.Value) })
    .OrderByDescending(x => x.Total)
    .Take(3);
```
**Sample Data:**
List of `Order` objects:
- { CustomerId = 1, Value = 100 }
- { CustomerId = 2, Value = 200 }
- { CustomerId = 1, Value = 150 }
- { CustomerId = 3, Value = 300 }
- { CustomerId = 2, Value = 50 }
Find top 3 customers by total purchase value.

### 4. Find missing numbers in a sequence from 1 to N
**Answer:**
```csharp
var missing = Enumerable.Range(1, N).Except(numbers);
```
**Sample Data:**
Given `numbers = [1, 2, 4, 6, 7]`, `N = 7`.
Find missing numbers.

### 5. Convert a list to a dictionary with composite key (Country + City)
**Answer:**
```csharp
var dict = list.ToDictionary(x => (x.Country, x.City));
```
**Sample Data:**
List of `Location` objects:
- { Country = "US", City = "NY" }
- { Country = "US", City = "LA" }
- { Country = "IN", City = "Mumbai" }
Convert to dictionary with (Country, City) as key.

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
**Sample Data:**
Provide 3 text files:
- file1.txt (10 lines)
- file2.txt (20 lines)
- file3.txt (15 lines)
Return total line count using async.

### 7. Convert a synchronous method to async/await without changing signature
**Answer:**
```csharp
public async Task<int> GetDataAsync()
{
    return await Task.Run(() => GetData());
}
```
**Sample Data:**
Given:
```csharp
public int GetData() { return 42; }
```
Wrap this in an async method.

### 8. Demonstrate a deadlock scenario using Task.Result or .Wait()
**Answer:**
```csharp
// UI thread calls:
var result = SomeAsync().Result; // Deadlock if SomeAsync awaits
```
**Sample Data:**
Show code that causes a deadlock in a UI app using `.Result` or `.Wait()`.

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
**Sample Data:**
Write a method that retries a failing HTTP call up to 3 times with exponential backoff.

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
**Sample Data:**
Write a method that processes 1000 items, but can be cancelled.

## 3. OOP & Design

### 11. Class structure for payment system with multiple providers
**Answer:**
```csharp
interface IPaymentProvider { void Pay(decimal amount); }
class Paypal : IPaymentProvider { public void Pay(decimal a) { /*...*/ } }
class Stripe : IPaymentProvider { public void Pay(decimal a) { /*...*/ } }
class PaymentService { public void Process(IPaymentProvider p, decimal a) => p.Pay(a); }
```
**Sample Data:**
Suppose you have to support Paypal and Stripe. Show how you would process a payment of $100 using both providers.

### 12. Refactor class violating Single Responsibility Principle
**Answer:**
```csharp
// Before: class handles data and logging
class Order { void Save() { /*...*/ } void Log() { /*...*/ } }
// After: separate classes
class Order { void Save() { /*...*/ } }
class Logger { void Log(string msg) { /*...*/ } }
```
**Sample Data:**
Given a class that saves orders and logs to file, refactor to follow SRP.

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
**Sample Data:**
Show how to create and send both Email and SMS notifications using the factory.

### 14. Method overloading vs overriding
**Answer:**
```csharp
class Base { public virtual void Foo() { } }
class Derived : Base { public override void Foo() { } }
class Overload { public void Bar(int x) { } public void Bar(string y) { } }
```
**Sample Data:**
Show an example where you override a method in a derived class and overload a method in the same class.

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
**Sample Data:**
Create a `Person` with name "John" and age 30. Try to set age to -1 and handle the exception.

## 4. Memory & Performance

### 16. Program causing memory leak and fix
**Answer:**
```csharp
// Leak: static event handler prevents GC
static event EventHandler MyEvent;
// Fix: Unsubscribe when done
MyEvent -= handler;
```
**Sample Data:**
Show a scenario where a static event handler causes a memory leak and how to fix it.

### 17. Difference between struct and class
**Answer:**
- Struct: value type, stored on stack, no inheritance.
- Class: reference type, stored on heap, supports inheritance.
**Sample Data:**
Define a struct `Point` and a class `Person`. Show how assignment differs for each.

### 18. Optimize loop processing 1 million records
**Answer:**
- Use parallelism: `Parallel.ForEach(records, r => Process(r));`
- Avoid unnecessary allocations.
**Sample Data:**
Given a list of 1 million integers, process them in parallel and measure time taken.

### 19. Span<T> or ReadOnlySpan<T> for performance
**Answer:**
```csharp
ReadOnlySpan<byte> span = new ReadOnlySpan<byte>(data);
// No allocations, fast slicing
```
**Sample Data:**
Given a byte array, use `ReadOnlySpan<byte>` to slice the first 10 bytes without allocation.

### 20. Boxing and unboxing example
**Answer:**
```csharp
object boxed = 123; // boxing
int unboxed = (int)boxed; // unboxing
```
**Sample Data:**
Box an integer, then unbox it and add 10.

## 5. Exception Handling & Logging

### 21. Global exception handler for console/web app
**Answer:**
- Console: `AppDomain.CurrentDomain.UnhandledException += ...`
- Web: Use middleware for exception handling.
**Sample Data:**
Show how to catch all unhandled exceptions in a console app.

### 22. Custom exceptions and usage
**Answer:**
```csharp
class MyException : Exception { }
throw new MyException();
```
**Sample Data:**
Define a custom exception and throw it when a value is negative.

### 23. Handle multiple exceptions in single catch
**Answer:**
```csharp
catch (Exception ex) when (ex is IOException || ex is SocketException) { }
```
**Sample Data:**
Show a try-catch block that handles both IO and Socket exceptions.

### 24. Log exceptions asynchronously
**Answer:**
```csharp
async Task LogAsync(Exception ex) => await File.WriteAllTextAsync("log.txt", ex.ToString());
```
**Sample Data:**
Write a method that logs exceptions to a file asynchronously.

### 25. Improper exception handling can crash app
**Answer:**
- Swallowing exceptions or not handling them at all can terminate the process.
**Sample Data:**
Show code where an unhandled exception crashes the app, and then fix it.

## 6. Web API Fundamentals

### 26. REST API with CRUD for Product
**Answer:**
- Use ASP.NET Core Controller with [HttpGet], [HttpPost], [HttpPut], [HttpDelete] actions.
**Sample Data:**
Design a Product API with endpoints to create, read, update, and delete products.

### 27. API versioning without breaking clients
**Answer:**
- Use URL versioning: `/api/v1/products`
- Use Microsoft.AspNetCore.Mvc.Versioning package.
**Sample Data:**
Show how to version an API so that both v1 and v2 endpoints are available.

### 28. Return proper HTTP status codes
**Answer:**
- 404 for not found, 400 for bad request, 500 for server error, 200 for success, 201 for created.
**Sample Data:**
Show controller actions returning 200, 201, 400, 404, and 500 status codes.

### 29. API endpoint with filtering, sorting, pagination
**Answer:**
- Accept query params: `?filter=...&sort=...&page=...&size=...`
- Use LINQ to filter, sort, and paginate.
**Sample Data:**
Design an endpoint for products that supports filtering by name, sorting by price, and pagination.

### 30. Secure endpoint for authenticated users
**Answer:**
- Use `[Authorize]` attribute in ASP.NET Core.
**Sample Data:**
Show a controller with an endpoint that only authenticated users can access.

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
**Sample Data:**
Write middleware that logs the time taken for each HTTP request.

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
**Sample Data:**
Create an action filter that checks for a custom header and returns 400 if missing.

### 33. Global exception handling using middleware
**Answer:**
- Use `app.UseMiddleware<ExceptionMiddleware>()` in Startup.
**Sample Data:**
Show how to register and use global exception handling middleware.

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
**Sample Data:**
Write middleware that blocks requests from IP 1.2.3.4.

### 35. Middleware vs filters real use case
**Answer:**
- Middleware: cross-cutting concerns (logging, auth)
- Filters: action/controller-specific logic (validation)
**Sample Data:**
Give an example where you would use middleware and another where you would use a filter.

## 8. Dependency Injection

### 36. Register services with different lifetimes
**Answer:**
- Singleton: `services.AddSingleton<T>()`
- Scoped: `services.AddScoped<T>()`
- Transient: `services.AddTransient<T>()`
**Sample Data:**
Show how to register and resolve singleton, scoped, and transient services in Startup.cs.

### 37. Fix circular dependency issue
**Answer:**
- Refactor to remove direct dependency, use interfaces or events.
**Sample Data:**
Given two services that depend on each other, refactor to remove the circular dependency.

### 38. Inject service conditionally by environment
**Answer:**
```csharp
if (env.IsDevelopment()) services.AddSingleton<IMy, DevMy>();
else services.AddSingleton<IMy, ProdMy>();
```
**Sample Data:**
Show how to inject a mock service in development and a real service in production.

### 39. Replace concrete class with interface
**Answer:**
- Register interface: `services.AddScoped<IMy, MyImpl>()`
- Use `IMy` in constructor.
**Sample Data:**
Refactor code to use an interface instead of a concrete class for dependency injection.

### 40. Mock dependency for unit testing
**Answer:**
- Use Moq: `var mock = new Mock<IMy>();`
**Sample Data:**
Write a unit test that mocks a dependency using Moq.

## 9. Authentication & Authorization

### 41. JWT-based authentication
**Answer:**
- Use Microsoft.AspNetCore.Authentication.JwtBearer
- Configure in Startup, add `[Authorize]`.
**Sample Data:**
Show how to configure JWT authentication and protect an endpoint.

### 42. Restrict access using roles/policies
**Answer:**
- Use `[Authorize(Roles = "Admin")]` or policies.
**Sample Data:**
Show a controller with endpoints restricted to Admin and User roles.

### 43. Refresh JWT tokens securely
**Answer:**
- Use refresh tokens, validate and issue new JWT.
**Sample Data:**
Show how to implement a refresh token endpoint.

### 44. Protect APIs from CSRF
**Answer:**
- Use anti-forgery tokens, validate on POST/PUT/DELETE.
**Sample Data:**
Show how to add and validate anti-forgery tokens in a POST endpoint.

### 45. Role-based access for admin/user endpoints
**Answer:**
- Use `[Authorize(Roles = "Admin")]` for admin, `[Authorize(Roles = "User")]` for users.
**Sample Data:**
Show endpoints for admin and user, each protected by their respective roles.

## 10. Database & EF Core

### 46. EF Core entities for blog system
**Answer:**
```csharp
class Blog { public int Id; public string Title; public List<Post> Posts; }
class Post { public int Id; public string Content; public int BlogId; public Blog Blog; }
```
**Sample Data:**
Design entities for a blog with multiple posts, and show how to add a post to a blog.

### 47. LINQ query that translates efficiently to SQL
**Answer:**
- Use only supported LINQ methods, avoid client-side evaluation.
**Sample Data:**
Write a LINQ query that filters and orders products, and explain why it runs efficiently in SQL.

### 48. Handle concurrency conflicts in EF Core
**Answer:**
- Use RowVersion property, catch DbUpdateConcurrencyException.
**Sample Data:**
Show how to handle a concurrency conflict when two users update the same record.

### 49. Soft delete using global query filters
**Answer:**
- Add `IsDeleted` property, use `modelBuilder.Entity<T>().HasQueryFilter(x => !x.IsDeleted)`.
**Sample Data:**
Show how to implement soft delete for an entity and filter out deleted records.

### 50. Optimize N+1 query issues
**Answer:**
- Use `.Include()` to eager load related data.
**Sample Data:**
Show how to use `.Include()` to load related data and avoid N+1 queries.

## 11. Testing & Dev Practices

### 51. Unit tests for a service using xUnit
**Answer:**
```csharp
[Fact]
public void TestMethod() { Assert.Equal(4, 2+2); }
```
**Sample Data:**
Write a unit test for a service that adds two numbers.

### 52. Mock database calls using in-memory provider
**Answer:**
- Use `UseInMemoryDatabase` with EF Core.
**Sample Data:**
Show how to use the in-memory provider to test a repository method.

### 53. Integration test for a controller
**Answer:**
- Use TestServer/WebApplicationFactory in ASP.NET Core.
**Sample Data:**
Write an integration test for a ProductController that tests the GET endpoint.

### 54. Test async methods correctly
**Answer:**
- Use `await` in test, mark test as `async Task`.
**Sample Data:**
Write an async unit test for a method that returns a Task.

### 55. What should NOT be unit tested
**Answer:**
- External dependencies, framework code, trivial getters/setters.
**Sample Data:**
List examples of code that should not be unit tested.

## 12. System Design (ASP.NET Core Focus)

### 56. Design a high-traffic API (1M req/day)
**Answer:**
- Use load balancers, stateless services, caching, horizontal scaling.
**Sample Data:**
Describe an architecture for an API that handles 1 million requests per day.

### 57. Handle rate limiting for public APIs
**Answer:**
- Use middleware or API gateway for rate limiting.
**Sample Data:**
Show how to implement rate limiting middleware for an API.

### 58. Caching using MemoryCache or Redis
**Answer:**
- Use IMemoryCache for in-memory, StackExchange.Redis for distributed.
**Sample Data:**
Show how to cache product data using IMemoryCache and Redis.

### 59. Background job using IHostedService
**Answer:**
- Implement IHostedService, register in DI.
**Sample Data:**
Write a background service that runs every minute and logs a message.

### 60. Scale ASP.NET Core app horizontally
**Answer:**
- Deploy multiple instances, use shared cache/db, stateless design.
**Sample Data:**
Explain how to scale an ASP.NET Core app to handle more traffic.

## 13. Real-World Scenarios

### 61. Debugging a slow deployed API
**Answer:**
- Use logging, profiling, Application Insights, check DB, analyze bottlenecks.
**Sample Data:**
Describe steps to debug a slow API in production.

### 62. Handling update conflicts
**Answer:**
- Use optimistic concurrency, RowVersion, handle DbUpdateConcurrencyException.
**Sample Data:**
Show how to handle update conflicts in EF Core when two users edit the same record.

### 63. API works locally but fails in production
**Answer:**
- Check config, environment variables, connection strings, logs.
**Sample Data:**
List possible reasons why an API works locally but fails after deployment.

### 64. Large file upload fails intermittently
**Answer:**
- Increase request size limits, check network, use streaming upload.
**Sample Data:**
Show how to configure ASP.NET Core to support large file uploads.

### 65. Database is down – API behavior
**Answer:**
- Return 503 Service Unavailable, log error, retry or fallback if possible.
**Sample Data:**
Show how to handle and return a 503 error when the database is unavailable.
