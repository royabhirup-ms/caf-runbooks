NEVER add NuGet package dependencies. Ask the user to install them with the exact package name and which project it should be added to. The user will add the package and update the project file accordingly.

# Important Guidance while Re-platforming .NET Framework Solutions

## Build and Compilation Requirements
- Always use `msbuild /t:rebuild` to build the solution or projects instead of `dotnet build`
- When building, verify that compilation succeeds before proceeding with additional changes

## C# Language Version is 7.3
- This project is limited to C# 7.3 features only. Please avoid using:
  - C# 8.0 features like using declarations (using var x = ...)
  - await using statements
  - Switch expressions
  - etc.

## Project File Management
- All new source files **MUST** be explicitly added to the project file (`.csproj`) using a `<Compile>` element
  - .NET Framework projects do not automatically include files in the directory like SDK-style projects
  - Example: `<Compile Include="Path\To\NewFile.cs" />`

## NuGet Package Management
- **Do NOT attempt to add NuGet packages directly**
- If a NuGet package is needed, ask the user to install it
  - The user will add the package and update the project file accordingly
- Only request NuGet packages that are compatible with .NET Framework 4.8

## Using Azure services
- When using Azure services, ensure that authentication is done using managed identity where possible
- Avoid using password-based authentication or hardcoded credentials in the code

## Code Change Guidance
- **NEVER use .Wait(), .Result, or .GetAwaiter().GetResult() to block async code.**
  - These sync-over-async patterns can lead to deadlocks and poor performance
  - Either make the entire call chain async (preferred approach):
    - Change method signatures to return Task/Task<T>
    - Use async/await keywords throughout the call chain
  - Or use truly synchronous APIs where available:
    - Find synchronous alternatives to async methods
    - Example: Instead of `client.SendMessageAsync(message).GetAwaiter().GetResult()`, see if there's a `SendMessage(message)` method available
  - When working with libraries that only offer async APIs:
    - Refactor the calling methods to be async all the way up the call chain
    - If refactoring to async is impossible due to framework constraints, consider creating a separate background process or message handler
- When adding new services, follow the existing service patterns in the codebase. For example, if the codebase uses dependency injection, ensure new services are registered in the same way.

## Environment Considerations (Windows environment)
- Use Windows-style paths with backslashes (e.g., `C:\path\to\file.cs`)
- Use Windows-appropriate commands when suggesting terminal operations
- Consider Windows-specific behaviors when working with file system operations

## Workflow Guidance
- After making code changes, ALWAYS verify the build succeeds before considering a task complete; do not say a task is successful until the build has completed and there are no new build errors
- When updating references or dependencies, ensure all related files are updated consistently
