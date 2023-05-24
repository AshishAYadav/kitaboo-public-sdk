# @ashishayadav/kitaboo-pwa-sdk

This Node module provides integration with the Kitaboo-PWA-SDK for Angular applications.

## Installation

To install a private package from a custom registry such as "https://npm.pkg.github.com", you need to configure your npm client to authenticate with the registry. Here's how you can install the `@ashishayadav/kitaboo-pwa-sdk` package from the GitHub package registry:

1. Make sure you have the necessary credentials and access to the private package in the GitHub package registry.

2. Create a `.npmrc` file in the root directory of your project (if it doesn't already exist).

3. Open the `.npmrc` file and add the following line, replacing `<GITHUB_USERNAME>` and `<GITHUB_TOKEN>` with your actual GitHub username and a personal access token that has the appropriate permissions to access the package:


    ```
     @${OWNER}:registry=https://npm.pkg.github.com
     //npm.pkg.github.com/:_authToken=${TOKEN}
    ```

    For example:

    ```
    @ashishayadav:registry=https://npm.pkg.github.com
    //npm.pkg.github.com/:_authToken=12345abcde
    ```

    Save the `.npmrc` file.

4. Run the following command to install the package, specifying the registry URL explicitly:



    To install the module, run the following command:
    ```
    npm install @ashishayadav/kitaboo-pwa-sdk --registry=https://npm.pkg.github.com
    ```

    This command tells npm to install the `@ashishayadav/kitaboo-pwa-sdk` package from the GitHub package registry.

Make sure to replace `<GITHUB_USERNAME>` and `<GITHUB_TOKEN>` with your actual GitHub username and access token. Also, update the package version (`1.0.0-alpha.1`) if needed.

By configuring the `.npmrc` file and specifying the custom registry URL, you can authenticate with the GitHub package registry and install the private package successfully.

## Usage

### App Module Configuration

In your app module, import the CUSTOM_ELEMENTS_SCHEMA from @angular/core and add it to the schemas array to suppress custom HTML tag errors:
```
import { CUSTOM_ELEMENTS_SCHEMA } from '@angular/core';

@NgModule({
  schemas: [
    CUSTOM_ELEMENTS_SCHEMA
  ],
  // Other module configuration
})
export class AppModule { }
```
### Component Integration

In your component TypeScript file, import the necessary functions from 'kitaboo' and initialize the Kitaboo-PWA-SDK:
```
import { kitaboo, kitabooDestroy } from '@ashishayadav/kitaboo-pwa-sdk';
import { Component, ElementRef, OnDestroy, ViewChild } from '@angular/core';

@Component({
  // Component configuration
})
export class YourComponent implements OnDestroy {
  usertoken: string = '';
  bookID: string = '';
  language: string = '';
  CONFIG: any = {}; //use kitaboo provided config file
  SERVICEURL: any = {} //use kitaboo provided Service file

  constructor() {
    kitaboo(this.CONFIG, this.SERVICEURL); // initialize kitaboo-pwa-sdk
    this.bookID = 'BOOK_ID';
    this.usertoken = 'USER_TOKEN';
    this.language = 'en-us' | es';
  }

  kitabooEvent(event: any) {
    console.log(event); //process events here
  }

  ngOnDestroy(): void {
    kitabooDestroy(); // destroy kitaboo-pwa-sdk
  }
}
```
### Component HTML Usage

In your component HTML file, use the Kitaboo-PWA-SDK custom element:
```
<kitaboo-reader (kitabooEvent)="kitabooEvent($event)" [usertoken]="usertoken" [bookID]="bookID" [language]="language"></kitaboo-reader>
```
### Angular.json Configuration

Update your angular.json file to include the Kitaboo-PWA-SDK assets in the build:
```
{
  "projects": {
    "your-project-name": {
      "architect": {
        "build": {
          "options": {
            "assets": [
              {
                "glob": "**/*",
                "input": "./node_modules/@ashishayadav/kitaboo-pwa-sdk/sdk/",
                "output": "./assets/kitaboo/",
                "ignore": ["main.js", "vendor.js", "runtime.js", "polyfills.js", "config/*", "services/*", "node_modules_firebase_compat_*"]
              },
              {
                "glob": "node_modules_firebase_compat_*.js",
                "input": "./node_modules/@ashishayadav/kitaboo-pwa-sdk/sdk/",
                "output": "./"
              }
            ]
          }
        }
      }
    }
  }
}
```
Note: Ensure that you do not change the /assets/kitaboo path.

That's it! You have successfully integrated the Kitaboo-PWA-SDK module into your Angular application.

For more information on using the Kitaboo-PWA-SDK, refer to the official documentation or contact the Kitaboo support team.
