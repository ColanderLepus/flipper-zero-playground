## Project Overview

This directory serves as a knowledge base *about* Flipper Zero application development. It contains two primary guides:

1.  `flipper_hello_world_guide.md`: Details the general setup of the Flipper Zero development environment and the creation of a basic "Hello World" application that prints to the device's log.
2.  `hello_flipper_ui_tutorial.md`: Provides an in-depth, step-by-step guide on creating a Flipper Zero UI application (`hello_flipper_ui`) that displays text directly on the device's screen using a `ViewPort`.

No actual Flipper Zero application development takes place directly within this directory; it functions as a repository for instructional context.

## Primary Resources

This project also includes a `resources.md` file that contains a list of primary resources for Flipper Zero development. These resources should be the first point of reference for any research. The resources include:

-   **User Interface:** A guide to the Flipper Zero's UI components.
-   **Message Queue:** A tutorial on using message queues for event-driven programming.
-   **uFBT:** The official documentation for the micro Flipper Build Tool.


## Building and Running

The guides outline the key commands for setting up the development environment, building, and deploying Flipper Zero applications using `uFBT`.

*   **`ufbt create APPID=<app_id>`**: Generates a new Flipper Zero application template within the current directory (e.g., `hello_flipper_ui`).
*   **`ufbt`**: Builds the Flipper Zero application, creating a `.fap` file in the `dist` folder.
*   **`ufbt launch`**: Deploys and runs the built application on a connected Flipper Zero device.
*   **`ufbt vscode_dist`**: Sets up VS Code integration for enhanced building and debugging capabilities.

## Development Conventions

This project encourages the use of Visual Studio Code for development due to its robust integration with `uFBT`. The primary language for Flipper Zero applications is C. For simple UI applications, the `ViewPort`-only approach is demonstrated, directly managing display and input without the need for `View` or `ViewDispatcher` abstractions. The `uFBT` tool automates the build process, ensuring consistency and ease of deployment.