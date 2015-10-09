---
title: Extending the mobile frontend
layout: guide
tags: ['guide', page']
guideOrder: 2060
---

### Basics

You can add custom JavaScript/CoffeeScript, HTML/Jade and CSS files to the mobile frontend from your plugin:

<script src="https://gist.github.com/sweetpi/901c222517bd627a50b3.js?file=adding-files.coffee"></script>

The HTML/Jade files will get appended to the `body` element of the index page. The JS/CoffeeScript and CSS files 
will be inserted in the html `head` element.

### Device templates

You can create your own frontend item templates for your devices. First add a `getTemplate`-function to your device:

<script src="https://gist.github.com/sweetpi/9157350.js?file=template.coffee"></script>

Then you need to define the HTML-template with the a corresponding id in an extra added HTML/Jade file:

<script src="https://gist.github.com/sweetpi/901c222517bd627a50b3.js?file=item-template.html"></script>

and define the behavior by adding a item class in an extra added JS/CS file;

<script src="https://gist.github.com/sweetpi/901c222517bd627a50b3.js?file=item-class.coffee"></script>

You can take a look on the [existing item classes](https://github.com/pimatic/pimatic-mobile-frontend/blob/master/app/pages/index-items.coffee) for examples.