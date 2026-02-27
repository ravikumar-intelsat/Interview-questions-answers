past c# interview questions:
write a program read multiple files concurrently 
how to delete duplicate rows from db
what is diffeence between IEnumerable and IQuearable
what is optimizations techniques in C#
what is cte
what is rank, dense
what si content type and access headers
what is diamond pattern


https://api.github.com/users


101	Ravi	ravi@mail.com
	50000
102	Ravi	ravi@mail.com
	52000
103	Anil	anil@mail.com
	40000
104	Anil	anil@mail.com
	40000


  public interface ISettingService
{
	Task Send(string message);
}
public class SettingService : ISettingService
{
   public SettingService(string applicationId)
   {
   }
  public async Task Send(string message)
  {
    throw new NotImplementedException();
  }	
} 

app.services.addTransient(SettingService,ISettingService)


public interface INotification

{

	Task SendEmail(string toEmail, string subject, string body);

	Task Send(string message);

}

public class EmailNotification : INotification

{

	public async Task SendEmail(string toEmail, string subject, string body)

	{

		await Task.CompletedTask;

	}

	public async Task Send(string message)

	{

		throw new NotImplementedException();

	}

}

public class MessageNotification : INotification

{

	public async Task SendEmail(string toEmail, string subject, string body)

	{

		throw new NotImplementedException();

	}

	public async Task Send(string message)

	{

		await Task.CompletedTask;

	}

}
Got it 👍 — no interface split, keep INotification exactly as you wrote it.
Here are clean, real-world DI ways to register and consume it.

✅ Option 1: Factory-based DI (BEST & works in all .NET versions)
1️⃣ Keep your code as-is

(No changes to interface or classes)

public interface INotification
{
    Task SendEmail(string toEmail, string subject, string body);
    Task Send(string message);
}
2️⃣ Register services + factory

Program.cs

builder.Services.AddScoped<EmailNotification>();
builder.Services.AddScoped<MessageNotification>();

builder.Services.AddScoped<Func<string, INotification>>(sp => key =>
{
    return key switch
    {
        "email" => sp.GetRequiredService<EmailNotification>(),
        "message" => sp.GetRequiredService<MessageNotification>(),
        _ => throw new ArgumentException("Invalid notification type")
    };
});
3️⃣ Consume using DI
public class NotificationService
{
    private readonly Func<string, INotification> _notificationFactory;

    public NotificationService(Func<string, INotification> notificationFactory)
    {
        _notificationFactory = notificationFactory;
    }

    public async Task SendNotifications()
    {
        var email = _notificationFactory("email");
        await email.SendEmail("test@mail.com", "Hello", "Body");

        var message = _notificationFactory("message");
        await message.Send("Hello via message");
    }
}

✔ No interface split
✔ No service locator
✔ Fully DI-friendly

✅ Option 2: Keyed Services (.NET 8+ ONLY – cleaner)

If you’re on .NET 8, this is 🔥.

1️⃣ Register keyed services
builder.Services.AddKeyedScoped<INotification, EmailNotification>("email");
builder.Services.AddKeyedScoped<INotification, MessageNotification>("message");
2️⃣ Consume using [FromKeyedServices]
public class NotificationService
{
    private readonly INotification _emailNotification;
    private readonly INotification _messageNotification;

    public NotificationService(
        [FromKeyedServices("email")] INotification emailNotification,
        [FromKeyedServices("message")] INotification messageNotification)
    {
        _emailNotification = emailNotification;
        _messageNotification = messageNotification;
    }

    public async Task Notify()
    {
        await _emailNotification.SendEmail("a@b.com", "Hi", "Body");
        await _messageNotification.Send("Hello");
    }
}

✔ No factory
✔ No string switching
✔ Very clean

❌ Option 3: Multiple registrations without factory (DON’T DO THIS)
builder.Services.AddScoped<INotification, EmailNotification>();
builder.Services.AddScoped<INotification, MessageNotification>();

Then:

IEnumerable<INotification> notifications

🚫 You cannot control which one to use
🚫 Leads to fragile runtime checks

✅ Recommendation (based on your constraint)
Scenario	Best Choice
.NET 6 / 7	Factory pattern
.NET 8+	Keyed services
Large system	Strategy + Factory

If you want, I can also show:

how to avoid NotImplementedException

how to route calls safely

how to add logging / retry / Polly

Just tell me 🚀
 Entity Framework

 multiple file reading with aysnc await alone and Task alone and comibnation of both
 
