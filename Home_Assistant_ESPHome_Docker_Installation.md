# Guide: Installing Home Assistant & ESPHome with Docker

**Version:** 1.0

**Author:** Makerfabs

**Creation Date:** 2025-09-02

### 1. Introduction

This document provides instructions on how to install Home Assistant and ESPHome using Docker on a Raspberry Pi.

For this guide, you should already be familiar with:

- [How to install Raspberry Pi OS](https://raspberrytips.com/install-raspberry-pi-os/)
- [How to install Docker on Raspberry Pi](https://itsfoss.com/raspberry-pi-install-docker/)

### 2. Installation Steps

#### 2.1. Connect to Your Raspberry Pi

1. Log in to your Raspberry Pi using SSH. You will be prompted for your user password.

   ```
   ssh <your_pi_username>@<your_pi_ip_address>
   ```

#### 2.2. Prepare Docker Directory

1. Create a directory to store your Docker configurations. In this example, we will use `~/docker`.

   ```
   mkdir ~/docker
   cd ~/docker
   ```

2. Inside the `~/docker` directory, create a `compose.yaml` file using your preferred text editor (e.g., `nano` or `vim`).

   ```
   nano compose.yaml
   ```

3. Copy and paste the following content into the `compose.yaml` file:

   ```
   version: '3'
   services:
     homeassistant:
       container_name: homeassistant
       image: "ghcr.io/home-assistant/home-assistant:stable"
       volumes:
         - /home/pi/docker/homeassistant/config:/config # Maps the container's /config directory to this host path
         - /etc/localtime:/etc/localtime:ro
         - /run/dbus:/run/dbus:ro
       restart: unless-stopped
       privileged: true
       network_mode: host
   
     esphome:
       container_name: esphome
       image: "ghcr.io/esphome/esphome"
       volumes:
         - /home/pi/docker/esphome/config:/config # Maps the container's /config directory to this host path
         - /etc/localtime:/etc/localtime:ro
       restart: always
       privileged: true
       network_mode: host
   ```

   > **Important:** Modify the `volumes` paths in the `compose.yaml` file to match the actual paths on your system if they differ from the example (`/home/pi/docker/...`).

#### 2.3. Start the Services

1. While in the directory containing your `compose.yaml` file (`~/docker`), run the following command to start the Home Assistant and ESPHome services in the background:

   ```
   docker compose up -d
   ```

#### 2.4. Access Your Services

Once the containers are running, you can access the web interfaces:

- **Home Assistant:** `http://<your_pi_ip_address>:8123`
- **ESPHome:** `http://<your_pi_ip_address>:6052`