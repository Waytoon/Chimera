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

# Chimera Code-Push SDK Integration

As above mentioned, it is easy to integrate Chimera SDK with you current App. But you need to access our manage platform to manage your account to deploy your App with our Code-Push service. 

## Getting Started

1.  Create a free account o [wiredash.io](https://console.wiredash.io/)

2.  Add wiredash to your pubspec.yaml.

   ```
   name: your_flutter_app
   dependencies:
     flutter:
       sdk: flutter
     chimera: ^0.1.0
   ```

3. Integrate the SDK entry-point with you app:

   ```
   import 'package:flutter/material.dart';
   import 'package:wiredash/wiredash.dart';
   
   class MyApp extends StatelessWidget {
     // It's important that Wiredash and your root Material- / Cupertino- / WidgetsApp
     // share the same Navigator key.
     final _navigatorKey = GlobalKey<NavigatorState>();
   
     @override
     Widget build(BuildContext context) {
       return Wiredash(
         projectId: 'YOUR-PROJECT-ID',
         secret: 'YOUR-SECRET',
         navigatorKey: _navigatorKey,
         child: MaterialApp(
           navigatorKey: _navigatorKey,
           title: 'Flutter Demo',
           home: YourSuperDuperAwesomeApp(),
         ),
       );
     }
   }
   ```

4. Launch & test  your App as the normal way you are working on.



### Methods

*Note: `access key` here refers to an AppCenter API Token.*

- Under construction 

### Error Handling

- Under construction
