# Setting Up Your Development Environment

To develop applications for the Flipper Zero, you need to install and configure a few tools. This guide will walk you through setting up everything you need on a Windows computer.

### 1. Visual Studio Code

VS Code is the recommended code editor for Flipper Zero development. It provides a great editing experience and has an integrated terminal that we will use for all subsequent commands.

*   **Download and install it from the [official website](https://code.visualstudio.com/).**

### 2. Python

Python is required to run the `uFBT` build tool.

*   **Install Python:** The recommended method is to use the official installer from the [python.org website](https://www.python.org/).
*   **IMPORTANT:** During installation, make sure to check the box that says **"Add Python to PATH"**. This is crucial for the `uFBT` tool to work correctly in the next step.
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