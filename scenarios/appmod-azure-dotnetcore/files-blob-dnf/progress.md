# Migration Progress Tracker: File IO in Local File System to Azure Blob Storage

## Important Guideline

1. When you use terminal command tool, never input a long command with multiple lines, always use a single line command. (This is a bug in VS Copilot)
2. Never create a new project in the solution, always use the existing project to add new files or update the existing files.
3. Minimize code changes:
    - Update only what's necessary for the migration.
    - Avoid unrelated code enhancement.
4. Add New Package References to Projects
   Read the `.csproj` file of the target project, if there is SDK attribute in the `<Project>` element (e.g., `<Project Sdk="Microsoft.NET.Sdk">`), it is a .NET SDK-style project.
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

## Migration Task List

- [ ] Analyze codebase for all File IO in Local File System usages (Server.MapPath, Directory.CreateDirectory, File.Delete, SaveAs, etc.)
- [ ] Add Azure.Storage.Blobs (12.24.0), Azure.Storage.Blobs.Batch (12.21.0), Azure.Identity (1.14.0) package references
- [ ] Add Azure Blob Storage configuration to Web.config
- [ ] Create BlobStorageService to handle file operations with Azure Blob Storage
- [ ] Update CoursesController file upload logic to use BlobStorageService instead of local file system
- [ ] Update CoursesController file delete logic to use BlobStorageService instead of local file system
- [ ] Remove local file system code (Server.MapPath, Directory.CreateDirectory, File.Delete, SaveAs operations)
- [ ] Remove local uploads folder references from project
- [ ] Build and verify successful compilation
- [ ] Fix any migration-related build errors

---

> Update this file in real-time as you work through the migration steps. Only one task should be marked as `[in_progress]` at a time.
