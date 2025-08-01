# Migration Progress: Windows AD to Microsoft Entra ID

## Important Guideline
1. When you use terminal command tool, never input a long command with multiple lines, always use a single line command. (This is a bug in VS Copilot)
2. Never create a new project in the solution, always use the existing project to add new files or update the existing files.
3. Minimize code changes:
    - Update only what's necessary for the migration.
    - Avoid unrelated code enhancement.
4. Add New Package References to Projects
   Read the `.csproj` file of the target project, if there is SDK attribute in the <Project> element (e.g., `<Project Sdk="Microsoft.NET.Sdk">`), it is a .NET SDK-style project.
   - For .NET SDK style project, use the following command to add each package: `dotnet add package <PACKAGE_NAME> --version <VERSION>`.
   - For non-sdk style project, follow these steps:
       1. Unload the project via tool `unload_project`.
       2. Install each package to directory `packages` via command `nuget install <PACKAGE_NAME> -Version <VERSION> -OutputDirectory packages`.
       3. From the `packages` folder, identify the highest version of each installed package, record the package name and version.
       4. Use tool `get_file` to read and `edit_file` to modify the .csproj file, add the package reference.
       5. If needed, update Web.config or App.config files if necessary.
       6. After the modification, reload the project via tool `reload_project`. Make sure you always reload the project after unload a project, never leave projects unloaded in the solution.
5. **Task Tracking and Progress Updates**
   - Use checkmark to track the progress of each task in `progress.md`:
     - `[]` for tasks not started
     - `[X]` for tasks completed
     - `[in_progress]` for tasks currently being worked on
   - Before starting any migration task, mark it as `in_progress` in `progress.md`. Only one task should be marked as `in_progress` at a time.
   - As soon as a task is completed, immediately update its status to completed in `progress.md` before moving to the next task.
   - Update the status of tasks in real-time as you work, ensuring `progress.md` always reflects the current state.
   - If you discover new required tasks during migration, add them to `progress.md` and the plan immediately, and track their status as above.
   - Do not batch status updates; always update `progress.md` as soon as a task's status changes.
6. After all tasks are finished, review `progress.md` to ensure all tasks are finished and marked as complete.

---

## Migration Task Progress

- [X] Remove Negotiate authentication package and code
- [X] Add Microsoft.Identity.Web and Microsoft.Identity.Web.UI packages
- [X] Update Program.cs for Microsoft Entra ID authentication
- [X] Update appsettings.json with AzureAd section
- [X] Clean up old Windows AD/Negotiate code and config
- [X] Build and verify compilation
- [X] Update progress tracking

## Migration Summary

? **Migration Complete!**

All Windows AD (Negotiate) authentication components have been successfully replaced with Microsoft Entra ID authentication:

1. **Removed** Microsoft.AspNetCore.Authentication.Negotiate package
2. **Added** Microsoft.Identity.Web and Microsoft.Identity.Web.UI packages (version 3.11.0)
3. **Updated** Program.cs with Microsoft Entra ID authentication configuration
4. **Added** AzureAd and DownstreamApis configuration sections to appsettings.json
5. **Verified** successful compilation with no errors

The project now uses Microsoft Entra ID for authentication instead of Windows AD/Negotiate authentication.
