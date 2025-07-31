# GitHub Copilot App Modernization for .NET Core Applications on Azure


## Document Summary
  See the full [Document Summary](Document-Summary.md)
## Change Log
  Full change history is available in the [Change Log](Change-Log.md)


## Contents

- [**Introduction**](#1-introduction)
- [**Role and Responsibilities**](#2-role-and-responsibilities)
- [**Planning**](#3-planning)
- [**Pre-requisites**](#4-pre-requisites)
- [**Utilization of Prompts**](#5-utilization-of-prompts)
- [**Migration Steps of Github Copilot Using Prompt Engineering for Azure PaaS Services**](#6-migration-steps-of-github-copilot-using-prompt-engineering-for-azure-paas-services)
- [**Guide To Known Issues**](#7-guide-to-known-issues)
- [**References**](#8-references)
- [**Abbreviations**](#9-abbreviations)


## 1. Introduction

This document offers a concise overview of the process of remediating AppCat issues which are recommended to use relevant Azure PaaS components using GitHub Copilot App Modernization Visual Studio Extension.

### 1.1 Github Copilot App Modernization

App modernization is the process of updating and improving existing applications to take advantage of modern cloud-native technologies and practices. GitHub Copilot can assist in this journey by providing intelligent code suggestions and automating repetitive tasks.

GitHub Copilot App Modernization for .NET aims to help enterprises migrate their .NET applications to Azure with confidence and efficiency, covering assessment, code remediation and validation, powered by the intelligence of GitHub Copilot.


## 2. Role and Responsibilities

| **Task**                        | **Responsible**     | **Accountable**     | **Consulted**           | **Informed**         |
|---------------------------------|----------------------|----------------------|--------------------------|----------------------|
| Assessment Report to be executed | Customer / Partner   | Customer / Partner   | Customer / Partner       | FACTORY              |
| Analysis of Report     | FACTORY              | FACTORY              | Customer / FACTORY       | Customer / Partner   |
| Github Copilot App Modernization    | FACTORY/Customer              | FACTORY/Customer              | FACTORY/Customer       | FACTORY/Customer   |

---

## 3. Planning

1. Ensure to run assessment for GitHub Copilot App Modernization for .NET.
2. Ensure to identify all applications, services, and dependencies before migration to Azure cloud.

---

## 4. Pre-requisites

- Finalization of the applications to be migrated (Wave planning)  
- Run [Azure Migrate Tool](https://learn.microsoft.com/en-us/azure/migrate/appcat/dotnet?view=migrate-classic) for assessment - Identify all applications, services, and dependencies for better visibility before copilot assessment scan.
- To use GitHub Copilot, you can install the following Integrated Development Environments (IDEs):
  - [Visual Studio 2022 version 17.14.7 or newer](https://visualstudio.microsoft.com/downloads/)
  - [Visual Studio Code](https://code.visualstudio.com/)
- A GitHub account to connect your code editor to Copilot
  - [Sign in to Visual Studio using a GitHub account](https://learn.microsoft.com/en-us/visualstudio/ide/work-with-github-accounts) with [Copilot access](https://docs.github.com/copilot/about-github-copilot/what-is-github-copilot#getting-access-to-copilot).
 - Supported subscription plans:
  - Copilot Pro
  - Copilot Pro+
  - Copilot Business
  - Copilot Enterprise

- [Sign in to Visual Studio using a GitHub account](https://learn.microsoft.com/en-us/visualstudio/ide/work-with-github-accounts) with [Copilot access](https://docs.github.com/copilot/about-github-copilot/what-is-github-copilot#getting-access-to-copilot).


## 5. GitHub Copilot App Modernization for .NET Core:

## 5.1 Github Copilot Sign in

Let’s sign in with Github Copilot Enterprise in Visual Studio.

![Enterprise Signin](./images/signin.png)

## 5.2 Install GitHub Copilot app modernization for .NET Extension:

Let’s install the GitHub Copilot app modernization for .NET extension in Visual Studio.

![Install Extension](./images/install-extension.png)

## 5.3 Run Assessment:

1. Right-click the top-level solution node, then select GitHub Copilot app modernization for .NET > Run Assessment. This will identify all applications, services, and dependencies related to specific Azure services.

![Run Assessment](./images/runassessment.png)

This may ask to install the latest version of the Azure Migrate AppCat extension, please install it to proceed with the assessment.

![App Cat](./images/AppCat.png)

This is will generate the Assessment report which will be used to for code remediation to Azure PaaS services.

![Loader Report](./images/loaderreport.png)

![Assessment Report](./images/assessmentreport.png)

## 5.3 Execution of GitHub Copilot app modernization for .NET:

We will analyze and execute GitHub Copilot using specific Azure services below:

1. **Azure Key Vault**
2. **Azure Blob Storage**
3. **Microsoft Entra ID**
4. **Azure Service Bus**
5. **Azure Redis Cache** (Using Prompt Engineering)



## 6. Migration Steps of Github Copilot Using Prompt Engineering for Azure PaaS Services:

## 6.1 Azure Key Vaults:

Let’s prepare an application which has hardcoded connection strings and passwords in the code.

![Hard Codded Password](./images/hardcoddedpassword.png)

Let's see the AppCat report findings related to Azure Key Vault:

![Appcat Findings](./images/appcatfindings.png)


Let's proceed with **STEP 1** i.e., [Create-Technology-Specific-Prompt](Create-Technology-Specific-Prompt.md) to create and attach necessary files as a context in copilot chat which will be used to create prompt for Azure Key Vault integration.

Once the files in copilot chat are attached, tell copilot to remediate and apply the code changes for the AppCat issues related to hardcoded secrets (i.e., Technology X) issue using Azure Keyvault (i.e., Technology Y) as a next step.
In background copilot will follow the guidance provided in the instruction file and will generate a new prompt which will be followed to remediate the specific issues.

**Example**, we can ask copilot to remediate the hardcoded secrets issue using the below command:

```bash
Please execute #file:[YourPromptCreationFileName].md using "secrets in web.config" as "Technology X" and "Azure Key Vault" as "Technology Y".

You can use the AppCat report #file:[YourAppCatFileName].appcat.json  and look at issue Security.0003 to see specific locations in the solution where hard-coded secrets need to be replaced.
```

 ![Command](./images/command.png)

This will generate a new prompt for code remediation on Azure Key Vault integration.

 ![Secrets KV](./images/secrets-kv.png)

**Example**, please see the full copilot generated prompt for Azure Key Vault integration [Key Vault Prompt](./prompts/CopilotGeneratedPrompts/secrets-to-keyvault.netfx.prompt.md) 


Now, we have successfully created a prompt for Azure Key Vault integration. Let's proceed with **STEP 2** i.e., the execution of the prompt to remediate the hardcoded secrets issue.

See the steps [Run-KeyVault-Technology-Specific-Prompt](Run-KeyVault-Technology-Specific-Prompt.md)


## 6.2 Azure Blob Storage:

Let’s prepare an application which has System.IO.File references with file access dependencies of server in the code.

![File Systems](./images/filesystems.png)

Let's see the AppCat report findings related to Azure Blob Storage:

![Appcat Findings Blob](./images/appcatfindingsblob.png)

Let's proceed with STEP 1 i.e., [Create-Technology-Specific-Prompt](Create-Technology-Specific-Prompt.md) to attach necessary files which will be used to create prompt for Azure Blob Storages.

Once the files in copilot chat are attached, tell copilot to remediate and apply the code changes for the AppCat issues related to Local file system IO (i.e., Technology X) issue using Azure Blob Storage (i.e., Technology Y) as a next step.
In background copilot will follow the guidance provided in the instruction file and will generate a new prompt which will be followed to remediate the specific issues.

**Example**, we can ask copilot to remediate the Local file system IO issue using the below command:

```bash
Please execute #file:[YourPromptCreationFileName].md using "Local file system IO" as "Technology X" and "Azure Blob Storage" as "Technology Y".

You can use the AppCat report #file:[YourAppCatFileName].appcat.json  and look at issue Local.0003 to see specific locations in the solution where Local file system IO need to be replaced.
```

![Blob Command](./images/blobcommand.png)

This will generate a new prompt for code remediation on Azure Blob Storage integration.

![Generated Prompt For Blob](./images/generatedpromptblob.png)

**Example**, please see the full copilot generated prompt for Azure Blob Storage integration [BlobStorage Prompt](./prompts/CopilotGeneratedPrompts/local-filesystem-to-azure-blob-storage.netfx.prompt.md) 

Now, we have successfully created a prompt for Azure Blob Storage integration. Let's proceed with **STEP 2** i.e., the execution of the prompt to remediate the Local file system IO issue.

See the steps [Run-BlobStorage-Technology-Specific-Prompt](Run-BlobStorage-Technology-Specific-Prompt.md)

 ## 6.3 Azure Redis Cache:

 Let’s prepare an application which has Local caching references and dependencies in the code.

![Local Caching](./images/localcaching.png)

Let's see the AppCat report findings related to Azure  Redis Cache:

![Appcat Findings Redis](./images/appcatfindingsredis.png)

Let's proceed with STEP 1 i.e., [Create-Technology-Specific-Prompt](Create-Technology-Specific-Prompt.md) to attach necessary files which will be used to create prompt for Azure Redis Cache.

Once the files in copilot chat are attached, tell copilot to remediate and apply the code changes for the AppCat issues related to Local caching (i.e., Technology X) issue using Azure Redis Cache (i.e., Technology Y) as a next step.
In background copilot will follow the guidance provided in the instruction file and will generate a new prompt which will be followed to remediate the specific issues.

**Example**, we can ask copilot to remediate the Local caching issue using the below command:

```bash
Please execute #file:[YourPromptCreationFileName].md using "Local caching" as "Technology X" and "Azure Redis Cache" as "Technology Y".

You can use the AppCat report #file:[YourAppCatFileName].appcat.json  and look at issue Scale.0002 to see specific locations in the solution where Local caching need to be replaced.
```

![Redis Command](./images/rediscommand.png)

This will generate a new prompt for code remediation on Azure Redis Cache integration.

![Generated Prompt For Redis](./images/generatedpromptredis.png)

**Example**, please see the full copilot generated prompt for Azure Redis Cache integration [Redis Prompt](./prompts/CopilotGeneratedPrompts/local-caching-to-azure-redis-cache.prompt.md) 

Now, we have successfully created a prompt for Azure Redis Cache integration. Let's proceed with **STEP 2** i.e., the execution of the prompt to remediate the Local caching issue.

See the steps [Run-RedisCache-Technology-Specific-Prompt](Run-RedisCache-Technology-Specific-Prompt.md)

## 6.4 Microsoft Entra ID:

Let’s prepare an application which has Windows auth for authenticating users references and dependencies in the code.

![Windows Auth](./images/winauthcode.png)

Let's see the AppCat report findings related to Entra ID:

![Appcat Findings Windows Auth](./images/winauth.png)

Let's proceed with STEP 1 i.e., [Create-Technology-Specific-Prompt](Create-Technology-Specific-Prompt.md) to attach necessary files which will be used to create prompt for Microsoft Entra ID.

Once the files in copilot chat are attached, tell copilot to remediate and apply the code changes for the AppCat issues related to Windows authentication (i.e., Technology X) issue using Microsoft Entra ID (i.e., Technology Y) as a next step.
In background copilot will follow the guidance provided in the instruction file and will generate a new prompt which will be followed to remediate the specific issues.

**Example**, we can ask copilot to remediate the Windows authentication issue using the below command:

```bash
Please execute #file:[YourPromptCreationFileName].md using "Windows authentication" as "Technology X" and "Microsoft Entra ID" as "Technology Y".

You can use the AppCat report #file:[YourAppCatFileName].appcat.json  and look at issue Identity.0002 to see specific locations in the solution where Windows authentication need to be replaced.
```

![Entra ID Command](./images/entracommand.png)

This will generate a new prompt for code remediation on Microsoft Entra ID integration.

![Generated Prompt For Entra ID](./images/generatedpromptentraid.png)

**Example**, please see the full copilot generated prompt for Microsoft Entra ID integration [Entra ID Prompt](./prompts/CopilotGeneratedPrompts/windows-auth-to-entra-id.netfx.prompt-manually-modified.md) 

Now, we have successfully created a prompt for Microsoft Entra ID integration. Let's proceed with **STEP 2** i.e., the execution of the prompt to remediate the Windows authentication issue.

See the steps [Run-EntraID-Technology-Specific-Prompt](Run-EntraID-Technology-Specific-Prompt.md)

**Note** -

Once the build is completed successfully after each migration, you can check and confirm the running status of your application.
 
#### 7. Guide To Known Issues

1. **msbuild/dotnet build issue**: If you encounter any build issues, please ensure that the correct version of the .NET framework is installed on your machine. Even though it is instructed to copilot in guidance file to use  "msbuild" to build the application post migration, sometime it fails, hence copilot uses "dotnet build" command to build the application.

    ![Build Issues](./images/msbuilderr.png)

2. **Continue option** : Copliot sometimes provides the option to continue the code changes in the same prompt and the execution stops, in that scenario please review the code changes and continue if needed. Copilot works better in smaller scope of commands, so it is recommended to clear the chat and try again with new copilot chat window.

    ![Continue option](./images/continueerr.png)

3. **Claude Sonnet 4 & 3.7** : It is recommended to use the the LLM Claude Sonnet 4 but sometimes copilot fails to execute the code changes in middle of migration, in this scenario, review your changes carefully and use other option like Claude Sonnet 3.7 which also works well.

    ![Claude Sonnet 4](./images/sonnet4.png)

    ![Claude Sonnet 3.7](./images/sonnet37.png)


4. **Manual code changes needed on code/build errors** : Sometimes copilot generates the code changes which are not syntactically correct and build issue occurs, in that scenario, please review the code changes and make the manual changes as needed.

    ![Manual changes for error](./images/manualcng.png)

5. **Visual Studio Code and Visual Studio both IDEs are required** : Visual Studio Code required to execute the commands adding context of the targeted codebase, Visual Studio is required to install nuget packages using nuget package manager which is more user friendly.

    ![Code base VS Code](./images/codebase.png)
    ![Nuget VS](./images/nugetredis.png)

6. **New branch creation** : Copilot code remediation using prompt does not create a new branch like copilot for .net upgrade does, we have to manually create a new branch where coplilot code changes can be performed, later on, we can merge the changes to the main branch.

    ![Branch Creation](./images/branch.png)

7. **Manual Modification on Copilot Generated Prompts** : Sometimes copilot generated prompts may need manual modification to make it more accurate and relevant to the specific code remediation task. It is recommended to review the generated prompt and make necessary modifications before executing it.

    **Example**: Copilot generated a prompt for Microsoft Entra ID integration [Copilot Generated Entra ID Prompt](./prompts/CopilotGeneratedPrompts/windows-auth-to-entra-id.netfx.prompt-copilot.md)
    which included packages that do not work in .net framework, but work in .net core applications, hence we followed manual modification in this scenario to make it work in .net framework before executing it for code remediation.
    See the full modified prompt with updated nuget packages for Microsoft Entra ID integration [Manually Modified Entra ID Prompt](./prompts/CopilotGeneratedPrompts/windows-auth-to-entra-id.netfx.prompt-manually-modified.md)
    
    In conclusion, it’s essential to validate prompts and incorporate contextual adjustments as necessary before proceeding.

### 8. References

1. [Copilot Prompt Engineering](https://learn.microsoft.com/en-us/training/modules/introduction-prompt-engineering-with-github-copilot/2-prompt-engineering-foundations-best-practices)
2. [Azure Key Vault Documentation](https://docs.microsoft.com/en-us/azure/key-vault/)
3. [Azure Blob Storage Documentation](https://docs.microsoft.com/en-us/azure/storage/blobs/)
4. [Azure Redis Cache Documentation](https://docs.microsoft.com/en-us/azure/azure-cache-for-redis/)
5. [Microsoft Entra ID Documentation](https://docs.microsoft.com/en-us/azure/active-directory/)


### 9. Abbreviations


| **Abbreviations**               | **Definition**       
|---------------------------------|----------------------|
| AppCat  | Azure Migrate application and code assessment|
| LLM     | Language Learning Model  |


