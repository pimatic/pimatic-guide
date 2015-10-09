---
title: Configuration
layout: guide
tags: ['guide', page']
guideOrder: 20
---
The `config.json` file is in the [json format](https://en.wikipedia.org/wiki/JSON) and currently includes four
sections:

    {
      "settings": { ... },
      "plugins": [ ... ],
      "devices": [ ... ],
      "rules": [ ... ]
    }

### The _settings_ section
The _settings_ section contains the configuration for the HTTP and HTTPS server. You have
to set the _username_ and _password_ property for the authentication or disable it with setting
_enabled_ to false.
In the default config just the HTTP server is enabled and configured to run on port 80.

See the [config-schema](http://www.pimatic.org/docs/config-schema.html) for more details and
all configuration options.

### The _plugins_ section
In the _plugins_ section you have to list all plugins to load in the form of

    {
      "plugin": "plugin-name"
    }

where _plugin-name_ ist the name and directory of the plugin you want to load. All plugins are
installed in the `node_modules` directory and prefixed with `pimatic-`.


### The _devices_ section
The _devices_ section should contain all devices, you want to have registered in the
framework. An actuator is typically provided by a plugin, so take a look at the desired plugin
for more details about the configuration of your devices. A device configuration has the form

    {
      "id": "light",
      "class": "SomeSwitch",
      "name": "Light in the kitchen",
      ...
    }

where the _id_ property should be unique, the _name_ property should be a human readable description
and the _class_ property determines the plugin and type of the device.

### The _rules_ section
The _rules_ section can contain a list of rules in the form of:

    {
      "id": "printerOff",
      "rule":  "if its 6pm then turn the printer off"
    }

where _id_ should be a unique string and rule a string of the form "if ... then ...".
