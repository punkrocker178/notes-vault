> ASP.NET Core is a cross-platform, high-performance, open-source framework for building modern web apps using [.NET](https://learn.microsoft.com/en-us/dotnet/core/introduction).

Key features:
- Lightweight and modular HTTP request pipeline.
- [Kestrel](https://learn.microsoft.com/vi-vn/aspnet/core/fundamentals/servers/kestrel?view=aspnetcore-9.0): A [high-performance](https://github.com/aspnet/benchmarks) and cross-platform HTTP server.
- Integrated [dependency injection](https://learn.microsoft.com/vi-vn/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-9.0).
- [Environment-based configuration](https://learn.microsoft.com/vi-vn/aspnet/core/fundamentals/configuration/?view=aspnetcore-9.0).
- Rich logging, tracing, and runtime metrics.
- [Blazor](https://learn.microsoft.com/vi-vn/aspnet/core/blazor/?view=aspnetcore-9.0): Create rich interactive web UI components using [C#](https://learn.microsoft.com/en-us/dotnet/csharp/)—no JavaScript required.
- [Minimal APIs](https://learn.microsoft.com/vi-vn/aspnet/core/fundamentals/minimal-apis?view=aspnetcore-9.0): Build fast web APIs with minimal code and configuration by fluently declaring API routes and endpoints.
- [SignalR](https://learn.microsoft.com/en-us/aspnet/signalr/): Add real-time web functionality.
- [gRPC](https://learn.microsoft.com/vi-vn/aspnet/core/grpc/?view=aspnetcore-9.0): High performance Remote Procedure Call (RPC) services.
- Security: Built-in security features for [authentication](https://learn.microsoft.com/vi-vn/aspnet/core/security/authentication/?view=aspnetcore-9.0), [authorization](https://learn.microsoft.com/vi-vn/aspnet/core/security/authorization/introduction?view=aspnetcore-9.0), and [data protection](https://learn.microsoft.com/vi-vn/aspnet/core/security/data-protection/introduction?view=aspnetcore-9.0).
- Testing: Easily create unit and integration tests.
- Tooling: Maximize your development productivity with [Visual Studio](https://visualstudio.microsoft.com/) and [Visual Studio Code](https://code.visualstudio.com/)
# Rest API
Representational State Transfer (REST) is an architectural style for building web services. REST requests are made over HTTP. They use the same HTTP verbs that web browsers use to retrieve webpages and send data to servers.

Web service APIs that adhere to REST are called **RESTful APIs**. 
They are defined as:
- A base URI.
- HTTP methods, such as `GET`, `POST`, `PUT`, `PATCH`, or `DELETE`.
- A media type for the data, such as `JSON` or `XML`.

# Web API Controller
In order to make a controller working, we should extend `ControllerBase` class in our controller file. Also, we need to decorate the controller with `[ApiController]` attribute.
###  Class `ControllerBase`
> A base class for an MVC controller without view support.

This base class provides much standard functionality for handling HTTP requests.

###  Controller level  attributes
1. `[Controller]`: Explicitly marks a class as an MVC controller, overriding the default convention of using the "Controller" suffix in the class name.
2. `[ApiController]`: Controllers decorated with this attribute are configured with features and behavior building APIs.
3. `[NonController]`: Prevents a class from being recognized as a controller, even if it follows the naming convention.
4. `[Route("template")]`:
    Defines a route template for the entire controller, which can then be combined with action-level routes.
- `[Authorize]`: Enforces authorization for all actions within the controller, requiring authenticated users to access them.
- `[Consumes("mediaType")]`: Specifies the media types (e.g., "application/json") that the controller's actions can consume in requests.
- `[Produces("mediaType")]`: Specifies the media types that the controller's actions can produce in responses.

### Action-Level Attributes:
- `[HttpGet]`, `[HttpPost]`, `[HttpPut]`, `[HttpDelete]`, `[HttpPatch]`: Restricts an action method to handle specific HTTP verbs.
- `[Route("template")]`: Defines a specific route template for an individual action, overriding or extending the controller-level route.
- `[FromRoute]`, `[FromQuery]`, `[FromBody]`, `[FromHeader]`, `[FromForm]`, `[FromServices]` Specifies the source from which an action parameter's value should be bound (e.g., from the URL route, query string, request body, headers, form data, or dependency injection).
- `[Bind]`: Controls which properties of a model should be included or excluded during model binding.
- `[ValidateAntiForgeryToken]`: Protects against cross-site request forgery (CSRF) attacks in MVC applications.
- `[AllowAnonymous]`: Allows unauthenticated access to a specific action, even if the controller or a parent filter requires authorization.