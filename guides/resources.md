# Flipper Zero Development Resources

This file contains a curated list of primary resources for Flipper Zero application development. These should be consulted first when researching related topics.

## Official Documentation

- **Link:** [https://developer.flipper.net/flipperzero/doxygen/index.html](https://developer.flipper.net/flipperzero/doxygen/index.html)
- **Description:** The official Doxygen documentation for the Flipper Zero firmware. This is the most comprehensive and authoritative source for API references, data structures, and detailed technical information.

## uFBT (micro Flipper Build Tool)

- **Link:** [https://github.com/flipperdevices/flipperzero-ufbt](https://github.com/flipperdevices/flipperzero-ufbt)
- **Description:** The official repository for the `uFBT` tool. This is the primary tool for building, deploying, and debugging Flipper Zero applications. The repository's README provides comprehensive instructions on installation, usage, and VS Code integration.

## User Interface

- **Link:** [https://github.com/jamisonderek/flipper-zero-tutorials/wiki/User-Interface](https://github.com/jamisonderek/flipper-zero-tutorials/wiki/User-Interface)
- **Description:** This guide covers the fundamental UI components available in the Flipper Zero SDK, including `ViewPort`, `Canvas`, `ViewDispatcher`, `View`, and `Modules`. It provides a high-level overview of how to handle display and input, manage different UI screens, and structure complex UI applications.

## Message Queue

- **Link:** [https://github.com/jamisonderek/flipper-zero-tutorials/wiki/Message-Queue](https://github.com/jamisonderek/flipper-zero-tutorials/wiki/Message-Queue)
- **Description:** This tutorial explains the use of `FuriMessageQueue` for event-driven programming in Flipper Zero applications. It details how to send and receive messages between different parts of an application, enabling non-blocking communication and better application structure.

## LED Control

- **Basic Blinking Example:**
  A simple code snippet demonstrating how to blink an LED using `furi_hal_light_set` and `furi_delay_ms`.

  ```c
  #include <furi.h>
  #include <furi_hal_light.h>

  // Example function to blink the red LED
  void blink_red_led_simple() {
      // Turn the red LED on to full brightness
      furi_hal_light_set(LightRed, 255);
      furi_delay_ms(500); // Wait 500ms

      // Turn the red LED off
      furi_hal_light_set(LightRed, 0);
      furi_delay_ms(500); // Wait 500ms
  }
  ```

- **Advanced LED Control (Cupprum/Blinker):**
  - **Link:** [https://github.com/Cupprum/Blinker](https://github.com/Cupprum/Blinker)
  - **Description:** A comprehensive example demonstrating various LED control techniques, including hardware-controlled blinking and more advanced patterns. This repository can serve as a reference for complex LED implementations.

## JavaScript Development

- **Link:** [https://developer.flipper.net/flipperzero/doxygen/js.html](https://developer.flipper.net/flipperzero/doxygen/js.html)
- **Description:** The main documentation page for JavaScript application development on the Flipper Zero. It covers the basics, API, and provides examples.