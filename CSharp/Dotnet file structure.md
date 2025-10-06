## **Solution file**
Representing a root folder, a solution file can link projects together and setup runtime configurations for each project.
Is named as: `filename.sln`. It stays in the root folder

## **Project file**
A solution can contain many projects, each project represents an application or a service.
In a project file, we can:
- Define packages required for the project to run
- Can reference other projects to improve
	- **Code reuse & modularity**: Can access other project classes, models, methods
	- **Dependency management**: When a project is referenced, it is guaranteed to be built before the referencing project. This ensures all necessary components are available during runtime.
	- **Encapsulation and Separation of Concerns**: By dividing your application into logically distinct projects, you can enforce boundaries and ensure that each project focuses on a specific set of responsibilities. This also helps in maintaining encapsulation, as only the public members of a referenced project are accessible to the referencing project.

## **Use cases**
### 1. Setup xUnit project for testing
We need to Add a new testing project in the current solution. If the main project is in the same directory as the solution, then adding the test project might cause build duplication errors. Which means, Visual studio is picking up testing project files as the main project ([Duplicate AssemblyVersion Attribute](https://stackoverflow.com/questions/10311347/duplicate-assemblyversion-attribute))

**Solution:**
We need to exclude files in the main project `csproj`
```xml
<PropertyGroup>
	<DefaultItemExcludes>$(DefaultItemExcludes);*.Tests\**\*;</DefaultItemExcludes>
</PropertyGroup>
```

