# Project: Flipper Zero Playground

## 1. Core Purpose

This repository serves two main functions:
- **Application Showcase:** It hosts a collection of Flipper Zero applications, starting from basic examples and intended to grow in complexity.
- **Educational Resource:** It provides a set of step-by-step guides that teach beginners how to build the applications contained in this repository from scratch.

## 2. Key Components

### 2.1. Instructional Guides (`guide/`)

This directory contains all the documentation. The guides are designed to be followed in order.

-   `setup_and_create_guide.md`: Covers the setup of the development environment (VS Code, Python, uFBT) and how to create a new application.
-   `flipper_hello_world_guide.md`: Details the creation of the `hello-flipper` application.
-   `hello_flipper_ui_tutorial.md`: Details the creation of the `hello-flipper-ui` application.
-   `deployment_guide.md`: Explains how to deploy applications to the Flipper Zero.
-   `resources.md`: A curated list of essential links for Flipper Zero development.

### 2.2. Example Applications

These are the Flipper Zero applications that the guides teach you how to build.

-   `hello-flipper/`: A minimal application that prints "Hello world" to the Flipper Zero's log.
-   `hello-flipper-ui/`: A simple UI application that displays "Hello, Flipper!" on the device screen using a `ViewPort`.

### 2.3. Project Planning

-   `IDEAS.md`: A document that tracks ideas for future applications and guides.

## 3. Development Workflow & Conventions

-   **Toolchain:** Development relies on the `uFBT` (micro Flipper Build Tool) for creating, building, and deploying applications.
-   **Language:** All applications are written in C.
-   **Editor:** Visual Studio Code is the recommended editor due to its strong integration with `uFBT`.
-   **UI Approach:** The initial guides focus on a simple, direct `ViewPort`-only approach for UI, without more complex abstractions like `ViewDispatcher`.
