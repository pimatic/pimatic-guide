---
title: Installation
layout: guide
tags: ['guide', page']
guideOrder: 10
---

## Node.js Installation

First you need to install [node.js](http://nodejs.org) that comes with the package manager
[npm](https://npmjs.org/).

You need to install Node.js version __0.10__. (Node.js 0.11/0.12 isn't supported by all plugins yet.)
If you are on the Raspberry Pi and running the standard Raspbian distribution you can use this:

    wget http://nodejs.org/dist/v0.10.24/node-v0.10.24-linux-arm-pi.tar.gz -P /tmp
    cd /usr/local
    sudo tar xzvf /tmp/node-v0.10.24-linux-arm-pi.tar.gz --strip=1

Node.js for other Raspberry Pi releases can be found [here](https://gist.github.com/adammw/3245130/).

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
