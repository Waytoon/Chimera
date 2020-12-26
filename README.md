# Flutter CodePush - Chimera

Chimera is a super SDK for flutter Code-Push. 

it would provide a cloud service that enables flutter/dart developers to deploy mobile app updates directly to their users' devices. It works by acting as a central repository that developers can publish updates to apps can query for updates from (using provided client SDK for flutter app include iOS/Android platform). This allows you to have a more deterministic and direct engagement model with your userbase, when addressing bugs and/or adding small features that don't require you to re-build a binary and re-distribute it through the respective app stores.

To get started using Chimera, refer to our documentation, otherwise, read the following steps if you'd like to build/contribute to the project from source.

## Dev Setup

- Download SDK from this link: 
- Put the SDK into your App Dev lib as below shows:



- When you debug your App, to run `test test` to debug the App.
- Run `npm run build` to build the management SDK for testing.
- Run `npm run build:release` to build the release version of management SDK.

### Running Tests

- To run tests, run `npm run test` from the root of the project.
- You can use debug mode for tests with `.vscode/launch.json` file.

### Coding Conventions

- Use double quotes for strings
- Use four space tabs
- Use `camelCase` for local variables and imported modules, `PascalCase` for types, and `dash-case` for file names

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

# Flutter CodePush Management SDK 

A JavaScript library for programmatically managing your CodePush account (e.g. creating apps, promoting releases), which allows authoring Node.js-based build and/or deployment scripts, without needing to shell out to the [App Center CLI](https://github.com/microsoft/appcenter-cli).

## Getting Started

1. Create a token to authenticate with the CodePush server using the following [App Center CLI](https://github.com/microsoft/appcenter-cli) command:

   ```
   appcenter tokens create -d "DESCRIPTION_OF_THE_TOKEN"
   ```

   Please copy your `API Token` and keep it secret. You won't be able to see it again.

2. Install the management SDK by running `npm install code-push --save`

3. Import it using one of the following statement: (using ES6 syntax as applicable):

   - On commonjs environments:

   ```
   const CodePush = require("code-push");
   ```

   - Using ES6 syntax with tsconfig.json:

   ```
   import CodePush from "code-push";
   ```

4. Create an instance of the `CodePush` class, passing it the `API Token` you created or retrieved in step #1:

   ```
   const codePush = new CodePush("YOUR_API_TOKEN");
   ```

5. Begin automating the management of your account! For more details on what you can do with this `codePush` object, refer to the API reference section below.

## API Reference

The `code-push` module exports a single class (typically referred to as `CodePush`), which represents a proxy to the CodePush account management REST API. This class has a single constructor for authenticating with the CodePush service, and a collection of instance methods that correspond to the commands in the [App Center CLI](https://github.com/microsoft/appcenter-cli), which allow you to programmatically control every aspect of your CodePush account.

### Constructors

- **CodePush(accessKey: string)** - Creates a new instance of the CodePush management SDK, using the specified access key to authenticated with the server.

### Methods

*Note: `access key` here refers to an AppCenter API Token.*

- **addAccessKey(description: string): Promise<AccessKey>** - Creates a new access key with the specified description (e.g. "VSTS CI").
- **addApp(name: string, os: string, platform: string, manuallyProvisionDeployments: boolean = false): Promise<App>** - Creates a new CodePush app with the specified name, os, and platform. If the default deployments of "Staging" and "Production" are not desired, pass a value of true for the manuallyProvisionDeployments parameter.
- **addCollaborator(appName: string, email: string): Promise<void>** - Adds the specified CodePush user as a collaborator to the specified CodePush app.
- **addDeployment(appName: string, deploymentName: string): Promise<Deployment>** - Creates a new deployment with the specified name, and associated with the specified app.
- **clearDeploymentHistory(appName: string, deploymentName: string): Promise<void>** - Clears the release history associated with the specified app deployment.
- **getAccessKey(accessKey: string): Promise<AccessKey>** - Retrieves the metadata about the specific access key.
- **getAccessKeys(): Promise<AccessKey[]>** - Retrieves the list of access keys associated with your CodePush account.
- **getApp(appName: string): Promise<App>** - Retrieves the metadata about the specified app.
- **getApps(): Promise<App[]>** - Retrieves the list of apps associated with your CodePush account.
- **getCollaborators(appName: string): Promise<CollaboratorMap>** - Retrieves the list of collaborators associated with the specified app.
- **getDeployment(appName: string, deploymentName: string): Promise<Deployment>** - Retrieves the metadata for the specified app deployment.
- **getDeploymentHistory(appName: string, deploymentName: string): Promise<Package[]>** - Retrieves the list of releases that have been made to the specified app deployment.
- **getDeploymentMetrics(appName: string, deploymentName: string): Promise<DeploymentMetrics>** - Retrieves the installation metrics for the specified app deployment.
- **getDeployments(appName: string): Promise<Deployment[]>** - Retrieves the list of deployments associated with the specified app.
- **patchRelease(appName: string, deploymentName: string, label: string, updateMetadata: PackageInfo): Promise<void>** - Updates the specified release's metadata with the given information.
- **promote(appName: string, sourceDeploymentName: string, destinationDeploymentName: string, updateMetadata: PackageInfo): Promise<Package>** - Promotes the latest release from one deployment to another for the specified app and updates the release with the given metadata.
- **release(appName: string, deploymentName: string, updateContentsPath: string, targetBinaryVersion: string, updateMetadata: PackageInfo): Promise<Package>** - Releases a new update to the specified deployment with the given metadata.
- **removeAccessKey(accessKey: string): Promise<void>** - Removes the specified access key from your CodePush account.
- **removeApp(appName: string): Promise<void>** - Deletes the specified CodePush app from your account.
- **removeCollaborator(appName: string, email: string): Promise<void>** - Removes the specified account as a collaborator from the specified app.
- **removeDeployment(appName: string, deploymentName: string): Promise<void>** - Removes the specified deployment from the specified app.
- **renameApp(oldAppName: string, newAppName: string): Promise<void>** - Renames an existing app.
- **renameDeployment(appName: string, oldDeploymentName: string, newDeploymentName: string): Promise<void>** - Renames an existing deployment within the specified app.
- **rollback(appName: string, deploymentName: string, targetRelease?: string): Promise<void>** - Rolls back the latest release within the specified deployment. Optionally allows you to target a specific release in the deployment's history, as opposed to rolling to the previous release.
- **transferApp(appName: string, email: string): Promise<void>** - Transfers the ownership of the specified app to the specified account.

### Error Handling

When an error occurs in any of the methods, the promise will be rejected with a CodePushError object with the following properties:

- **message**: A user-friendly message that describes the error.

- statusCode

  : An HTTP response code that identifies the category of error:

  - **CodePush.ERROR_GATEWAY_TIMEOUT**: A network error prevented you from connecting to the CodePush server.
  - **CodePush.ERROR_INTERNAL_SERVER**: An error occurred internally on the CodePush server.
  - **CodePush.ERROR_NOT_FOUND**: The resource you are attempting to retrieve does not exist.
  - **CodePush.ERROR_CONFLICT**: The resource you are attempting to create already exists.
  - **CodePush.ERROR_UNAUTHORIZED**: The access key you configured is invalid or expired.
