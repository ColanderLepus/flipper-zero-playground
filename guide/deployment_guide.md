### Deploy the Application to Your Flipper Zero

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
