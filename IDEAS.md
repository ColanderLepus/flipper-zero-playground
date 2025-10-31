# Project Ideas

This file contains a list of ideas for future applications and guides to add to this project.

## Applications

*   **Multi-View Application:**
    *   **Goal:** Create an application that uses multiple views (screens) and allows the user to navigate between them. This will be a step up from the single-screen `hello_flipper_ui` example.
    *   **Key Concepts:** This will involve using the `ViewDispatcher` to manage different `View` objects.
    *   **Research:** The "User Interface" guide listed in our [Primary Resources](guide/resources.md) should contain the necessary documentation on `ViewDispatcher` and `View`.

*   **Blinking LED Application:**
    *   **Goal:** Create a simple application that makes the Flipper Zero's LED blink. This is a fundamental hardware interaction example.
    *   **Key Concepts:** This will involve using Flipper Zero's GPIO (General Purpose Input/Output) functions to control the LED.
    *   **Research:** Look into `furi_hal_gpio` functions and examples for LED control.

*   **Reading Button Input:**
    *   **Goal:** Create an application that displays the name of the button being pressed on the screen (e.g., "Up", "Down", "OK").
    *   **Key Concepts:** This involves handling `InputEvent` data from the message queue and mapping `InputKey` enums to strings.
    *   **Research:** Expand on the input handling already present in the `hello_flipper_ui` application.

*   **Simple Counter:**
    *   **Goal:** Create a multi-view application where one view displays a number, and buttons can increment, decrement, and reset the counter.
    *   **Key Concepts:** State management (storing the counter value), passing data between views, and handling multiple input types.
    *   **Research:** Combine knowledge from the multi-view and button input projects.

## Bucket of Unstructured Thoughts

A place to park ideas before they are fully fleshed out.

*   **Vibration Motor Control:** An app to turn the vibration motor on and off.
*   **Basic Animation:** An app that moves a small icon or shape around the screen, likely using `furi_timer` to trigger redraws.
*   **Saving Data to a File:** A simple "notes" app that can save text to the SD card, introducing the storage and file system APIs.
*   **Using a Submenu:** An app that uses the built-in submenu module to select from a list of options (e.g., choosing an LED blink pattern).