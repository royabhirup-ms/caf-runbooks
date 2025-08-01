# Code Migration Prompt Template: [Technology X] to [Technology Y]

## Migration Request

Migrate this codebase from [Technology X] to [Technology Y], focusing **exclusively** on code-level changes required for successful compilation.

## Scope

- ✅ Code modification to replace [X] dependencies with [Y] equivalents
- ✅ Configuration file updates necessary for compilation
- ✅ Dependency management changes (NuGet package references, packages.config, etc.)
- ❌ No infrastructure setup (assumed to be handled separately)
- ❌ No testing beyond compilation verification
- ❌ No deployment considerations

## Success Criteria

1. Codebase compiles successfully with [Technology Y]
2. Any authentication required with Azure services for [Technology Y] uses managed identity
3. All [Technology X] dependencies and imports are replaced
4. All migration tasks are tracked and completed

## Execution Process

1. Analyze the codebase to identify all [Technology X] usages
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
# Report success/failure
```

Do not pause for confirmation between steps. Continue methodically until all [Technology X] code is replaced with [Technology Y] and the build compiles successfully.
