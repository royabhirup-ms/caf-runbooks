# Important Guidance while Re-platforming .NET Solutions

## C# Language Version
- Note the C# language version in `.csproj` files and do not use C# language features that are not supported by the specified version.

## Code Change Guidance
- Do NOT use .Wait(), .Result, or .GetAwaiter().GetResult() to block async code.
  - Either make callers of async methods async or use synchronous methods everywhere.

## Environment Considerations (Windows environment)
- Use Windows-style paths with backslashes (e.g., `C:\path\to\file.cs`)
- Use Windows-appropriate commands when suggesting terminal operations
- Consider Windows-specific behaviors when working with file system operations

## Using Azure services
- When using Azure services, ensure that authentication is done using managed identity where possible
- Avoid using password-based authentication or hardcoded credentials in the code
- If managed identity is not available, use Azure Key Vault to securely manage secrets and credentials

## Workflow Guidance
- After making code changes, ALWAYS verify the build succeeds (using `dotnet build`) before considering a task complete; do not say a task is successful until the build has completed and there are no new build errors or warnings
