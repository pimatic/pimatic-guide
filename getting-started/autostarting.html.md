---
title: Autostarting
layout: guide
tags: ['guide', page']
guideOrder: 77
---
You can autostart pimatic by additional installing the init.d script:

    wget https://raw.github.com/pimatic/pimatic/master/install/pimatic-init-d
    sudo cp pimatic-init-d /etc/init.d/pimatic
    sudo chmod +x /etc/init.d/pimatic
    sudo chown root:root /etc/init.d/pimatic
    sudo update-rc.d pimatic defaults

It should now start with:
  
    sudo service pimatic start

and log the outputs to: `pimatic-app/pimatic-daemon.log`