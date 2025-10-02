The following app startup code supports several app types:

- [Blazor Web Apps](https://learn.microsoft.com/vi-vn/aspnet/core/blazor/?view=aspnetcore-9.0)
- [Razor Pages](https://learn.microsoft.com/vi-vn/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-9.0)
- [MVC controllers with views](https://learn.microsoft.com/vi-vn/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-9.0)
- [Web API with controllers](https://learn.microsoft.com/vi-vn/aspnet/core/tutorials/first-web-api?view=aspnetcore-9.0)
- [Minimal APIs](https://learn.microsoft.com/vi-vn/aspnet/core/tutorials/min-web-api?view=aspnetcore-9.0)

`Program.cs`
```csharp
using WebAll.Components;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddRazorComponents()
    .AddInteractiveServerComponents();
builder.Services.AddRazorPages();
builder.Services.AddControllersWithViews();

// Register TodoContext to connect to SQL Server using connection string
builder.Services.AddDbContext<TodoContext>(opt => 
	opt.UseSqlServer(
		builder.Configuration.GetConnectionString("DefaultConnection")
	)
);

var app = builder.Build();

// Configure the HTTP request pipeline.
if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Error");
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();

app.UseAuthorization();

app.MapGet("/hi", () => "Hello!");

app.MapDefaultControllerRoute();
app.MapRazorPages();

app.MapRazorComponents<App>()
    .AddInteractiveServerRenderMode();

app.UseAntiforgery();

app.Run();

```

[Reference](https://learn.microsoft.com/vi-vn/aspnet/core/fundamentals/startup?view=aspnetcore-9.0)