# Guide to Installing Home Assistant and ESPHome with Docker

**Version**: 1.0

**Author**: Makerfabs

**Last Updated**: 2025-09-02

## I. Overview

This document aims to guide users on how to efficiently install and deploy Home Assistant and ESPHome services on a Raspberry Pi using Docker.

## II. Prerequisites

Before you begin, please ensure you have completed the following preparations:

- [Successfully installed Raspberry Pi OS](https://raspberrytips.com/install-raspberry-pi-os/)
- [Installed the Docker environment on your Raspberry Pi](https://itsfoss.com/raspberry-pi-install-docker/)

## III. Installation Steps

### Step 1: Prepare the Working Directory

1. Log in to your Raspberry Pi via SSH.

   ```
   ssh <your_username>@<your_raspberry_pi_ip>
   ```

2. First, create a root directory to store Docker container data. This guide uses `~/docker` as an example, but you can choose a different path according to your preference.

   ```
   mkdir ~/docker
   cd ~/docker
   ```

3. Within this directory, create separate subdirectories for Home Assistant and ESPHome data.

   ```
   mkdir homeassistant
   mkdir esphome
   ```

### Step 2: Install Home Assistant

1. Navigate to the `homeassistant` directory and create a `compose.yaml` file.

   ```
   cd homeassistant
   # You can use the commands you are familiar with to edit compose.yaml, such as vi, vim, etc.
   nano compose.yaml
   ```

2. Paste the following content into the `compose.yaml` file.

   > **Note**: Please modify the `- /home/pi/docker/homeassistant/config:/config` line in the `volumes` section according to your actual user and path.

   ```
   # ~/docker/homeassistant/compose.yaml
   version: '3'
   services:
     homeassistant:
       container_name: homeassistant
       image: "ghcr.io/home-assistant/home-assistant:stable"
       volumes:
         # Map the container's /config directory to the host for persistent storage of configuration
         - /home/pi/docker/homeassistant/config:/config 
         - /etc/localtime:/etc/localtime:ro
         - /run/dbus:/run/dbus:ro
       restart: unless-stopped
       privileged: true
       network_mode: host
   ```

3. Ensure your current terminal path is in the same directory as the `compose.yaml` file, then execute the following command to start the service:

   ```
   docker compose up -d
   ```

### Step 3: Install ESPHome

1. Return to the `docker` root directory, navigate into the `esphome` directory, and create a new `compose.yaml` file.

   ```
   cd ../esphome
   # You can use the commands you are familiar with to edit compose.yaml, such as vi, vim, etc.
   nano compose.yaml
   ```

2. Paste the following configuration content, **specific to ESPHome**, into the `compose.yaml` file.

   > **Note**: Similarly, please modify the `- /home/pi/docker/esphome/config:/config` line in the `volumes` section according to your actual path.

   ```
   # ~/docker/esphome/compose.yaml
   version: '3'
   services:
     esphome:
       container_name: esphome
       image: "ghcr.io/esphome/esphome"
       volumes:
         # Map the container's /config directory to the host for persistent storage of device firmware and configurations
         - /home/pi/docker/esphome/config:/config
         - /etc/localtime:/etc/localtime:ro
       restart: unless-stopped
       privileged: true
       network_mode: host
   ```

3. Again, ensure your current terminal path is in the same directory as this `compose.yaml` file, then execute the following command to start the service:

   ```
   docker compose up -d
   ```

### Step 4: Accessing the Services

Once the services have started successfully, you can access Home Assistant and ESPHome via the following addresses in your browser:

- **Home Assistant**: `http://<your_raspberry_pi_ip>:8123`
- **ESPHome**: `http://<your_raspberry_pi_ip>:6052`