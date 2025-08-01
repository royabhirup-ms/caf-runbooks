````markdown
# Code Migration Prompt Template: Local Caching to Azure Redis Cache

## Migration Request

Migrate this codebase from Local Caching to Azure Redis Cache, focusing **exclusively** on code-level changes required for successful compilation.

## Scope

- ✅ Code modification to replace local in-memory caching dependencies with Azure Redis Cache equivalents
- ✅ Configuration file updates necessary for compilation
- ✅ Dependency management changes (NuGet package references)
- ❌ No infrastructure setup (assumed to be handled separately)
- ❌ No testing beyond compilation verification
- ❌ No deployment considerations

## Success Criteria

1. Codebase compiles successfully with Azure Redis Cache
2. Authentication with Azure Redis Cache uses managed identity where possible
3. All Local Caching dependencies and imports are replaced
4. All migration tasks are tracked and completed

## NuGet Packages Required

The following NuGet packages **MUST** be added to the project:

- **Microsoft.Extensions.Caching.StackExchangeRedis** (latest version compatible with .NET 9.0)
- **Azure.Identity** (latest version compatible with .NET 9.0) - for managed identity authentication

## Identified Local Caching Usage

Based on the AppCAT report (Cache.0001 rule), the following local caching usage has been identified:

### Location: Program.cs (Line 22)
- **Current Implementation**: `builder.Services.AddMemoryCache();`
- **Required Change**: Replace with Redis cache configuration

## Execution Process

1. Analyze the codebase to identify all Local Caching usages
2. Create a `progress.md` file to track changes with checkmarks
3. Execute migration tasks systematically:
   - Update dependency management files (add required NuGet packages listed above)
   - Replace memory cache registration with Redis cache configuration
   - Update any cache usage patterns in controllers or services
   - Update configuration files to support Redis connection
   - Mark tasks as completed in `progress.md` as they are done
4. Review code changes to ensure that migration guidance from `migration-guidance.netcore.instructions.md` has been followed
5. Verify compilation after each step is REQUIRED using `dotnet build`
6. Mark tasks as completed: [ ] → [✓]
   - Tasks should be marked as done as soon as they are completed
7. Continue until all tasks are complete and build succeeds

## Migration Tasks

Based on the codebase analysis, the following specific tasks need to be completed:

### 1. Update Program.cs
- **File**: `Program.cs`
- **Line**: 22
- **Current**: `builder.Services.AddMemoryCache();`
- **Action**: Replace with Redis cache configuration using `AddStackExchangeRedisCache()`

### 2. Configuration Updates
- **File**: `appsettings.json` and `appsettings.Development.json`
- **Action**: Add Redis connection string configuration section
- **Note**: Use connection string placeholder that can be replaced with Azure configuration

### 3. Dependency Injection Updates
- **Action**: Ensure any controllers or services that inject `IMemoryCache` are updated to inject `IDistributedCache` instead
- **Note**: Search codebase for any `IMemoryCache` usage patterns

## Important Migration Guidance

Please follow the instructions in the `migration-guidance.netcore.instructions.md` file. This guidance is important and must not be overlooked. Key points include:

- Note the C# language version in `.csproj` files and do not use C# language features that are not supported by the specified version
- Do NOT use .Wait(), .Result, or .GetAwaiter().GetResult() to block async code
- When using Azure services, ensure that authentication is done using managed identity where possible
- Avoid using password-based authentication or hardcoded credentials in the code

## Progress Tracking

Maintain a `progress.md` file with:
- [ ] Task description (with files modified)
- [ ] Verification step
- [ ] Completion status

## Build Verification

After each step you are REQUIRED to:
```powershell
# Run build command for .NET Core project
dotnet build
# Report success/failure
```

Do not pause for confirmation between steps. Continue methodically until all Local Caching code is replaced with Azure Redis Cache and the build compiles successfully.

## Expected Configuration Changes

### appsettings.json Updates Required:
```json
{
  "ConnectionStrings": {
    "Redis": "placeholder-for-redis-connection-string"
  }
}
```

### Program.cs Updates Required:
- Replace `builder.Services.AddMemoryCache();` with Redis cache configuration
- Add Redis connection string configuration
- Configure authentication for Azure Redis Cache using managed identity when possible

## Code Changes:
- Any `IMemoryCache` injection should be replaced with `IDistributedCache`
- Cache access patterns may need to be updated from synchronous to asynchronous operations
- Consider serialization requirements for complex objects stored in distributed cache
````
