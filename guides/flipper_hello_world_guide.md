### Introduction

This guide will walk you through building and deploying the default "Hello World" application for the Flipper Zero.

### Prerequisites

Before you begin, please follow the [Setup and Create Guide](setup_and_create_guide.md) to:
1.  Set up your development environment.
2.  Create a new application. For this guide, you can use `hello_flipper` as your `APPID`.

After following the guide, you will have a folder containing a pre-made "Hello World" application.

### Step 1: Build the Application

1.  **Build with uFBT:**
    From within your application's directory, run the following command in the integrated terminal in VS Code to build your application:

    ```bash
    ufbt
    ```

    A successful build will show various compilation messages and will ultimately create a `.fap` file (Flipper Application Package) in the `dist` folder within your application's directory (e.g., `C:\FlipperProjects\my_hello_world_app\dist\hello_flipper.fap`).

### Step 2: Deploy the Application

For instructions on how to deploy your application to your Flipper Zero, please see the [Deployment Guide](deployment_guide.md).

### Conclusion

You have successfully created, built, and deployed your first Flipper Zero application! You can now modify the generated source code (`hello_flipper.c`) to customize your application. For more advanced development, you can explore the official Flipper Zero developer documentation and other community resources, including our [Primary Resources](resources.md) file.
