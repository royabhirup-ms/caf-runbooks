# .NET App Migration Prompt Template: Local File IO to Azure Blob Storage

## Migration Request

Migrate this codebase from (Local File IO) to (Azure Blob Storage), focusing **exclusively** on code-level changes required for successful compilation.

## Tools Usage

You **MUST** use the tools from (AzureStorageBlobKnowledgeBase) for more detailed SDK specs and (Azure Blob Storage) samples.
- Serve as a knowledge base for you when you make a plan.
- Serve as a knowledge base for you whenever you make code changes.
- Refer to the code samples for better code quality and keep the same code styles.

## Scope

* DO - Collect the framework used (.NET or .NET Framework) and keep the original project framework
* DO - Code modification to replace Local File IO dependencies with Azure Blob Storage equivalents
* DO - Configuration file updates necessary for compilation
* DO - Dependency management changes
* DO - Update the function references to use the new generated functions.
* DO NOT - No testing beyond compilation verification
* DO NOT - No deployment considerations

## Success Criteria

1. All Local File IO dependencies and imports are replaced.
2. All old (Local File IO) code files and project configurations are cleaned from the solution.
3. Codebase compiles successfully with Azure Blob Storage.
4. All migration tasks are tracked and marked as completed.

## Execution Process

### Analyze and Identify Migration Tasks

1. First read .NET related knowledge base from (AzureStorageBlobKnowledgeBase) for more (Azure Blob Storage) details.
   - Collect required package dependencies from knowledge base and save the dependency versions to the migration plan   
2. Analyze the codebase to identify all Local File IO usages as well as those places using the old (Local File IO) API.
   - Identify all files that need to be modified.
   - Identify all dependencies that need to be updated.
   - Identify all configuration files that need to be updated.
   - Identify all project files that need to be updated.

### Create Migration Temporary Files

1. Create the required migration files using PowerShell:
   ```powershell
   # Create the plan and progress tracking files
   New-Item -Path ".appmod/.migration/plan.md", ".appmod/.migration/progress.md" -ItemType File -Force
   ```
2. Use the `edit_file` tool to populate these files:
   - Edit `plan.md` to document the migration plan
   - Edit `progress.md` to track migration progress

NOTE: **DO NOT** add files under `.appmod/` to the .csproj project files, they are temporary files for migration purpose only.

### Before Starting Migration

After creating the plan.md and progress.md, stop the session and wait for user's review and continue signal.

### Execute Migration and Track Progress

Execute the migration tasks as follows:

1. Refer to section `Important Guideline` about how to track the status.
2. Execute migration tasks in the order they are listed in `progress.md`.
3. Ask for user to review the `plan.md` and `progress.md` files before starting the migration tasks, you DO NOT need to pause for confirmation between other tasks.
4. Continue until all tasks are complete.
5. Identify and clean up old (Local File IO) files that have been replaced by new (Azure Blob Storage) equivalents.
6. Make sure build passed for the entire project after all steps, refer to the (AzureStorageBlobKnowledgeBase) when you meet compile errors related to api and sdk, keep fixing until the project compiles successfully.
7. Stick to the `plan.md` and `progress.md` files, finish all the tasks and do not deviate from the plan unless absolutely necessary.
8. Before finish, review the `progress.md` file to ensure all tasks are completed.

## Build Verification

After all steps you are REQUIRED to:
- Add newly created projects to the solution if applicable
- Make sure all the projects are reloaded before triggering the build process
- Run the appropriate build command for project type
- Report success/failure
- Fix any compilation errors and re-verify

---

### Migration Plan

#### 1. Collect framework and dependencies
- Project is .NET 9.0 (SDK-style)
- Add the following NuGet packages:
  - Azure.Storage.Blobs (12.24.0)
  - Azure.Storage.Blobs.Batch (12.21.0)
  - Azure.Identity (1.14.0)

#### 2. Identify Local File IO usages
- Controllers/HomeController.cs: Usage of System.IO.File.Exists, System.IO.File.WriteAllText, System.IO.File.ReadAllText

#### 3. Migration Tasks
- [ ] Add Azure Blob Storage NuGet dependencies to the project
- [ ] Update configuration to include Azure Blob Storage endpoint
- [ ] Refactor HomeController.cs to replace System.IO.File usage with Azure Blob Storage SDK
- [ ] Remove obsolete Local File IO code
- [ ] Build and verify successful compilation
- [ ] Clean up and finalize migration

---

> For detailed API usage, always refer to AzureStorageBlobKnowledgeBase.
