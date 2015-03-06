---
title: API
layout: guide
tags: ['guide', page']
guideOrder: 1500
---

Pimatic features a rich API for external scripting or frontends. The API can be accessed in two
ways:

  * The REST-API: Using standrard HTTP-Requests.
  * The websocket-API: Using websockets and the socket.io protocol.

## REST-API

The REST-API fits best for simple tasks because it is easy to use and implement. You could for 
example read the value of the variable `$the-answer` by a simple HTTP-Request using curl:

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

The websocket-API is the second method to interact with pimatic. The Advantage over the REST-API is that you get live events, if something in pimatic changes. On top of websockets, pimatic
is using the [socket.io Protocol](https://github.com/Automattic/socket.io-protocol) to send and receive messages.

A simple axample:

    var socket = io('http://your-pimatic/');
    io.on('connection', function(socket){
      console.log('connected');
      
      socket.socket.on('devices', function(devices){
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

      socket.on("deviceAttributeChanged", (attrEvent) -> 
        console.log(attrEvent);
      });

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
