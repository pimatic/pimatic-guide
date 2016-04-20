---
title: API
layout: guide
tags: ['guide', page']
guideOrder: 1500
---

Pimatic features a rich API for external scripting or frontends. The API can be accessed in two
ways:

  * The REST-API: Using standard HTTP-Requests.
  * The websocket-API: Using websockets and the socket.io protocol.

## REST-API

The REST-API fits best for simple tasks because it is easy to use and implement. You could for 
example read the value of the variable `$the-answer` value by a simple HTTP-Request using curl:

    curl \
      -X GET \
      --user "user:password" \
      http://your-pimatic/api/variables/the-answer

This yields:

    {
      "variable": {
        "name": "the-answer",
        "readonly": false,
        "type": "value",
        "value": 42
      },
      "success": true
    }

You can also create (using 'POST') or update (using 'PATCH') the value of a variable:

    curl \
      -X PATCH \
      --header "Content-Type:application/json" \
      --data '{"type": "value", "valueOrExpression": 1337}' \
      --user "user:password" \
      http://your-pimatic/api/variables/the-answer 

See the [API-Docs](/api/actions) for a list of all available functions.

## websocket-API

The websocket-API is the second method to interact with pimatic. The Advantage over the REST-API
is that you get live events, if something in pimatic changes. On top of websockets pimatic is
using the [socket.io Protocol](https://github.com/Automattic/socket.io-protocol) to send and 
receive messages.

A simple example:

    var io = require('socket.io-client');

    var host = 'your-pimatic';
    var port = 80;
    var u = encodeURIComponent('your-username');
    var p = encodeURIComponent('your-password');
    var socket = io('http://' + host + ':' + port + '/?username=' + u + '&password=' + p, {
      reconnection: true,
      reconnectionDelay: 1000,
      reconnectionDelayMax: 3000,
      timeout: 20000,
      forceNew: true
    });

    socket.on('connect', function() {
      console.log('connected');
    });

    socket.on('event', function(data) {
      console.log(data);
    });

    socket.on('disconnect', function(data) {
      console.log('disconnected');
    });

    socket.on('devices', function(devices){
      console.log(devices);
    });

    socket.on('rules', function(rules){
      console.log(rules); 
    });

    socket.on('variables', function(variables){
      console.log(variables); 
    });

    socket.on('pages', function(pages){
      console.log(pages); 
    });

    socket.on('groups', function(groups){
      console.log(groups); 
    });

    socket.on('deviceAttributeChanged', function(attrEvent) {
      console.log(attrEvent);
    });

You can also call actions from the socket.io connection:

    socket.emit('call', {
      id: 'update-variable-call1',
      action: 'updateVariable',
      params: {
        name: 'the-answer',
        type: 'value',
        valueOrExpression: 1337
      }
    });

    socket.on('callResult', function(msg){
      if(msg.id === 'update-variable-call1') {
        console.log(msg.result);
      }
    });

For performance reasons the "production" mode uses minified and pre-compiled code. If you need to debug the mobile frontend code, e.g., as you are developing a mobile frontend extension, set the mode as part of the plugin configuration to "development". Then clear all browser caches and delete all app settings. Best is to use an incognito tab for testing.