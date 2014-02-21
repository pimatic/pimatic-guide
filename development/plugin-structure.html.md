---
title: Plugin Structure
layout: guide
tags: ['guide', page']
guideOrder: 2020
---
-----------------------

For the plugin template on github and clone your foked version into your `node_modules` folder 
in your `pimatic-dev` directory.

	cd node_modules
	git clone https://github.com/your-name/pimatic-plugin-template.git pimatic-my-plugin

Your `pimatic-dev` directory should now look like this:

	config.json                		<- the config file
	node_modules               		<- directory for the framework and plugins
	node_modules/pimatic       		<- the pimatic framework files
	node_modules/pimatic-my-plugin  <- your plugin in development


In your `pimatic-my-plugin` directory are following files:

	my-plugin.coffee                   <- This should become the main source file of your Plugin.
	my-plugin-config-schema.coffee     <- Template for config definitions for your plugin.
	package.json:                      <- The [npm package specification](https://npmjs.org/doc/json.html).

* Change into your plugin folder `cd pimatic-your-plugin` and edit the `package.json`. Take a look
  at the [npm package.json documentation](https://npmjs.org/doc/json.html) for infos.

You should end up with this in your 

