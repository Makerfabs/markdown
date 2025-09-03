# Guide: Using ESPHome & Home Assistant

This guide will walk you through creating a new device in ESPHome, installing its firmware, and integrating it with Home Assistant.

## 1. Using ESPHome

### 1.1. Creating a New Device

1. Open the ESPHome web interface in your browser. The default address is typically `http://<your-raspberry-pi-ip>:6052`.

2. Click on **"NEW DEVICE"**.

   ![image-20250902141428317](https://easyimage.linwanrong.com/i/2025/09/02/ne1zgr-0.webp)

3. Enter a name for your device. For this example, we'll use "TEST". Click **"NEXT"**.

   > **Note:** If this is your first time creating a device in ESPHome, you will be prompted to enter your Wi-Fi credentials.

   ![image-20250821165653536](https://easyimage.linwanrong.com/i/2025/08/21/re9o5v-0.webp)

4. On the next screen, click **"SKIP THIS STEP"**.

   ![image-20250902153717900](https://easyimage.linwanrong.com/i/2025/09/02/pf7fhd-0.webp)

5. Select the appropriate chip for your board. For this example, we will choose **"ESP32"**.

   ![image-20250820110410956](https://easyimage.linwanrong.com/i/2025/08/20/i9da9l-0.webp)

6. Click **"SKIP"**.

   ![image-20250902153913904](https://easyimage.linwanrong.com/i/2025/09/02/pgdh3k-0.webp)

7. You should now see the newly created device on your ESPHome dashboard.

   ![image-20250902154216110](https://easyimage.linwanrong.com/i/2025/09/02/pi5yxx-0.webp)

### 1.2. Configuration & Installation

1. Click the **"EDIT"** button under your newly created device.

2. After reviewing the configuration, click **"SAVE"** in the top-right corner, and then click **"INSTALL"**.

   ![image-20250902155839476](https://easyimage.linwanrong.com/i/2025/09/02/pru20c-0.webp)

3. In the installation dialog, select **"Manual download"**.

   ![image-20250902162441568](https://easyimage.linwanrong.com/i/2025/09/02/qv52u8-0.webp)

4. Once the compilation is complete, choose **"Factory format"**. Your browser will automatically download the binary file (`.bin`).

   ![image-20250902163235959](https://easyimage.linwanrong.com/i/2025/09/02/qzvefq-0.webp)

### 1.3. Flashing the Firmware

1. Connect your device to your computer using a USB-C cable.

2. Open the [ESPHome Web Flasher](https://web.esphome.io/) in your browser.

   ![image-20250820112428934](https://easyimage.linwanrong.com/i/2025/08/20/ildsc4-0.webp)

3. Click **"CONNECT"**. A pop-up window will appear; select the COM port corresponding to your device.

   ![image-20250820120932734](https://easyimage.linwanrong.com/i/2025/08/20/k007nd-0.webp)

4. Click **"INSTALL"**, choose the binary file you downloaded earlier, and click **"INSTALL"** again to begin the flashing process.

5. After a successful flash, go back to your ESPHome dashboard. Click on **"LOGS"** under the device to view the device logs. In the log window, you will find the IP address assigned to your device. This is crucial for the Home Assistant integration.

## 2. Home Assistant Integration

1. Open your Home Assistant interface in a browser. The default address is typically `http://<your-raspberry-pi-ip>:8123`.

### 2.1. Automatic Discovery

Home Assistant will usually discover the new ESPHome device automatically.

1. Navigate to **Settings** -> **Devices & Services**.

2. You should see the discovered device. Click **"CONFIGURE"**.

3. You will be prompted to enter the encryption key. This is the `key` value from your device's YAML configuration file in ESPHome.

   ![image-20250902164559875](https://easyimage.linwanrong.com/i/2025/09/02/r7zu3y-0.webp)

### 2.2. Manual Setup

If Home Assistant does not discover the device automatically, you can add it manually:

1. Go to **Settings** -> **Devices & Services**.
2. Click the **"+ ADD INTEGRATION"** button in the bottom-right corner.
3. Search for and select **"ESPHome"**.
4. In the pop-up window, enter the IP address of your device (which you found in the logs) and click **"SUBMIT"**.
5. Enter the encryption `key` when prompted.
6. You can then assign the device to an area or skip this step.

Once integrated, Home Assistant will typically add the device's entities to your **Overview** dashboard automatically.