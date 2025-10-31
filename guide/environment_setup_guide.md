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
