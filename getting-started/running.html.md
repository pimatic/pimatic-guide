---
title: Running
layout: guide
tags: ['guide', page']
guideOrder: 30
---
The server can be started with

    sudo node_modules/pimatic/pimatic.js

To daemonize pimatic you can run:

    sudo node_modules/pimatic/pimatic.js start

You can also use `status`, `stop`, `restart`.

### Installing globally

To make pimatic available globally you can run:

    cd ./node_modules/pimatic
    sudo npm link

Then pimatic can be used with:

    sudo pimatic.js [start|stop|status|restart]
