# Setting Up Your Development Environment

To develop applications for the Flipper Zero, you need to install and configure a few tools. This guide will walk you through setting up everything you need on a Windows computer.

### 1. Visual Studio Code

VS Code is the recommended code editor for Flipper Zero development. It provides a great editing experience and has an integrated terminal that we will use for all subsequent commands.

*   **Download and install it from the [official website](https://code.visualstudio.com/).**

### 2. Python

Python is required to run the `uFBT` build tool.

*   **Install Python:** The recommended method is to use the official installer from the [python.org website](https://www.python.org/).
*   **Configure PATH during Installation:** When using the official installer, make sure to check the box that says **"Add `python.exe` to PATH"**. This is the most convenient way to set up your environment. It configures your system to recognize the `python` command and, just as importantly, automatically adds the `Scripts` folder to your `PATH`. This second part is what allows you to run tools like `ufbt` directly from your terminal after you install them.
*   **Verify the installation:** After installation, open a *new* Command Prompt or PowerShell window and type `py --version`. You should see the installed Python version.

### 3. uFBT (micro Flipper Build Tool)

`uFBT` is the command-line tool used to create, build, and deploy your Flipper Zero applications.

*   **Install uFBT:** Once Python is installed, open a Command Prompt or PowerShell and run the following command:
    ```bash
    pip install --upgrade ufbt
    ```
*   **How it Works:** The `pip` command installs the `ufbt.exe` executable inside Python's `Scripts` folder. For your terminal to find and run `ufbt` simply by typing its name, that specific `Scripts` folder must be listed in your system's `PATH` environment variable.

    The "Add Python to PATH" option in the official installer usually handles this for you by adding both directories. However, if you install `ufbt` and get a "command not found" error, it's almost certainly because the `Scripts` folder is not in your `PATH`, and you will need to add it manually.

Once you have completed these steps, your environment is ready.

# Creating an Application

Once your environment is set up, you can create a new Flipper Zero application.

1.  **Open Your Project Folder in VS Code:**
    Create a new folder for your project (e.g., `C:\FlipperProjects\my_new_app`) and open it in Visual Studio Code (`File > Open Folder...`).

2.  **Generate a New Application:**
    Open the integrated terminal in VS Code (`View > Terminal`). You should already be in your project's root directory. Use `ufbt create` to generate a new application template. Replace `<app_id>` with a unique identifier for your application.

    ```bash
    ufbt create APPID=<app_id>
    ```

    This command will create the application manifest (`application.fam`) and its main source file (`<app_id>.c`) directly within your current directory.

3.  **Set up VSCode Integration:**
    For a better development experience, you can integrate your project with Visual Studio Code. Run the following command from your application's root directory in the integrated terminal:

    ```bash
    ufbt vscode_dist
    ```

    This command will generate VSCode configuration files that allow you to build and debug your application directly from the IDE. You can then use the provided launch (Ctrl+Shift+B) and debugging (Ctrl+Shift+D) configurations.

### Understanding the Generated Files

The `ufbt create` command generates two key files:

*   **`application.fam`**: The application manifest, which contains metadata about your app.
*   **`<app_id>.c`**: The main source file.

The generated `.c` file contains a simple "Hello World" implementation that prints a message to the Flipper Zero's log using `FURI_LOG_I`. You can view this log output by running your application with `ufbt launch --log` or through the qFlipper desktop application.