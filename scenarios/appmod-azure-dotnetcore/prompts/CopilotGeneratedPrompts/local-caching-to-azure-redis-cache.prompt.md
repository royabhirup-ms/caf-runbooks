# Code Migration Prompt Template: Local Caching to Azure Redis Cache

## Migration Request

Migrate this codebase from Local Caching to Azure Redis Cache, focusing **exclusively** on code-level changes required for successful compilation.

## Scope

- ✅ Code modification to replace local in-process session state dependencies with Azure Redis Cache equivalents
- ✅ Configuration file updates necessary for compilation
- ✅ Dependency management changes (NuGet package references, packages.config, etc.)
- ❌ No infrastructure setup (assumed to be handled separately)
- ❌ No testing beyond compilation verification
- ❌ No deployment considerations

## Success Criteria

1. Codebase compiles successfully with Azure Redis Cache
2. Any authentication required with Azure services for Azure Redis Cache uses managed identity
3. All Local Caching dependencies and imports are replaced
4. All migration tasks are tracked and completed

## Required NuGet Packages

The following NuGet packages **MUST** be added to the `eShopLegacyMVC` project:
- `Microsoft.Web.RedisSessionStateProvider` - For Redis-based session state provider
- `StackExchange.Redis` - Redis client library for .NET

## Session State Migration Details

Based on the AppCat report issue Scale.0002, the following locations need to be updated:

### 1. Web.config Session Configuration
- **File**: `eShopLegacyMVC\Web.config`
- **Current**: `<sessionState mode="InProc" />`
- **Required**: Replace with Redis session state provider configuration

### 2. Session Usage Locations
The following files use session state and should continue to work with Redis-based sessions:
- `eShopLegacyMVC\Global.asax.cs` (lines 43-44): Sets MachineName and SessionStartTime
- `eShopLegacyMVC\Controllers\AspNetSessionController.cs` (lines 11-13, 22-24): Demo session usage
- `eShopLegacyMVC\Controllers\UserInfoController.cs` (line 10): Sets Username
- `eShopLegacyMVC\Views\Shared\_Layout.cshtml` (line 42): Displays session info

## Important Migration Guidance

Please follow the instructions in the `migration-guidance.netfx.prompt.md` file. This guidance is important and must not be overlooked.

## Execution Process

1. Analyze the codebase to identify all Local Caching usages
2. Create a `progress.md` file to track changes with checkmarks
3. Execute migration tasks systematically:
   - Update dependency management files (be sure to list all NuGet packages that will need to be added with their exact names)
   - Replace API calls and imports
   - Update configuration files
   - Mark tasks as completed in `progress.md` as they are done
4. Review code changes to ensure that any migration guidance specified has been followed
5. Verify compilation after each step is REQUIRED
6. Mark tasks as completed: [ ] → [✓]
   - Tasks should be marked as done as soon as they are completed
7. Continue until all tasks are complete and build succeeds

## Progress Tracking

Maintain a `progress.md` file with:
- [ ] Task description (with files modified)
- [ ] Verification step
- [ ] Completion status

## Build Verification

After each step you are REQUIRED to:
```
# Run appropriate build command for project type
msbuild /t:rebuild
# Report success/failure
```

Do not pause for confirmation between steps. Continue methodically until all Local Caching code is replaced with Azure Redis Cache and the build compiles successfully.

## Expected Configuration Changes

### Web.config Updates Required:
1. Replace `<sessionState mode="InProc" />` with Redis session state provider configuration
2. Add connection string for Redis cache
3. Configure session timeout and other Redis-specific settings

### Code Changes:
- Session access patterns (Session["key"], HttpContext.Session["key"]) should remain the same
- The underlying storage mechanism will change from in-process memory to Redis
- Ensure managed identity is used for Redis authentication where possible

## Notes:
- The current session usage is primarily for demonstration purposes (username, role, machine name, session start time)
- All existing session access patterns should continue to work transparently with Redis backend
- Focus on configuration changes rather than application code changes for session access
