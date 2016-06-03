---
title: Developing Environment
layout: guide
tags: ['guide', page']
guideOrder: 2010
---

Develop on a Linux box or a Mac. It makes things easier. You can develop on the Raspberry Pi, but its too 
slow. If you don't have a Linux or Mac running (how can you?) then I suggest to use VirtualBox and 
install a Ubuntu.

### Install Node.js

You need to install or update to the __LTS__ version of Node.js ([version 4.4.5](https://nodejs.org/en/download/) at 
the time of writing). Earlier versions of Node.js aren't supported. 

### Setup pimatic for development

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

### Debug outputs

You should add these options to the `settings` section of your `config.json` to get debug outputs

    "debug": true,
    "logLevel": "debug"

Editor / IDE Setup
------------------
Coffeescript is whitespace sensitive, so make sure to use the following editor settings:

* tab size: 2
* translate tabs to spaces: true
* max line length: 100

I'm using [sublime text](http://www.sublimetext.com/) as a editor. An example project config would be:

    {
      "folders":
      [
        {
          "path": "."
        }
      ],
      "settings":
      {
        "tab_size": 2,
        "translate_tabs_to_spaces": true,
        "rulers": [100]
      }
    }

If you use sublime then install [BetterCoffee](https://github.com/aponxi/sublime-better-coffeescript).