### Introduction

This guide will walk you through creating your very own "Hello World" application for the Flipper Zero. We will use the micro Flipper Build Tool (uFBT) to generate a new project and simplify the development process. This guide assumes you will be using Visual Studio Code and its integrated terminal for a streamlined workflow.

### Environment Setup

Before you begin, you need to set up your development environment. Please follow the [Environment Setup Guide](environment_setup_guide.md) to install all the necessary tools.

### Step 2: Create Your "Hello World" Application

1.  **Open Your Project Folder in VS Code:**
    Create a new folder for your project (e.g., `C:\FlipperProjects\my_hello_world_app`) and open it in Visual Studio Code (`File > Open Folder...`).

2.  **Generate a New Application:**
    Open the integrated terminal in VS Code (`View > Terminal`). You should already be in your project's root directory. Use `ufbt create` to generate a new application template. Replace `<app_id>` with a unique identifier for your application, for example, `hello_flipper`.

    ```bash
    ufbt create APPID=hello_flipper
    ```

    This command will create the application manifest (`application.fam`) and its main source file (`hello_flipper.c`) directly within your current directory. **Note:** The generated `hello_flipper.c` file already contains a basic "Hello World" implementation using `FURI_LOG_I` to print messages to the Flipper Zero's internal log.

3.  **Set up VSCode Integration:**
    For a better development experience, you can integrate your project with Visual Studio Code. Run the following command from your application's root directory in the integrated terminal:

    ```bash
    ufbt vscode_dist
    ```

    This command will generate VSCode configuration files that allow you to build and debug your application directly from the IDE. You can then use the provided launch (Ctrl+Shift+B) and debugging (Ctrl+Shift+D) configurations.

### Step 3: Build the Application

1.  **Build with uFBT:**
    From within your application's directory, run the following command in the integrated terminal in VS Code to build your application:

    ```bash
    ufbt
    ```

    A successful build will show various compilation messages and will ultimately create a `.fap` file (Flipper Application Package) in the `dist` folder within your application's directory (e.g., `C:\FlipperProjects\my_hello_world_app\dist\hello_flipper.fap`).

### Step 4: Deploy the Application

For instructions on how to deploy your application to your Flipper Zero, please see the [Deployment Guide](deployment_guide.md).

### Conclusion

You have successfully created, built, and deployed your first Flipper Zero application! You can now modify the generated source code (`hello_flipper.c`) to customize your application. For more advanced development, you can explore the official Flipper Zero developer documentation and other community resources.
