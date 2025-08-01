# .NET App Migration Prompt Template: Windows AD to Microsoft Entra ID

## Migration Request

Migrate this codebase from (Windows AD) to (Microsoft Entra ID), focusing **exclusively** on code-level changes required for successful compilation.

## Tools Usage

You **MUST** use the tools from (MicrosoftEntraIDKnowledgeBase) for more detailed SDK specs and (Microsoft Entra ID) samples.
- Serve as a knowledge base for you when you make a plan.
- Serve as a knowledge base for you whenever you make code changes.
- Refer to the code samples for better code quality and keep the same code styles.

## Scope

* DO - Collect the framework used (.NET or .NET Framework) and keep the original project framework
* DO - Code modification to replace [Windows AD] dependencies with [Microsoft Entra ID] equivalents
* DO - Configuration file updates necessary for compilation
* DO - Dependency management changes
* DO - Update the function references to use the new generated functions.
* DO NOT - No testing beyond compilation verification
* DO NOT - No deployment considerations

## Success Criteria

1. All [Windows AD] dependencies and imports are replaced.
2. All old (Windows AD) code files and project configurations are cleaned from the solution.
3. Codebase compiles successfully with [Microsoft Entra ID].
4. All migration tasks are tracked and marked as completed.

## Execution Process

### Analyze and Identify Migration Tasks

1. First read .NET related knowledge base from (MicrosoftEntraIDKnowledgeBase) for more (Microsoft Entra ID) details.
   - Collect required package dependencies from knowledge base and save the dependency versions to the migration plan   
2. Analyze the codebase to identify all [Windows AD] usages as well as those places using the old (Windows AD) API.
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
5. Identify and clean up old (Windows AD) files that have been replaced by new (Microsoft Entra ID) equivalents.
6. Make sure build passed for the entire project after all steps, refer to the (MicrosoftEntraIDKnowledgeBase) when you meet compile errors related to api and sdk, keep fixing until the project compiles successfully.
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

### Migration Plan for Windows AD to Microsoft Entra ID

#### 1. Project Framework
- Project is .NET 9.0 (SDK-style, ASP.NET Core)

#### 2. Required Packages
- Remove: `Microsoft.AspNetCore.Authentication.Negotiate`
- Add: `Microsoft.Identity.Web` (latest)
- Add: `Microsoft.Identity.Web.UI` (latest)

#### 3. Code/Config Changes
- Remove Negotiate authentication setup from `Program.cs`
- Add Microsoft Identity Web authentication setup in `Program.cs` (see KnowledgeBase for code sample)
- Update controllers to use `[Authorize]` as needed (already present)
- Update `appsettings.json` to include `AzureAd` config section (see KnowledgeBase for sample)
- (Optional) Add Microsoft Graph integration if group/user checks are needed

#### 4. Clean Up
- Remove any code, config, or packages related to Windows AD/Negotiate

#### 5. Build Verification
- Ensure project builds and compiles after migration

---

### Migration Tasks
1. Remove Negotiate authentication package and code
2. Add Microsoft.Identity.Web and Microsoft.Identity.Web.UI packages
3. Update Program.cs for Microsoft Entra ID authentication
4. Update appsettings.json with AzureAd section
5. Clean up old Windows AD/Negotiate code and config
6. Build and verify compilation
7. Update progress tracking
