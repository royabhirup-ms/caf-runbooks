# Code Migration Prompt Template: Secrets in Web.config to Azure Key Vault

## Migration Request

Migrate this codebase from hardcoded secrets in Web.config to Azure Key Vault, focusing **exclusively** on code-level changes required for successful compilation.

## Scope

- ✅ Code modification to replace ConfigurationManager.AppSettings with Azure Key Vault client calls
- ✅ Configuration file updates necessary for compilation  
- ✅ Dependency management changes (NuGet package references, packages.config, etc.)
- ❌ No infrastructure setup (assumed to be handled separately)
- ❌ No testing beyond compilation verification
- ❌ No deployment considerations

## Success Criteria

1. Codebase compiles successfully with Azure Key Vault integration
2. Authentication with Azure Key Vault uses managed identity
3. All hardcoded secrets in Web.config are replaced with Azure Key Vault references
4. All migration tasks are tracked and completed

## NuGet Packages Required

The following NuGet packages **MUST** be added to the `eShopLegacyMVC` project:

- **Azure.Security.KeyVault.Secrets** (latest compatible with .NET Framework 4.8)
- **Azure.Identity** (latest compatible with .NET Framework 4.8)
- **Microsoft.Extensions.Configuration.AzureKeyVault** (if available for .NET Framework, otherwise use Azure.Security.KeyVault.Secrets directly)

**Important:** Do NOT attempt to add these packages yourself. Ask the user to install them for you with their exact names and specify that they should be added to the `eShopLegacyMVC` project.

## Migration Areas Identified

Based on the AppCat report Security.0003 findings, the following hardcoded secrets need to be replaced:

### Web.config AppSettings to Migrate:
- `files:ServiceAccountPassword` (currently empty in Web.config but referenced in code)
- `weather:ApiKey` (currently empty)
- Any other sensitive configuration values that should not be in plain text

### Code Files to Update:
- `eShopLegacyMVC\Services\FileService.cs` - Replace ConfigurationManager.AppSettings calls for service account credentials
- `eShopLegacyMVC\Services\FileServiceConfiguration.cs` - May need updates to support Key Vault integration

## Execution Process

1. Analyze the codebase to identify all hardcoded secret usages
2. Create a `progress.md` file to track changes with checkmarks
3. Execute migration tasks systematically:
   - Update dependency management files (be sure to list all NuGet packages that will need to be added with their exact names)
   - Create Azure Key Vault client service for retrieving secrets
   - Replace ConfigurationManager.AppSettings calls with Key Vault client calls
   - Update configuration files to support managed identity authentication
   - Mark tasks as completed in `progress.md` as they are done
4. Follow guidance from `migration-guidance.netfx.instructions.md` - this guidance is critical and must not be overlooked
5. Verify compilation after each step is REQUIRED using `msbuild /t:rebuild`
6. Mark tasks as completed: [ ] → [✓]
   - Tasks should be marked as done as soon as they are completed
7. Continue until all tasks are complete and build succeeds

## Authentication Requirements

- **MUST** use managed identity for Azure Key Vault authentication
- **MUST NOT** use connection strings, client secrets, or certificates in configuration files
- Use `DefaultAzureCredential` from Azure.Identity package for managed identity support

## Progress Tracking

Maintain a `progress.md` file with:
- [ ] Task description (with files modified)
- [ ] Verification step
- [ ] Completion status

## Build Verification

After each step you are REQUIRED to:
```
msbuild /t:rebuild
# Report success/failure
```

## Important Notes

- Follow all guidance in `migration-guidance.netfx.instructions.md`
- This is a .NET Framework 4.8 project - ensure all packages are compatible
- Use C# 7.3 syntax only - no newer language features
- All new source files MUST be explicitly added to the project file (.csproj) using `<Compile>` elements
- NEVER use .Wait(), .Result, or .GetAwaiter().GetResult() to block async code
- Either make the entire call chain async or use synchronous APIs where available

Do not pause for confirmation between steps. Continue methodically until all hardcoded secrets are replaced with Azure Key Vault integration and the build compiles successfully.
