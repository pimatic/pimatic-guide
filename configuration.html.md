---
title: Configuration
layout: page
tags: ['guide', page']
guideOrder: 1
---
The `config.json` file is in the [json format](https://en.wikipedia.org/wiki/JSON) and currently includes five 
sections:

    { 
      "settings": { ... },
      "plugins": [ ... ],
      "devices": [ ... ],
      "rules": [ ... ]
    }

### The "settings"-section
The `"settings"`-section contains the configuration for the http- and https-server. You have 
to set `"username"` and `"password"` for the authentication or disable it. In the default config 
just the http-server is enabled and configurated to run on port 80.

See the [config-schema](http://www.pimatic.org/docs/config-schema.html) for more details and
all configuration options.

### The "plugins"-section
In the `"plugins"`-section you have to list all plugins to load in the form of

    { 
      "plugin": "plugin-name" 
    }

where `"plugin-name"` ist the name and directory of the plugin you want to load. All plugins are 
installed in the `node_modules` directory and prefixed with `pimatic-`. 


### The "devices"-section
The `"devices"`-section should contain all devices, you want to have registered in the 
framework. An actuator is typically provided by a plugin, so take a look at the desired plugin 
for more details about the configuration of your devices. A device configuration has the form

    { 
      "id": "light",
      "class": "SomeSwitch",
      "name": "Light in the kitchen",
      ...
    }

where the `"id"` should be unique, the `"name"` should be human readable description and `"class"`
determines the plugin and type of the device. 

### The "rules"-section
The `"rules"`-section can contain a list of rules in the form of:

    { 
      "id": "printerOff",
      "rule":  "if its 6pm then turn the printer off"
    }

where `"id"` should be a unique string and rule a string of the form "if ... then ...". 