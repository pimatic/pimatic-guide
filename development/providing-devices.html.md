---
title: Providing Devices
layout: guide
tags: ['guide', page']
guideOrder: 2050
---

###Basics

Devices are added to pimatic by first providing a config for it. Every device needs an entry in the devices-section 
of the `config.json` file

A device config looks like:

    { 
      "id": "light",
      "class": "MySwitch",
      "name": "Kitchen Light"
    }

You must first register your new device by calling the `registerDeviceClass` function of the `deviceManager`. The framework reads 
every device config on startup and calls the provided `createCallback` function for all registered devices 
of the registered class. The callback gets the device-config from the config file and should construct and return
the instance of the device:

<script src="https://gist.github.com/sweetpi/9157350.js?file=providing-devices.coffee"></script>

###Device-class

Any device must be a subclass of the device class. A device has "attributes" and "actions"

####Attributes

Attributes are properties of the device like the state of a switch, or sensor values like temperature. All Sensor-Devices are displayed as values at the frontend. For other devices, the display type depends on the device type.
For example the state of a switch is displayed as a switch button.

Attributes are defined by adding the `attributes` property of the `Device` class:

<script src="https://gist.github.com/sweetpi/9157350.js?file=attributes.coffee"></script>

Each attribute must have a getter function that returns a promise fulfilled with the current attribute value. The getter must
be named like the attribute, prefixed with `get` and uppercase first letter of the attribute name. 

If an attribute changes an event, the attribute name should be emitted that contains the new value:

<script src="https://gist.github.com/sweetpi/9157350.js?file=attribute-emit.coffee "></script>

For more attribute examples take a look at the [predefined Devices](/docs/lib/devices.html).

####Actions

In additional to attributes a device can have "actions". Actions are functions that can be called by the framework. Actions
are defined like attributes:

<script src="https://gist.github.com/sweetpi/9157350.js?file=actions.coffee"></script>

For each action, there should be a function with the same name, that executes the action and returns a promise that gets fulfilled when done.

For more action examples, take a look at the [predefined Devices](/docs/lib/devices.html).

####Constructor

Your constructor function must assign a name and an ID to the device (typical from the device config).

<script src="https://gist.github.com/sweetpi/9157350.js?file=device-constructor.coffee"></script>

####Predefined devices

If you don't want to define an exotic device try to use a [predefined Device](/docs/lib/devices.html) as base class. 

###Switch Device

For Switch devices you can use the `PowerSwitch` class as base. You have to define the `changeStateTo` and `getState`
function.

<script src="https://gist.github.com/sweetpi/9157350.js?file=switch-device.coffee"></script>

A full example for an switch device can be found in the 
[with-switch-device branch](https://github.com/pimatic/pimatic-plugin-template/tree/with-switch-device)


###Temperature Sensor

A Temperature sensor can use the `TemperatureSensor` class as base. You must define a `getTemperature` function and emit the
"temperature" attribute event, if a new value has been read.

<script src="https://gist.github.com/sweetpi/9157350.js?file=temperature-sensor.coffee"></script>
