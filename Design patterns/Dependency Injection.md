Dependency Injection is a technique where an object receives its dependencies from an external source rather than creating them itself. 

This means:
- A class **doesn't instantiate** its own dependencies.
- Instead, those dependencies are **"injected"** into it—typically via constructors, setters, or interfaces.

For example:
```java
class Car {
  private Engine engine;

  // Dependency injected via constructor
  public Car(Engine engine) {
    this.engine = engine;
  }
}
```
Here, the `Car` class doesn’t create the `Engine`—it receives it from outside.

### Why Use It?
- **Loose Coupling**: Classes are independent of specific implementations. [[SOLID Principles |Can be used in Dependency Inversion Principal]]
- **Testability**: You can easily swap real dependencies with mocks or stubs.
- **Flexibility**: Swap out implementations without changing client code.
- **Scalability**: Easier to manage complex systems.

## **Scopes** 
_Reference: Qwen3-32B model_

Also called **service lifetimes**. Which is how long a dependency instance should live and when a new one should be created. Choosing the right scope is crucial for performance, memory management, and correct behavior in your application.

It determines:
- **How many instances** of a service are created.
- **When the service is disposed** (if it implements `IDisposable`).
- **How dependencies are shared** between objects.

### 🎯 **Common DI Scopes**

#### 1. **Transient**
- **Lifetime**: A **new instance** is created **every time** the service is requested.
- **Use Case**:
  - Services that are **stateless** and **lightweight** (e.g., value objects, utilities).
  - Services that should **not be shared** between different parts of the application (e.g., random number generators).

- **Example**:  
  ```csharp
  services.AddTransient<ILogger>();
  ```

- **Pros**:
  - No risk of state corruption between requests.
  - Safe for thread-unsafe services.

- **Cons**:
  - Higher memory usage if used excessively.
  - Not suitable for services that require shared state.

#### 2. **Singleton**
- **Lifetime**: A **single instance** is created and **shared** across the **entire application**.
- **Use Case**:
  - Services that are **stateless** and **global** (e.g., configuration managers, caches, or singleton repositories).
  - Services that require **shared state** (e.g., a counter that tracks application-wide metrics).

- **Example**:  
  ```csharp
  services.AddSingleton<IMyService, MyService>();
  ```

- **Pros**:
  - High performance (no repeated object creation).
  - Efficient for global state.

- **Cons**:
  - **Risk of thread-safety issues** if the service is not thread-safe.
  - **Not suitable for mutable state** (e.g., a cache that changes over time).

#### 3. **Scoped**
- **Lifetime**: A **single instance** is created **per scope**, typically **per HTTP request** in web applications.
- **Use Case**:
  - Services that need to be **shared within a single request** (e.g., database contexts, user-specific data).
  - Services that require **short-lived state** (e.g., a transaction manager or a request-specific cache).
  
- **Example**:  
  ```csharp
  services.AddScoped<IMyService, MyService>();
  ```

- **Pros**:

  - Efficient for per-request operations.
  - Ensures isolation between different requests.

- **Cons**:
  - Not suitable for long-running operations (e.g., background tasks).
 
### 🧪 **When to Use Each Scope**

| **Scope**     | **Use Case**                                                                 | **Example**                          |
|---------------|-------------------------------------------------------------------------------|------------------------------------|
| **Transient** | Stateless, lightweight, or thread-unsafe services.                            | `ILogger`, `RandomNumberGenerator`   |
| **Singleton** | Global state, configuration, or services that should be reused everywhere.    | `ConfigurationManager`, `Cache`      |
| **Scoped**    | Per-request or per-unit-of-work operations.                                 | `DbContext`, `RequestScopedCache`    |

### ⚠️ **Best Practices**
1. **Avoid Singleton for Stateful Services**:
   - Never register a **mutable** or **thread-unsafe** service as a singleton. This can lead to **race conditions** or **data corruption**.
2. **Use Scoped for Web Applications**:
   - In web apps, register **database contexts** (e.g., `DbContext`) as **scoped** to ensure isolation between requests.
3. **Prefer Transient for Utilities**:
   - Use **transient** for **value objects** or **utilities** that do not need to maintain state.
4. **Dispose Resources Properly**:
   - Services implementing `IDisposable` should be registered with a scope that ensures they are **disposed at the end of the scope** (e.g., **scoped** or **transient**).
5. **Avoid Overuse of Singleton**:
   - Use **singleton** only for **global state** or **services that are truly stateless**.

### 📌 **Example: Registering Services in ASP.NET Core**

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Transient: New instance per request
    services.AddTransient<ILogger, ConsoleLogger>();
    // Singleton: Shared across the entire application
    services.AddSingleton<IMyService, MyService>();
    // Scoped: Shared per HTTP request
    services.AddScoped<DbContext, MyDbContext>();
}
```

### 🧱 **Scope Nesting (Advanced)**
Some DI containers allow **nested scopes**, which can be useful in scenarios like:
- **Unit of Work**: Create a new scope for a transaction.
- **Background Jobs**: Isolate a job's dependencies from the main application scope.

Example in ASP.NET Core:

```csharp
using (var scope = services.CreateScope())
{
    var dbContext = scope.ServiceProvider.GetRequiredService<MyDbContext>();
    // Use dbContext within this scope
}
```

### 📊 **Comparison of Scopes**

| **Scope**     | **Instance Count** | **Shared Across Requests?** | **Disposed?** | **Thread-Safe?** |
|---------------|--------------------|------------------------------|----------------|------------------|
| **Transient** | Many               | No                           | Yes            | If implemented   |
| **Singleton** | 1                  | Yes                          | Yes            | Must be         |
| **Scoped**    | 1 per scope        | No (within scope)            | Yes            | If implemented   |

### 🔍 **When in Doubt: Default to Transient or Scoped**
- **Transient** is safe for **short-lived** or **stateless** services.
- **Scoped** is ideal for **web applications** where isolation is needed.
- **Singleton** should be used sparingly and only for **global state**.