---
title: Rules
layout: guide
tags: ['guide', page']
guideOrder: 1040
---

What's a rule
------------
A rule is a string that has the format: "if _this_ then _that_". The _this_ part will be called 
the condition of the rule and the _that_ part the actions of the rule.

__Examples:__

  * if its 10pm then turn the tv off
  * if its friday and its 8am then turn the light on
  * if (music is playing or the light is on) and somebody is present then turn the speaker on
  * if temperature of living room is less than 15°C for 5 minutes then log "its getting cold" 

The condition of a rule consists of one or more predicates. The predicates can be combined with
"and", "or" and can be grouped by parentheses.

__for-suffix__

A predicate can have a "for" as a suffix like in "music is playing for 5 seconds" or 
"tv is on for 2 hours". If the predicate has a for-suffix then the rule action is only triggered,
when the predicate stays true the given time. Predicates that represent one time events like "10pm"
can't have a for-suffix because the condition can never hold.

Predicates
-----------

### Built in

## Switches

Predicate for devices that have a state like switches

  * _device_ is on|off
  * _device_ is switched on|off
  * _device_ is turned on|off

__Examples:__

  * tv is on
  * light is off

## Presence sensors

Predicates for presence sensors like a motion detector  

  * _device_ is present
  * _device_ is not present
  * _device_ is absent

__Examples:__

  * my smartphone is present

## Contact sensors

  * _device_ is opened
  * _device_ is closed

## Variables

  * _expression [==|<|>|<=|>=] _expression_

__Examples:__

  * $tempsetting < 42
  * $device.attribute >= $someVar + 10

## General Device attributes

Predicates for comparing device attributes like sensor value or other states.

  * _attribute_ of _device_ is equal to _value_
  * _attribute_ of _device_ equals _value_
  * _attribute_ of _device_ is not _value_
  * _attribute_ of _device_ is less than _value_
  * _attribute_ of _device_ is lower than _value_
  * _attribute_ of _device_ is greater than _value_
  * _attribute_ of _device_ is higher than _value_

__Examples:__

  * temperature of temperature sensor 1 is lower than 15°C
  * humidity of temperature sensor 1 is greater than 60% 

## Device attribute watchdog
  
  Becomes true if an attribute was not update for a certain time.

  * _attribute_ of _device_ was not updated for _time_

__Examples:__

  * temperature of temperature sensor 1 was not updated for 5 minutes

### chron-Plugin

Provided by the [cron-plugin](http://www.pimatic.org/docs/pimatic-cron/)

  * its _time_
  * its _day_ _time_
  * its _day_

__Examples:__

  * its 8am
  * its 8:00
  * its friday 10pm

### mobile-frontend-Plugin

  * _button text_ is pressed
  * button _button text_ is pressed

__Examples:__

  * watch tv button is pressed

### sunrise-Plugin

  * its _suntime_
  * its _suntime_
  * its _time period_ before|after _suntime_
  * its before|after _suntime_

where _suntime_ is "sunrise", "sunset" or any other [supported suntime event](http://www.pimatic.org/docs/pimatic-sunrise/).

__Examples:__

  * its sunrise
  * its sunset
  * its before sunrise
  * its after sunset
  * its 30 minutes after sunrise
  * its 2h before sunset

Actions
-------

### Built in

## Switches

Actions for devices that can be turned on or off:

  * switch [the] _device_ on|off
  * turn [the] _device_ on|off
  * switch on|off [the] _device_ 
  * turn on|off [the] _device_ 

These actions support a _for_-Suffix to switch the device back to the state before after
a certain time.

__Examples:__

  * turn tv on
  * switch the light off
  * switch the light on for 5 minutes

## Dimmer

Actions dimmer devices. 

  * dim [the] _device_ to _value_[%]

__Examples:__

  * dim couch-light to 30%

## Shutter/screens

Actions for shutter/screen devices:

  * lower [the] _device_ [down]
  * raise [the] _device_ [up]
  * move [the] _device_ up|down
  * stop [the] _device_

These actions support a _for_-Suffix to stop the shutter/screen from moving after
a certain time.

__Examples:__
  
  * raise kitchen-screen 
  * lower kitchen-screen 
  * lower kitchen-screen for 5 seconds
  * stop kitchen-screen 

## Logger

  * log "_a string_"

## Variables

  * set $_varname_ to _expression_

__Examples:__
  
  * set $tempsetting to $tempsetting + 0.5

### shell-execute-Plugin
 
  * execute "_shell-command_"

### mail-Plugin

  * send mail to: "_address_" subject:"_subject_" text:"_text_"

### pushover-Plugin

  * push title:"_title_" message:"_message_" priority:1


Development
------------
Take a look at the [developer documentation](http://www.pimatic.org/docs/lib/rules.html) for how
it works and how to implement your own predicates and actions.