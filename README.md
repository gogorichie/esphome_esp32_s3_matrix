# ESP32 S3 Matrix 8x8 64 LED Configuration

This repository contains an ESPHome configuration for an ESP32-S3-based with 8x8 Onboard 8×8 RGB LED Matrix. The configuration uses the WS2812B LED chipset and supports various addressable light effects. This setup is ideal for creating colorful light displays, animations, and more, controlled over Wi-Fi. 

## Features

- **ESPHome Integration**: Easily integrate with Home Assistant or other ESPHome-compatible platforms.
- **Over-The-Air Updates**: Update the firmware wirelessly using the ESPHome dashboard.
- **Wi-Fi Provisioning**: Supports Wi-Fi provisioning via Bluetooth LE or a captive portal.
- **Multiple Light Effects**: Includes various built-in light effects like rainbow, color wipe, twinkle, and fireworks.
- **API Encryption**: Secure communication with an encrypted API key.
- **Web Server**: Simple web interface to manage your device.

## Requirements

- **ESP32-S3 Matrix ESP32 S3 Development Board with 8×8 RGB LED Matrix**: This configuration is designed for the ESP32-S3-Matrix Development Board, Based on ESP32-S3, Onboard 8×8 RGB LED Matrix.
- **ESPHome**: Version 2024.6.0 or later.

## Configuration

### Substitutions

This configuration uses substitutions to allow easy customization:

- `name`: Device name (default: `esp32_s3_matrix`)
- `friendly_name`: Friendly display name (default: `esp32_s3_matrix`)

### Wi-Fi Setup

You must replace the placeholders for Wi-Fi credentials with your actual details:

```yaml
wifi:
  ssid: !secret wifi_ssid  # Replace with your actual Wi-Fi SSID
  password: !secret wifi_password  # Replace with your actual Wi-Fi password
```

### API Encryption

Ensure you replace the API encryption key with your actual key:

```yaml
api:
  encryption:
    key: !secret api_encryption_key  # Replace with your actual encryption key
```

### Light Effects

The configuration supports the following light effects:

- **Rainbow**
- **Color Wipe**
- **Scan**
- **Twinkle**
- **Flicker**
- **Fireworks**

### Provisioning and OTA

This configuration supports multiple methods for provisioning Wi-Fi credentials and Over-The-Air (OTA) updates:

- **Improv Serial**: Allows provisioning via a serial connection.
- **Captive Portal**: Allows provisioning via a Wi-Fi access point.
- **Bluetooth LE**: Provisioning via Bluetooth LE (ESP32 Improv).

## Getting Started

1. Clone this repository.
2. Modify the `substitutions` and Wi-Fi configuration sections as needed.
3. Upload the configuration to your ESP32-S3 board using ESPHome.
4. Once the upload is complete, your device should be available on your network with the friendly name specified.

## Dashboard Import

This configuration includes a dashboard import from the official ESPHome firmware repository:

```yaml
dashboard_import:
  package_import_url: github://esphome/firmware/esphome-web/esp32s3.yaml@main
  import_full_config: true
```

This allows you to extend the functionality by importing additional configurations.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

---

For more information, visit the [ESPHome documentation](https://esphome.io/) or the official [ESP32-S3 documentation](https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/index.html).
