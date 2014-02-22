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

<script src="https://gist.github.com/sweetpi/9157350.js?file=providing-devices.coffee"></script>

###Device-class

Any device must be subclass of the device class. A device has Attributes and Actions

####Attributes

Attributes are properties of the device like the state of a switch or sensor values like temperature. For 
Sensor-Devices these are displayed at the frontend as values. For other devices the display type depends on the device type.
For example the state of a switch is displayed as an switch button.

Attributes are defined by adding defining the `attributes` property of the `Device` class:

<script src="https://gist.github.com/sweetpi/9157350.js?file=attributes.coffee"></script>

Each attribute must have a getter function that returns a Promise fullfiled with the current attribute value. The getter must
be named like the attribute prefixed with `get` and Uppercase first letter of the attribute name. 

If an attribute changes an event with the attribute name should be emitted that contains the new value:

<script src="https://gist.github.com/sweetpi/9157350.js?file=attribute-emit.coffee "></script>

For more attribute examples take a look at the [predefined Devices](/docs/lib/devices.html).

####Actions

In additional to attributes a device can have Actions. Actions are functions that can be called by the framework. Actions
are defined like attributes:

<script src="https://gist.github.com/sweetpi/9157350.js?file=actions.coffee"></script>

For eacht Action there should be a function with the same name that executes the action and returns a promise that get fullfiled
when done.

For more actions examples take a look at the [predefined Devices](/docs/lib/devices.html).


####Predefined devices

If you don't want to define an exotic device try to use a [predefined Device](/docs/lib/devices.html) as base class. 

###Switch Device

For Switch devices you can use the `PowerSwitch` class as base and you have to define the `changeStateTo` and `getState`
function.

<script src="https://gist.github.com/sweetpi/9157350.js?file=switch-device.coffee"></script>

An full example for an switch device can be found in the 
[with-switch-device branch](https://github.com/pimatic/pimatic-plugin-template/tree/with-switch-device)


###Temperature Sensor

A Temperature ensor can use the `TemperatureSensor` class as base. You must define a `getTemperature` function and emit the
"temperature" attribute event, if a new value was readed.

<script src="https://gist.github.com/sweetpi/9157350.js?file=temperature-sensor.coffee"></script>