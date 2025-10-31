# Building Your First Flipper Zero UI Application: Hello, Flipper!

## Introduction

In this guide, we will create a new Flipper Zero application named `hello_flipper_ui`. Unlike our previous "Hello World" example that only printed to the device's internal log, this application will display the text "Hello, Flipper!" directly on the Flipper Zero's monochrome screen. This will introduce you to the fundamental concepts of Flipper Zero's graphical user interface (GUI) development using a simple `ViewPort`.

### Setup and Creation

Before you begin, please follow the [Setup and Create Guide](setup_and_create_guide.md) to:
1.  Set up your development environment.
2.  Create a new application. For this guide, you can use `hello_flipper_ui` as your `APPID`.

After following the guide, you will have a folder containing a generated application. The rest of this tutorial will focus on modifying the code in `hello_flipper_ui.c`.

## Understanding Flipper Zero's GUI Basics: The `ViewPort` Approach

The Flipper Zero's UI is built around a 128x64 pixel monochrome LCD. For simple, single-screen applications, the `ViewPort` is the most straightforward way to display content and handle input. A `ViewPort` represents a drawing area on the screen and uses a `Canvas` to draw elements.

*   **`ViewPort`**: This is a fundamental UI element that represents a rectangular area on the screen where your application can draw. It's ideal for simple, single-screen UIs.
*   **`Canvas`**: This is the actual drawing surface provided to your `ViewPort`'s draw callback. It offers a set of functions (like `canvas_draw_str_aligned`, `canvas_draw_box`, etc.) that allow you to draw text, shapes, and images onto the screen.

The Flipper Zero's GUI framework operates on a "draw callback" mechanism. You provide a function that the system calls whenever the screen needs to be updated. Inside this function, you use the `Canvas` to draw your UI elements.

## Modifying `hello_flipper_ui.c`

Now, let's open the `hello_flipper_ui.c` file that `ufbt create` generated. We will modify this file to display our "Hello, Flipper!" message.

### Step-by-Step Modifications

1.  **Includes:**
    To access Flipper Zero's core functionalities and GUI components, we only need to include the main GUI header. The `<gui/gui.h>` header is a convenience header that pulls in `furi.h`, `view_port.h`, `canvas.h`, `input/input.h`, `furi_hal_resources.h`, and other essential headers, simplifying our include list.

    ```c
    #include <gui/gui.h>          // Comprehensive GUI, Furi, and Input functionality
    ```

2.  **Draw Callback Function:**
    This function is responsible for redrawing the screen. The Flipper Zero's GUI system calls it whenever the display needs to be updated. The `Canvas* canvas` argument provides the drawing surface, while `void* context` allows us to pass custom data to the callback (though it's `UNUSED` in this simple drawing example).

    ```c
    static void hello_flipper_ui_draw_callback(Canvas* canvas, void* context) {
        UNUSED(context); // Indicates that 'context' is intentionally unused

        canvas_clear(canvas); // Clears the entire display to prevent artifacts
        canvas_set_font(canvas, FontPrimary); // Sets the font to a standard, readable primary font
        // Draws "Hello, Flipper!" centered on the screen. (64, 32) is the center of the 128x64 screen.
        canvas_draw_str_aligned(canvas, 64, 32, AlignCenter, AlignCenter, "Hello, Flipper!");
    }
    ```
    *   `UNUSED(context)`: A macro indicating that the `context` parameter is intentionally unused in this function, preventing compiler warnings.
    *   `canvas_clear(canvas)`: Essential for clearing previous frames from the display buffer before drawing new content.
    *   `canvas_set_font(canvas, FontPrimary)`: Controls the typeface used for subsequent text drawing operations. `FontPrimary` is a predefined system font suitable for general use.
    *   `canvas_draw_str_aligned(canvas, x, y, horizontal_align, vertical_align, text)`: A versatile function for drawing text. It places the text `"Hello, Flipper!"` at the center of the device's screen (coordinates `64, 32`), with both horizontal and vertical alignment set to `AlignCenter` to precisely center the string.

3.  **Input Callback Function:**
    This function is invoked when the user presses a button on the Flipper Zero. Its primary role here is to capture these input events and push them into a message queue, allowing the main application loop to process them.

    ```c
    static void hello_flipper_ui_input_callback(InputEvent* input_event, void* context) {
        // The context is a pointer to our FuriMessageQueue for event handling.
        FuriMessageQueue* event_queue = (FuriMessageQueue*)context;
        // Place the captured input event into the message queue.
        // FuriWaitForever ensures the event is put into the queue, waiting indefinitely if the queue is full.
        furi_message_queue_put(event_queue, input_event, FuriWaitForever);
    }
    ```
    *   `InputEvent* input_event`: A pointer to a structure containing details about the button press (e.g., key, type of press).
    *   `FuriMessageQueue* event_queue = (FuriMessageQueue*)context`: The `context` passed to this callback is cast back to our `FuriMessageQueue*`, which is essential for sending events to our main loop.
    *   `furi_message_queue_put(event_queue, input_event, FuriWaitForever)`: This function adds the `input_event` to the `event_queue`. `FuriWaitForever` is a timeout value that tells the system to block indefinitely if the queue is full, ensuring the event is eventually queued.

4.  **Main Application Entry Point (`hello_flipper_ui_app`):**
    This is the heart of our application, where execution begins. It initializes the GUI, sets up our display (`ViewPort`), handles the main event loop, and cleans up resources upon exit.

    ```c
    int32_t hello_flipper_ui_app(void* p) {
        UNUSED(p); // 'p' is unused in this simple application

        // 1. Initialize GUI and Event Handling
        // Get a handle to the Flipper Zero's GUI service. This service manages display and input.
        Gui* gui = furi_record_open(RECORD_GUI);
        // Allocate a ViewPort, which is our drawing surface on the screen.
        ViewPort* view_port = view_port_alloc();
        // Create an event queue to receive input events from our callback.
        // The queue can hold 8 InputEvent structures.
        FuriMessageQueue* event_queue = furi_message_queue_alloc(8, sizeof(InputEvent));

        // 2. Set ViewPort Callbacks
        // Register our draw callback. 'NULL' is passed as context because the draw callback doesn't need external data.
        view_port_draw_callback_set(view_port, hello_flipper_ui_draw_callback, NULL);
        // Register our input callback, passing the 'event_queue' as context so the callback can push events to it.
        view_port_input_callback_set(view_port, hello_flipper_ui_input_callback, event_queue);

        // 3. Integrate ViewPort with GUI
        // Add our configured ViewPort to the GUI manager, making it visible on the screen.
        // GuiLayerFullscreen ensures it occupies the entire display.
        gui_add_view_port(gui, view_port, GuiLayerFullscreen);

        // 4. Main Application Event Loop
        InputEvent event; // Structure to hold incoming input events
        bool processing = true; // Flag to control the loop's execution

        // The application's main loop. It continues as long as 'processing' is true.
        for(; processing;) {
            // Wait indefinitely for an input event from the queue.
            // furi_check ensures the queue operation is successful.
            furi_check(furi_message_queue_get(event_queue, &event, FuriWaitForever) == FuriStatusOk);

            // Check if the received event is a short press of the Back button.
            if(event.type == InputTypeShort && event.key == InputKeyBack) {
                processing = false; // Set flag to false to exit the loop and application
            }
        }

        // 5. Clean Up Resources
        // Remove the ViewPort from the GUI before freeing its memory.
        gui_remove_view_port(gui, view_port);
        // Free the allocated ViewPort memory.
        view_port_free(view_port);
        // Close the GUI service handle.
        furi_record_close(RECORD_GUI);
        // Free the allocated FuriMessageQueue memory.
        furi_message_queue_free(event_queue);

        return 0; // Indicate successful application exit
    }
    ```
    *   `UNUSED(p)`: A macro signifying that the `p` parameter (which can be used to pass initial data to the app) is not used in this simple application.
    *   **Resource Allocation:**
        *   `Gui* gui = furi_record_open(RECORD_GUI);`: This obtains a pointer to the Flipper Zero's global GUI service. This service is crucial for managing the display and user input system.
        *   `ViewPort* view_port = view_port_alloc();`: Allocates memory for a new `ViewPort` object. This `ViewPort` will serve as our primary drawing area.
        *   `FuriMessageQueue* event_queue = furi_message_queue_alloc(8, sizeof(InputEvent));`: Creates a message queue. This queue will store `InputEvent` structures and has a capacity for 8 events. Message queues are vital for inter-thread communication and handling asynchronous events like button presses.
    *   **Set ViewPort Callbacks:**
        *   `view_port_draw_callback_set(view_port, hello_flipper_ui_draw_callback, NULL);`: Registers `hello_flipper_ui_draw_callback` as the function responsible for drawing on the `view_port`. We pass `NULL` as the context because our draw callback doesn't need any external application data for this simple display.
        *   `view_port_input_callback_set(view_port, hello_flipper_ui_input_callback, event_queue);`: Registers `hello_flipper_ui_input_callback` to receive input events for the `view_port`. We pass `event_queue` as context to this callback, allowing it to enqueue received input events into our message queue.
    *   **Integrate with GUI:**
        *   `gui_add_view_port(gui, view_port, GuiLayerFullscreen);`: This critical step adds our configured `view_port` to the Flipper Zero's GUI system, making it active and visible on the device's screen. `GuiLayerFullscreen` specifies that our `ViewPort` should occupy the entire display.
    *   **Main Event Loop:**
        *   `for(bool processing = true; processing;)`: This loop constitutes the core of our application's runtime. It continuously processes events until the `processing` flag is set to `false`.
        *   `furi_check(furi_message_queue_get(event_queue, &event, FuriWaitForever) == FuriStatusOk);`: This line waits for an `InputEvent` from our `event_queue`. `FuriWaitForever` ensures that the application will block here until an event is available, efficiently managing CPU usage. `furi_check` ensures the operation was successful.
        *   `if(event.type == InputTypeShort && event.key == InputKeyBack)`: Within the loop, we check if the received event is a `short` press of the `Back` button. This is our designated exit condition.
        *   `processing = false;`: If the Back button is pressed, this flag is set to `false`, causing the loop to terminate.
    *   **Resource Cleanup:** It is paramount to free all allocated resources when the application exits to prevent memory leaks and ensure system stability. These are freed in the reverse order of their allocation:
        *   `gui_remove_view_port(gui, view_port);`: Removes the `view_port` from the GUI.
        *   `view_port_free(view_port);`: Deallocates the `ViewPort` memory.
        *   `furi_record_close(RECORD_GUI);`: Releases the handle to the GUI service.
        *   `furi_message_queue_free(event_queue);`: Deallocates the message queue memory.

## Complete `hello_flipper_ui.c` Code

Here's the complete code for `hello_flipper_ui.c` after all modifications (no comments):

```c
#include <gui/gui.h>

/* generated by fbt from .png files in images folder */
#include <hello_flipper_ui_icons.h>

static void hello_flipper_ui_draw_callback(Canvas* canvas, void* context) {
    UNUSED(context);
    canvas_clear(canvas);
    canvas_set_font(canvas, FontPrimary);
    canvas_draw_str_aligned(canvas, 64, 32, AlignCenter, AlignCenter, "Hello, Flipper!");
}

static void hello_flipper_ui_input_callback(InputEvent* input_event, void* context) {
    FuriMessageQueue* event_queue = (FuriMessageQueue*)context;
    furi_message_queue_put(event_queue, input_event, FuriWaitForever);
}

int32_t hello_flipper_ui_app(void* p) {
    UNUSED(p);

    Gui* gui = furi_record_open(RECORD_GUI);
    ViewPort* view_port = view_port_alloc();
    FuriMessageQueue* event_queue = furi_message_queue_alloc(8, sizeof(InputEvent));

    view_port_draw_callback_set(view_port, hello_flipper_ui_draw_callback, NULL);
    view_port_input_callback_set(view_port, hello_flipper_ui_input_callback, event_queue);

    gui_add_view_port(gui, view_port, GuiLayerFullscreen);

    InputEvent event;
    for(bool processing = true; processing;) {
        furi_check(furi_message_queue_get(event_queue, &event, FuriWaitForever) == FuriStatusOk);

        if(event.type == InputTypeShort && event.key == InputKeyBack) {
            processing = false;
        }
    }

    gui_remove_view_port(gui, view_port);
    view_port_free(view_port);
    furi_record_close(RECORD_GUI);
    furi_message_queue_free(event_queue);

    return 0;
}
```

## Building the Application

Once you have updated `hello_flipper_ui.c` with the code above, save the file. Then, from your application's directory (where `application.fam` and `hello_flipper_ui.c` are located), run the `ufbt` command in your terminal (or VS Code integrated terminal):

```bash
ufbt
```

This will compile your application and create the `hello_flipper_ui.fap` file in the `dist` folder within your application's directory.

## Deploying the Application

For instructions on how to deploy your application to your Flipper Zero, please see the [Deployment Guide](deployment_guide.md).

## Expected Output

On your Flipper Zero's screen, you should now see the text "Hello, Flipper!" displayed in the center. You can press the "Back" button on your Flipper Zero to exit the application.
