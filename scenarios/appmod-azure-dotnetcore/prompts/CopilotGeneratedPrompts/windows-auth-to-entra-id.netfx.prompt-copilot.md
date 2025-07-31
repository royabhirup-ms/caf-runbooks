# Code Migration Prompt Template: Windows Authentication to Entra ID

## Migration Request

Migrate this codebase from Windows authentication to Entra ID authentication, focusing **exclusively** on code-level changes required for successful compilation.

## Scope

- ✅ Code modification to replace Windows authentication dependencies with Entra ID equivalents
- ✅ Configuration file updates necessary for compilation
- ✅ Dependency management changes (NuGet package references, packages.config, etc.)
- ❌ No infrastructure setup (assumed to be handled separately)
- ❌ No testing beyond compilation verification
- ❌ No deployment considerations

## Success Criteria

1. Codebase compiles successfully with Entra ID authentication
2. Any authentication required with Azure services for Entra ID uses managed identity
3. All Windows authentication dependencies and imports are replaced
4. All migration tasks are tracked and completed

## Required NuGet Packages

The following NuGet packages need to be added to the specified projects:

### eShopLegacyMVC project:
- `Microsoft.AspNetCore.Authentication.OpenIdConnect` (latest version compatible with .NET Framework 4.8)
- `Microsoft.AspNetCore.Authentication.Cookies` (latest version compatible with .NET Framework 4.8)
- `Microsoft.Identity.Web` (already present - version 3.10.0)
- `Microsoft.Identity.Web.MicrosoftGraph` (latest version compatible with .NET Framework 4.8)

### eShopLegacy.Utilities project:
- `Microsoft.Graph` (latest version compatible with .NET Framework 4.8)
- `Microsoft.Graph.Auth` (latest version compatible with .NET Framework 4.8)

## Execution Process

1. Analyze the codebase to identify all Windows authentication usages
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

## Specific Changes Required

Based on the AppCat analysis (Identity.0002 issues), the following specific changes are required:

### 1. Web.config Authentication Mode
- Change `<authentication mode="Windows" />` to support Entra ID authentication
- Update connection strings to remove `Integrated Security=True` and use Azure SQL authentication

### 2. FileService.cs Windows Identity Usage
- Replace all instances of `WindowsIdentity.GetCurrent()` with Entra ID token acquisition
- Replace `WindowsIdentity.Impersonate()` calls with proper Azure authentication context
- Update the `GetAuthToken` method to use Entra ID instead of Windows logon

### 3. AccountController and Identity Configuration
- Update `Startup.Auth.cs` to configure Entra ID authentication
- Modify `IdentityConfig.cs` to work with Entra ID claims
- Update `AccountController.cs` to handle Entra ID sign-in/sign-out

### 4. Application User Model
- Update `ApplicationUser` class to work with Entra ID claims
- Modify user identity generation to use Entra ID tokens

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

## Important Migration Guidance

Follow the instructions in the `migration-guidance.netfx.instructions.md` file, particularly:
- Always use `msbuild /t:rebuild` to build the solution
- Use C# 7.3 features only
- Add new source files explicitly to the project file using `<Compile>` elements
- Use managed identity for Azure service authentication
- Do not use sync-over-async patterns like `.Wait()`, `.Result`, or `.GetAwaiter().GetResult()`

Do not pause for confirmation between steps. Continue methodically until all Windows authentication code is replaced with Entra ID authentication and the build compiles successfully.
