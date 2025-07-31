# Code Migration Prompt: Local File System IO to Azure Blob Storage

## Migration Request

Migrate this codebase from Local File System IO to Azure Blob Storage, focusing **exclusively** on code-level changes required for successful compilation.

## Scope

- ✅ Code modification to replace File System IO dependencies with Azure Blob Storage equivalents
- ✅ Configuration file updates necessary for compilation
- ✅ Dependency management changes (NuGet package references, packages.config, etc.)
- ❌ No infrastructure setup (assumed to be handled separately)
- ❌ No testing beyond compilation verification
- ❌ No deployment considerations

## Success Criteria

1. Codebase compiles successfully with Azure Blob Storage integration
2. Authentication with Azure Blob Storage uses managed identity
3. All local file system IO operations are replaced with Azure Blob Storage operations
4. All migration tasks are tracked and completed

## NuGet Packages Required

The following NuGet packages **MUST** be added to the specified projects:

### eShopLegacyMVC project:
- **Azure.Storage.Blobs** (latest compatible with .NET Framework 4.8)
- **Azure.Identity** (latest compatible with .NET Framework 4.8)

### eShopLegacyMVC.Test project:
- **Azure.Storage.Blobs** (latest compatible with .NET Framework 4.8)
- **Azure.Identity** (latest compatible with .NET Framework 4.8)

## Identified File System Operations to Replace

Based on the AppCAT report (Local.0003 rule) and codebase analysis, the following file system operations need to be replaced:

### 1. FileService Class (eShopLegacyMVC\Services\FileService.cs)
- **ListFiles()**: Replace `Directory.GetFiles()` with blob enumeration
- **DownloadFile()**: Replace `File.ReadAllBytes()` with blob download
- **UploadFile()**: Replace `File.Create()` with blob upload
- Remove Windows authentication/impersonation logic as it's not needed for Azure Blob Storage

### 2. CatalogDBInitializer Class (eShopLegacyMVC\Models\Infrastructure\CatalogDBInitializer.cs)
- **GetCatalogTypesFromFile()**: Replace `File.Exists()` and `File.ReadAllLines()` with blob operations
- **GetCatalogItemsFromFile()**: Replace `File.ReadAllLines()` with blob download and text parsing
- **AddCatalogItemPictures()**: Replace `Directory.GetFiles()`, `ZipFile.ExtractToDirectory()` with blob operations

### 3. PicController Tests (eShopLegacyMVC.Test\Controllers\PicControllerTest.cs)
- Update test methods to work with blob storage mocking instead of file system operations

### 4. FileService Tests (eShopLegacyMVC.Test\Services\FileServiceTest.cs)
- Update all test methods to work with blob storage mocking instead of file system operations

## Execution Process

1. Analyze the codebase to identify all Local File System IO usages
2. Create a `progress.md` file to track changes with checkmarks
3. Execute migration tasks systematically:
   - Add required NuGet packages to both projects (ask user to install them)
   - Create Azure Blob Storage service classes
   - Replace FileService implementation with Azure Blob Storage operations
   - Replace CatalogDBInitializer file operations with blob operations
   - Update configuration to support Azure Blob Storage connection strings
   - Update test classes to work with Azure Blob Storage mocking
   - Mark tasks as completed in `progress.md` as they are done
4. Review code changes to ensure that migration guidance from `migration-guidance.netfx.instructions.md` has been followed
5. Verify compilation after each step is REQUIRED using `msbuild /t:rebuild`
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
```powershell
# Use MSBuild for .NET Framework projects
msbuild eShopLegacyMVC.sln /t:rebuild
# Report success/failure
```

## Migration Guidance Requirements

**IMPORTANT**: You must follow the guidance specified in `migration-guidance.netfx.instructions.md` including:

1. **Never add NuGet package dependencies directly** - Ask the user to install the required packages listed above
2. **Use C# 7.3 language features only** - This project is limited to C# 7.3
3. **Add new source files to project files** - All new .cs files must be explicitly added to the .csproj with `<Compile>` elements
4. **Use MSBuild for compilation** - Always use `msbuild /t:rebuild` instead of `dotnet build`
5. **Authentication with Azure services** - Ensure that authentication uses managed identity where possible
6. **Avoid blocking async code** - Never use .Wait(), .Result, or .GetAwaiter().GetResult()

## Configuration Changes Required

Update `Web.config` to include Azure Blob Storage connection string settings:
- Add app settings for Azure Storage Account connection string
- Ensure configuration builders are used to read from environment variables when running in Azure

## Key Implementation Notes

- Replace all `System.IO.File` operations with `BlobClient` operations
- Replace all `System.IO.Directory` operations with `BlobContainerClient` operations  
- Maintain the same public interface for `FileService` to minimize changes to consuming code
- Use blob naming conventions that mirror the original file paths
- Handle blob container creation and management
- Update error handling to work with Azure storage exceptions instead of file system exceptions
- Remove Windows-specific authentication/impersonation code since Azure Blob Storage uses different authentication mechanisms
