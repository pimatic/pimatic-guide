---
title: Providing Devices
layout: guide
tags: ['guide', page']
guideOrder: 2050
---

###Basics

Devices are added to pimatic by first providing a config for it. Every device needs an entry in the devices-Section 
of the `config.json` file

A device config looks like that:

    { 
      "id": "light",
      "class": "MySwitch",
      "name": "Kitchen Light",
      
    }

The framework reads every device config on startup and calls the `createDevice` function, if existing, on your plugin
with the device-config from the devices-Section. If the device class belongs to your plugin then it should create a device
from the device-config and add it to the framework.

<script src="https://gist.github.com/sweetpi/9143534.js"></script>

###Switch Devices

An full example for an switch device can be found 
[in the with-switch-device branch](https://github.com/pimatic/pimatic-plugin-template/tree/with-switch-device)