---
title: Installation
layout: guide
tags: ['guide', page']
guideOrder: 10
---

## Node.js Installation

First you need to install [node.js](http://nodejs.org) that comes with the package manager
[npm](https://npmjs.org/).

You need to install or update to the __LTS__ version of Node.js ([version 4.4.5](https://nodejs.org/en/download/) at 
the time of writing). Earlier versions of Node.js aren't supported. 

If you are on the Raspberry Pi and running the standard Raspbian distribution you can use the following installation 
procedure. 

__Pi Model A, B, B+ or Zero__

    wget https://nodejs.org/dist/v4.4.5/node-v4.4.5-linux-armv6l.tar.gz -P /tmp
    cd /usr/local
    sudo tar xzvf /tmp/node-v4.4.5-linux-armv6l.tar.gz --strip=1
    
__Pi 2 Mode B or Pi 3 Model B__

    wget https://nodejs.org/dist/v4.4.5/node-v4.4.5-linux-armv7l.tar.gz -P /tmp
    cd /usr/local
    sudo tar xzvf /tmp/node-v4.4.5-linux-armv7l.tar.gz --strip=1
        
To install node on another platform than Raspberry Pi have a look at 
[installing Node.js via package manager](https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions).

Check you Node.js version with:

    /usr/bin/env node --version

## pimatic Installation

You must have the `gcc` compiler or some other suitable compiler installed. On Debian-based systems run:

    sudo apt-get install build-essential

Once node.js and npm are installed you can run

    cd /home/pi
    mkdir pimatic-app
    npm install pimatic --prefix pimatic-app --production

to install the pimatic framework.

Copy the default config file:

    cd pimatic-app
    cp ./node_modules/pimatic/config_default.json ./config.json

You should end up with these files in your `pimatic-app` directory:

<table class="table file-listing">
<tr><td>`config.json`</td>				       <td>the config file</td></tr>
<tr><td>`node_modules`</td>				       <td>directory for the framework and plugins</td></tr>
<tr><td>`node_modules/pimatic`</td>			   <td>the pimatic framework files</td></tr>
</table>

Now, you need to set the password for the admin user. Open the file `config.json` using a text editor (e.g., `nano`)
and search for the string `"users"`. Then, change the value of the `password` property for user "admin" below.
