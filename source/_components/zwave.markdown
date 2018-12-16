---
layout: page
title: "Z-Wave"
description: "Instructions on how to integrate your existing Z-Wave within Home Assistant."
date: 2016-02-27 19:59
sidebar: true
comments: false
sharing: true
footer: true
logo: z-wave.png
ha_category: Hub
featured: true
ha_iot_class: "Local Push"
---

The [Z-Wave](http://www.z-wave.com/) integration for Home Assistant allows you to observe and control connected Z-Wave devices. Please see the [Z-Wave getting started section](/docs/z-wave/) for in-depth documentation on how to use and setup the Z-Wave component.

## {% linkable_title Configuration %}
<P class='note'>
You can use the Z-Wave *Integration* in the *Configuration* menu to set up the Z-Wave component or use a manual configuration as seen below. Refer to [Z-Wave Installation](/docs/z-wave/installation#configuration) for more information.
</p>

```yaml
# Example configuration.yaml entry
zwave:
  usb_path: /dev/ttyACM0
  device_config: !include zwave_device_config.yaml
```

{% configuration zwave %}
usb_path:
  description: The port where your device is connected to your Home Assistant host.
  required: false
  type: string
  default: /zwaveusbstick
network_key:
  description: The 16-byte network key in the form `"0x01, 0x02..."` used in order to connect securely to compatible devices. It is recommended that a network key is configured as security enabled devices may not function correctly if they are not added securely.
  required: false
  type: string
  default: None
config_path:
  description: "The path to the Python OpenZWave configuration files. NOTE: there is also the [update_config service](https://www.home-assistant.io/docs/z-wave/services/) to perform updating the config within python-openzwave automatically."
  required: false
  type: string
  default: the 'config' that is installed by python-openzwave
autoheal:
  description: Allows disabling auto Z-Wave heal at midnight.
  required: false
  type: boolean
  default: True
polling_interval:
  description: The time period in milliseconds between polls of a nodes value. Be careful about using polling values below 30000 (30 seconds) as polling can flood the zwave network and cause problems.
  required: false
  type: integer
  default: 60000
debug:
  description: Print verbose z-wave info to log.
  required: false
  type: boolean
  default: False
device_config / device_config_domain / device_config_glob:
  description: "This attribute contains node-specific override values. NOTE: This needs to be specified if you are going to use any of the following options. See [Customizing devices and services](/docs/configuration/customizing-devices/) for the format."
  required: false
  type: string, list
  keys:
    ignored:
      description: Ignore this entity completely. It won't be shown in the Web Interface and no events are generated for it.
      required: false
      type: boolean
      default: False
    polling_intensity:
      description: Enables polling of a value and sets the frequency of polling (0=none, 1=every time through the list, 2=every other time, etc). If not specified then your device will not be polled.
      required: false
      type: integer
      default: 0
    refresh_value:
      description: Enable refreshing of the node value. Only the light component uses this.
      required: false
      type: boolean
      default: False
    delay:
      description: Specify the delay for refreshing of node value. Only the light component uses this.
      required: false
      type: integer
      default: 5
    invert_openclose_buttons:
      description: Inverts function of the open and close buttons for the cover domain. This will not invert the position and state reporting.
      required: false
      type: boolean
      default: False
{% endconfiguration %}

<p class='note'>
As of Home Assistant 0.81, the Z-Wave `usb_path` and `network_key` options are configured through the Integrations page in Home Assistant. Specifying a `zwave:` section in configuration.yaml is no longer required unless you need to customize other settings, such as `device_config`, `polling_interval`, etc.
</p>
