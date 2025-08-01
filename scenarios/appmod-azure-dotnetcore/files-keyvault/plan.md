# .NET App Migration Prompt Template: Plaintext Credential to Secure Credentials

## Migration Request

Migrate this codebase from (Plaintext Credential) to (Secure Credentials), focusing **exclusively** on code-level changes required for successful compilation.

## Tools Usage

You **MUST** use the tools from (AzureKeyVaultKnowledgeBase) for more detailed SDK specs and (Secure Credentials) samples.
- Serve as a knowledge base for you when you make a plan.
- Serve as a knowledge base for you whenever you make code changes.
- Refer to the code samples for better code quality and keep the same code styles.

## Scope

* DO - Collect the framework used (.NET or .NET Framework) and keep the original project framework
* DO - Code modification to replace [Plaintext Credential] dependencies with [Secure Credentials] equivalents
* DO - Configuration file updates necessary for compilation
* DO - Dependency management changes
* DO - Update the function references to use the new generated functions.
* DO NOT - No testing beyond compilation verification
* DO NOT - No deployment considerations

## Success Criteria

1. All [Plaintext Credential] dependencies and imports are replaced.
2. All old (Plaintext Credential) code files and project configurations are cleaned from the solution.
3. Codebase compiles successfully with [Secure Credentials].
4. All migration tasks are tracked and marked as completed.

## Execution Process

### Analyze and Identify Migration Tasks

1. First read .NET related knowledge base from (AzureKeyVaultKnowledgeBase) for more (Secure Credentials) details.
   - Collect required package dependencies from knowledge base and save the dependency versions to the migration plan   
2. Analyze the codebase to identify all [Plaintext Credential] usages as well as those places using the old (Plaintext Credential) API.
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
5. Identify and clean up old (Plaintext Credential) files that have been replaced by new (Secure Credentials) equivalents.
6. Make sure build passed for the entire project after all steps, refer to the (AzureKeyVaultKnowledgeBase) when you meet compile errors related to api and sdk, keep fixing until the project compiles successfully.
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

### Migration Plan for Plaintext Credential to Secure Credentials (Azure Key Vault)

#### 1. Collect .NET Framework and Project Type
- Project: factory-dotnetcore-copilot-code-remediation.csproj
- Framework: net9.0 (SDK-style project)

#### 2. Required Azure Key Vault Packages
- Azure.Extensions.AspNetCore.Configuration.Secrets (1.4.0)
- Azure.Identity (1.14.0)

#### 3. Identify All Plaintext Credential Usages
- Controllers/HomeController.cs: Multiple hardcoded secrets, connection strings, API keys, passwords, tokens, and NetworkCredential usages.
- Controllers/SecurityController.cs: Hardcoded connection string with password.

#### 4. Migration Steps
- Add required Azure Key Vault NuGet packages to the project.
- Update configuration to support Key Vault integration (add KeyVaultName to appsettings.json).
- Refactor code to retrieve secrets from Azure Key Vault using DefaultAzureCredential and configuration.
- Remove all hardcoded secrets from codebase.
- Update usages of NetworkCredential, connection strings, API keys, and other secrets to use values from Key Vault.
- Clean up any obsolete code or configuration related to plaintext credentials.
- Verify build and compilation.

#### 5. Files to Modify
- factory-dotnetcore-copilot-code-remediation.csproj
- appsettings.json (create if missing)
- Program.cs
- Controllers/HomeController.cs
- Controllers/SecurityController.cs

#### 6. Dependencies to Update
- Add: Azure.Extensions.AspNetCore.Configuration.Secrets (1.4.0)
- Add: Azure.Identity (1.14.0)

#### 7. Configuration Files to Update
- appsettings.json: Add KeyVaultName

#### 8. Project Files to Update
- factory-dotnetcore-copilot-code-remediation.csproj: Add package references

#### 9. Build Verification
- Run build and fix any compilation errors.

---
