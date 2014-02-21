---
title: Developing Environment
layout: guide
tags: ['guide', page']
guideOrder: 2010
---
-----------------------

Develop on a Linux box. It makes things easier. You can develop on the Raspberry Pi, but its too 
slow. If you don't have a Linux running (how can you?) then I suggest to use VirtualBox and 
install a Ubuntu.

###Instal node.js and CoffeeScript
* Install Node.js with the package manager of you distro `sudo apt-get install node` 
* Install CoffeeScript gloabaly with: `sudo npm install -g coffee-script`

###Setup pimatic for development

    mkdir pimatic-dev
    npm install pimatic --prefix pimatic-dev

to install the pimatic framework.

Copy the default config file:

    cd pimatic-dev
    cp ./node_modules/pimatic/config_default.json ./config.json

You should end up with this in your `pimatic-dev` directory:

<table class="table file-listing">
<tr><td>`config.json`</td>				       <td>the config file</td></tr>
<tr><td>`node_modules`</td>				       <td>directory for the framework and plugins</td></tr>
<tr><td>`node_modules/pimatic`</td>			   <td>the pimatic framework files</td></tr>
</table>

###Debug outputs

You should add these options to the `settings` section of your `config.json` to get debug outputs

    "debug": true,
    "logLevel": "debug"

