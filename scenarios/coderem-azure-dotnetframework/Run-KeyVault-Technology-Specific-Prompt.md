## Run Technology Specific Prompt for Azure Key Vault Integration:

This section represents on how to execute the newly created prompt for code remediation on a specific technology.



1. Download the packages mentioned in the newly created prompt from NuGet package manager manually.
    
   ![Nuget](./images/nuget.png)

- Add the below as context to the copilot chat:

1. Instruction markdown file.
2. The Codebase to be migrated.
3. Run the newly created prompt for code remediation on Azure Key Vault integration.
   This will also generate a progress file to track the status of the code remediation process. Example: See the full progress [here](./prompts/KeyVault-Progress/progress.md).

    ![Run Prompt](./images/runprompt.png)

This will generate the necessary code changes to replace hardcoded secrets with Azure Key Vault integration and will build the code as per instructions successfully.

   ![Progress](./images/progressstatus.png)
   ![Progress](./images/progressstatus2.png)

Note: 
1. Ensure to verify the modified configuration file and application code.

    ![Configuration Changes](./images/configchanges.png)
    ![Code Changes Changes](./images/codesecrets-kv.png)

2. Ensure to verify the build status and test the application post code changes, for any build or runtime issues, we may have to modify few parts of the code manually depending on the build error.
   
   ![Build Status](./images/buildstatus.png)


3. Review the overall integration with Azure Key Vault to ensure successful implementation.

---

[*Back to content*](README.md)