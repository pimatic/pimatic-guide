---
title: Autostarting
layout: guide
tags: ['guide', page']
guideOrder: 77
---
You can autostart pimatic by additionally installing the init.d script:

    wget https://raw.githubusercontent.com/pimatic/pimatic/v0.9.x/install/pimatic-init-d
    sudo cp pimatic-init-d /etc/init.d/pimatic
    sudo chmod +x /etc/init.d/pimatic
    sudo chown root:root /etc/init.d/pimatic
    sudo update-rc.d pimatic defaults

It should now start with:

    sudo service pimatic start

and log the output to: `pimatic-app/pimatic-daemon.log`
