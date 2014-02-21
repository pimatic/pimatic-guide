---
title: Load you Plugin
layout: guide
tags: ['guide', page']
guideOrder: 2040
---

Just add your plugin to your pimatic `config.json` file like any other plugin.

    {
      "plugin": "my-plugin",
      "my-config-option": "some thing"
    }

pimatic searches for a directory called `pimatic-my-plugin` in its parent `node_modules` directory
and loads your plugin.

You should see the string "Hello World" in pimatics output.