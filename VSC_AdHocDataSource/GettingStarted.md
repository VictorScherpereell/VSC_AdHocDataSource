# Getting Started with Skyline DataMiner DevOps

Welcome to the Skyline DataMiner DevOps environment!  
This quick-start guide will help you get up and running. It was auto-generated based on the initial project setup during creation.  
For more details and comprehensive instructions, please visit [DataMiner Docs](https://docs.dataminer.services/).

## Creating a DataMiner Application Package

This project was configured to create a `.dmapp` file every time you build the project.  
When you compile or build the project, you will find the generated `.dmapp` in the standard output folder, typically the `bin` folder of your project.

When you publish the project (see Publishing topic below), a corresponding item will be created in the online DataMiner Catalog.

## Migrating to a Multi-Artifact DataMiner Application Package

If you need to combine additional components in your `.dmapp` file, you should:

1. Open the `VSC_AdHocDataSource.csproj` file and ensure the `<GenerateDataminerPackage>` property is set to `False`.

2. Right-click your solution and select **Add > New Project**.

3. Select the **Skyline DataMiner Package Project** template.

Follow the provided **Getting Started** guide in the new project for further instructions.

## Publishing to the Catalog

This project was created with support for publishing to the DataMiner Catalog.  
You can publish your artifact either manually via the Visual Studio IDE or by setting up a CI/CD workflow.

## Publishing to the Catalog with Complete CI/CD Workflow

This project includes a comprehensive GitHub workflow that adheres to Skyline Communications' quality standards, including static code analysis, custom validation, and unit testing.

### Prerequisite

You need a **SonarCloud Organization**. If you don’t have one, you can create it [here](https://sonarcloud.io/create-organization).

### Steps

1. Create a GitHub repository by going to **Git > Create Git Repository**, selecting GitHub, and filling in the wizard before clicking **Create and Push**.

1. In GitHub, go to the *Actions* tab.

1. Click the workflow run that failed (usually called *Add project files*).

1. Click the "build" step that failed and read the failing error.

   ``` text
   Error: DATAMINER_TOKEN is not set. Release not possible!
   Please create or re-use an admin.dataminer.services token by visiting: https://admin.dataminer.services/.
   Navigate to the right Organization then go to Keys and create/find a key with permissions to Register Catalog Items.
   Copy the value of the token.
   Then set a DATAMINER_TOKEN secret in your repository settings: **Dynamic Link**
   ```

   You can use the links from the actual error to better address the next couple of steps.

1. Obtain an **Organization Key** from [admin.dataminer.services](https://admin.dataminer.services/) with the following scopes:
   - **Register Catalog items**
   - **Read Catalog items**

1. Add the key as a secret in your GitHub repository, by navigating to **Settings > Secrets and variables > Actions** and creating secrets or variables with the required names.

1. Re-run the workflow.

The following secrets and variables will have been added to your repository after all issues are resolved:

| Name            | Type    | Description                                        | Setup Guide                                                                                 |
|-----------------|---------|----------------------------------------------------|---------------------------------------------------------------------------------------------|
| `DATAMINER_TOKEN` | Secret  | Organization key for publishing to the Catalog   | Obtain from [admin.dataminer.services](https://admin.dataminer.services/) and add it as a secret. |
| `SONAR_TOKEN`    | Secret  | Token for SonarCloud authentication               | Obtain from [SonarCloud Security](https://sonarcloud.io/account/security) and add it as a secret.  |
| `SONAR_NAME`     | Variable | SonarCloud project ID                            | Visit [SonarCloud](https://sonarcloud.io/projects/create), copy the project ID, and add it as a variable. |

### Releasing a Version

1. Navigate to the **<> Code** tab in your GitHub repository.

1. In the menu on the right, select **Releases**.

1. Create a new release, select the desired version as a **tag**, and provide a title and description.

> [!NOTE]
> The description will be visible in the DataMiner Catalog.
