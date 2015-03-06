---
title: Load your Plugin
layout: guide
tags: ['guide', page']
guideOrder: 2040
---

Just add your plugin to your pimatic `config.json` file like any other plugin.

    {
      "plugin": "my-plugin",
      "my-config-option": "some thing"
    }

Pimatic will search for a directory called `pimatic-my-plugin` in its parent `node_modules` directory
and will load your plugin afterwards.

You should see the string "Hello World" in pimatic's output.
