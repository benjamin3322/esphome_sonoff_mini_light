# esphome_sonoff_mini_light
This project is a ESPHome configuration that facilitate the configuration of SONOFF Mini.

# How to use this configuration
To use this base configuration create a new file in the ESPHome folder (with a name close to the device name, E.G: bedroom-left-light.yaml).

Edit this new file to add the substitution used in the common configuration:

```yaml
substitutions:
  # Device name is used as host name by mDNS to resolve ip address. Avoid using '_' in name. 
  # It can that can cause mDNS resolution issues
  device_name: <put_device_name_here> # required

  # Variables used in commons/wifi.yaml
  wifi_ssid: !secret wifi_ssid
  wifi_password: !secret wifi_password
  wifi_ap_password: <put_some_wifi_fallback_password_here>

  ota_password: <put_some_ota_password_here>
  api_encryption_key: <put_some_encryption_key_here>
```

Add those secrets in the secrets.yaml file:
secrets.yaml:
```yaml
wifi_ssid: <put_your_wifi_ssid_here>
wifi_password: <put_your_wifi_password_here>
```

Add the remote package repository reference to the new file. A new configuration file will be build by downloading all file and compiling it into a full config file.
```yaml
packages:
  remote_package:
    url: https://github.com/benjamin3322/esphome_sonoff_mini_light
    ref: main # optional
    files: [
      commons/wifi.yaml, 
      commons/esphome_8266.yaml, 
      
      # This mode configure the S1/S2 input lines into push button mode (push toggle the light on or off)
      # To use a regulat switch mode use the file named commons/sonoff_mini_light_switch_mode.yaml (toggle the light on/off by switching a button up/down)
      commons/sonoff_mini_light_push_mode.yaml
    ]
    refresh: 1d # optional
```

