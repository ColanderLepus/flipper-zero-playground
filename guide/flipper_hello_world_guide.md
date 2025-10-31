### Introduction

This guide will walk you through creating your very own "Hello World" application for the Flipper Zero. We will use the micro Flipper Build Tool (uFBT) to generate a new project and simplify the development process. This guide assumes you will be using Visual Studio Code and its integrated terminal for a streamlined workflow.

### Prerequisites

Before you begin, you need to install the following software on your Windows computer:

*   **Python:** Python is required for `uFBT`. You have two main options for installation:
    *   **Option 1: Using the Official Installer (Recommended for beginners)**
        Download and install Python from the [official website](https://www.python.org/). During installation, make sure to check the box that says "Add Python to PATH" or "Install launcher for all users (recommended)". This is crucial for `ufbt` to work correctly. After installation, open a Command Prompt and verify Python is installed by typing `python --version` or `py --version`. You should see the installed Python version.
    *   **Option 2: Using Winget (Windows Package Manager)**
        If you have Winget installed (it comes pre-installed with modern Windows versions), you can install Python by opening a Command Prompt or PowerShell and running:
        ```bash
        winget install Python.Python.3.10 # Or your preferred version
        ```
        **Note on PATH:** While `winget` installations often handle PATH configuration automatically, it's always a good practice to verify. After installation, open a *new* Command Prompt or PowerShell window and type `python --version` or `py --version`. If the command is not recognized, you may need to manually add Python to your system's PATH environment variables. You can find guides online for "how to add Python to PATH Windows".

**A Note on the `Scripts` Folder and PATH:**

When you use `pip` to install packages, any command-line tools they include (like `ufbt.exe`) are placed in a `Scripts` folder inside your Python installation directory. For you to be able to type `ufbt` directly in your terminal instead of `py -m ufbt`, this `Scripts` folder must be included in your system's `PATH` environment variable. The standard Python installer has an option to do this for you, but it's a good thing to double-check if you run into issues.
*   **Visual Studio Code:** This guide uses Visual Studio Code as the primary code editor. Download it from the [official website](https://code.visualstudio.com/). All commands should be run from the integrated terminal in VS Code.

### Step 1: Set Up the Development Environment

1.  **Install uFBT:**
    Open a Command Prompt or PowerShell (or the integrated terminal in VS Code) and run the following command to install uFBT using pip, the Python package manager:

    ```bash
    py -m pip install --upgrade ufbt
    ```

    uFBT is a tool that automates the process of building and deploying Flipper Zero applications.

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

### Step 4: Deploy the Application to Your Flipper Zero

There are two ways to deploy the application to your Flipper Zero:

**Method 1: Using `ufbt launch` (Recommended)**

1.  **Connect Your Flipper Zero:**
    Connect your Flipper Zero to your computer using a USB cable.

2.  **Launch the Application:**
    From within your application's directory, run the following command in the integrated terminal in VS Code:

    ```bash
    ufbt launch
    ```

    This command will automatically build the application (if it hasn't been built already) and transfer it to your Flipper Zero's SD card. The application will then launch on your device.

**Method 2: Manual Deployment**

1.  **Copy the `.fap` File:**
    After building the application with `ufbt`, you will find a `.fap` file in the `dist` directory of your application (e.g., `C:\FlipperProjects\my_hello_world_app\dist\hello_flipper.fap`).

2.  **Transfer to SD Card:**
    Copy this `.fap` file to the `apps/Misc` folder on your Flipper Zero's SD card. You can do this by removing the SD card from your Flipper Zero and using a card reader, or by using the qFlipper application to manage files on your device.

3.  **Run the Application:**
    On your Flipper Zero, navigate to `Applications` -> `Misc` and select your "Hello World" application to run it.

### Conclusion

You have successfully created, built, and deployed your first Flipper Zero application! You can now modify the generated source code (`hello_flipper.c`) to customize your application. For more advanced development, you can explore the official Flipper Zero developer documentation and other community resources.
