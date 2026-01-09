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
 compiled query
 Entity Framework
 
