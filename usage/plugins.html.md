---
title: Installing Plugins
layout: guide
tags: ['guide', page']
guideOrder: 1030
---

Installing plugins
------------
Most functionality of pimatic is provided by plugins. Every Plugins is an npm package prefixed
with `pimatic-`. You can advice pimatic to install a package at start by [adding it to the 
config.json](http://www.pimatic.org/guide/getting-started/configuration/#the-_plugins_-section) 
file. pimatic will install the package from the npm-registry (if its not already 
installed) at start.

Manual plugin installation or update
-----------------------
You can manually install or update a plugin by running:

    sudo npm install pimatic-pluginname

inside your _pimatic-app_ directory.