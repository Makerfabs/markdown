# ESPHome and Home Assistant User Guide

This document aims to guide users through the process of creating an ESPHome device, flashing the firmware, and integrating it into the Home Assistant platform.

## ESPHome Workflow

### 1. Create a New Device

1. In a web browser, access the ESPHome web interface, usually located at `your-raspberry-pi-ip:6052`.

2. On the main page, click the **NEW DEVICE** button.
   ![image-20250902141428317](https://easyimage.linwanrong.com/i/2025/09/02/ne1zgr-0.webp)

3. In the pop-up dialog, enter a name for the new device (e.g., `TEST`) and click **NEXT**.

   > **Note**: The first time you create a device with ESPHome, you will be prompted to enter your Wi-Fi SSID and password for network connectivity.

   ![image-20250821165653536](https://easyimage.linwanrong.com/i/2025/08/21/re9o5v-0.webp)

4. Click **SKIP THIS STEP**.
   ![image-20250902153717900](https://easyimage.linwanrong.com/i/2025/09/02/pf7fhd-0.webp)

5. Select the corresponding chip model for your development board (e.g., `ESP32`).
   ![image-20250820110410956](https://easyimage.linwanrong.com/i/2025/08/20/i9da9l-0.webp)

6. Click **SKIP** to complete the creation process.
   ![image-20250902153913904](https://easyimage.linwanrong.com/i/2025/09/02/pgdh3k-0.webp)

7. After completing these steps, you will see a new device card on the ESPHome main page.
   ![image-20250902154216110](https://easyimage.linwanrong.com/i/2025/09/02/pi5yxx-0.webp)

### 2. Configure and Install

1. Below the device card, click the **EDIT** button to view or modify the device's YAML configuration file.
2. After confirming the configuration is correct, click **SAVE** in the top right corner, then click **INSTALL**.
   ![image-20250902155839476](https://easyimage.linwanrong.com/i/2025/09/02/pru20c-0.webp)
3. In the installation options, select **Manual download**.
   ![image-20250902162441568](https://easyimage.linwanrong.com/i/2025/09/02/qv52u8-0.webp)
4. The system will begin compiling the firmware online. Once successful, select the **Factory format** option, and the browser will automatically download the binary firmware file (`.bin` format) for the initial flashing.
   ![image-20250902163235959](https://easyimage.linwanrong.com/i/2025/09/02/qzvefq-0.webp)

### 3. Flashing

1. Connect the ESP device to your computer using a USB-C cable.
2. In your browser, go to the [ESPHome Web Flasher](https://web.esphome.io/) online tool.
   ![image-20250820112428934](https://easyimage.linwanrong.com/i/2025/08/20/ildsc4-0.webp)
3. Click **CONNECT**, and in the pop-up dialog, select the COM port corresponding to your device and connect.
   ![image-20250820120932734](https://easyimage.linwanrong.com/i/2025/08/20/k007nd-0.webp)
4. Click **INSTALL**, select the binary firmware file downloaded in the previous step, and click **INSTALL** again to begin flashing.
5. After a successful flash, return to the ESPHome main page and click the **LOGS** button below the device card. In the log window that appears, you will see the IP address assigned to the device. **Please record this IP address**, as it will be needed for the Home Assistant integration.

## Home Assistant Integration Process

1. In your browser, access your Home Assistant instance, usually located at `your-raspberry-pi-ip:8123`.
2. Navigate to **Settings** > **Devices & Services**.

### Automatic Discovery Integration

Typically, Home Assistant will automatically discover new ESPHome devices on the local network.

1. At the top of the "Devices & Services" page, you will see the discovered devices.
   ![image-20250903170501710](https://easyimage.linwanrong.com/i/2025/09/03/s759he-0.webp)
2. Click the **Add** button on the corresponding device card.
3. You will be prompted to enter the device's encryption key. You can find this key in the ESPHome device's YAML configuration file under the `api` -> `encryption` -> `key` field.
4. After entering the key, the integration is complete.

### Manual Integration

If Home Assistant does not automatically discover the device, follow these steps to add it manually:

1. On the **Settings** > **Devices & Services** page, click the **+ ADD INTEGRATION** button in the bottom right corner.
2. Search for and select **ESPHome**.
3. In the pop-up dialog, enter the IP address you previously obtained from the device logs, and then click **SUBMIT**.
4. When prompted, enter the device's encryption key.
5. You can choose to assign the device to an Area, or click **FINISH** to skip this step.

Once the integration is successful, the device-related entities (such as sensors, switches, etc.) will typically be added to the Home Assistant Overview dashboard automatically, and you can begin configuring automations.