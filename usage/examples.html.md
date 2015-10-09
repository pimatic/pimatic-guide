---
title: Examples
layout: guide
tags: ['guide', page']
guideOrder: 1050
---

### How to make creative use of the features of pimatic and its plugin.

__Using an Up/Down arrow device to lower or increase a value__

First, implement a Screen or Shutter device in pimatic. This can be done by adding a Screen device in Pilight (use a fake address). Now that we have Up and Down buttons, make a variable and some rules for it to use them.
Create a variable containing the value you want to change, let's call it $TemperatureSetting
Following this, create the following rules:

    IF position of pilight-screen = down
    THEN $TemperatureSetting = $TemperatureSetting - 1 AND stop pilight-screen

    IF position of pilight-screen = up
    THEN $TemperatureSetting = $TemperatureSetting + 1 AND stop pilight-screen

This will decrease and increase the value of $TemperatureSetting but also set the buttons to a stopped state (neutral stand).

__Detect rising and falling of temperature to turn off central heating__

When using Pimatic for central heating, you will find out it will just do what you tell the rules to do. When it is too
cold, it will turn on the heating. Simple as that. With the following variables and rules, you can prevent pimatic
from turning on the heating as long as the temperature is rising by itself - even if it is to cold. This example
assumes you have a device called 'heat', to turn the central heating on or off.

Create the following variables: $PreviousTemp & $WarmsUp

Now, create the following rules:

    IF $pilight-thermostaat-woonkamerwireless.temperature > $PreviousTemp and heat is turned off
    THEN $WamrsUp = 1 and $PreviousTemp = $pilight-thermostaat-woonkamerwireless.temperature

    IF $pilight-thermostaat-woonkamerwireless.temperature < $PreviousTemp and heat is turned off
    THEN $WamrsUp = 0 and $PreviousTemp = $pilight-thermostaat-woonkamerwireless.temperature

Now, edit your rule responsible for turning the central heating on:

    IF $pilight-thermostaat-woonkamerwireless.temperature < ($TemperatuurInstelling - $ThermostaatMarge)
       and heat is turned off and $WarmsUp = 0 and $BlockHeat = 0 for 5 minutes
    THEN turn heat on

However, don't use the $WarmsUp in your rule to turn it off, because it will always be heating up when the Central Heating is on ;)

### How to work with various time-based settings to change the desired temperature for heating


When I started with Pimatic, I created a different rule for every time window to stop and start heating based on temperatures. Since the feature of variables in Pimatic I have changed this way of regulating temperature.
Let me explain the way I control my Central Heating:

  * First, create the following variable: $DesiredTemp
  * After that, create some normal on/off switches: RunProgram & TodaySunday
  * Now, create a set of rules for every time window you have. I will give a few of mine:

Rules:

    IF it is before 06:00 and pilight-thermostaat-runprogram is on
    THEN $DesiredTemp = 18

    IF it is after 06:00 and before 07:30 and pilight-thermostaat-runprogram is on
    THEN $DesiredTemp = 18

    IF it is Monday or Tuesday or Thursday or Friday and it is after 07:30 and before 14:00
        and pilight-thermostaat-runprogram is on and pilight-thermostaat-sunday is off
    THEN $DesiredTemp = 18

    IF it is Wednesday or Saturday or Sunday or pilight-thermostaat-sunday is turned on
       and it is after 07:30 and before 22:00 and pilight-thermostaat-runprogram is on
    THEN $DesiredTemp = 20

Now, you have some rules that will change the desired temperature to the temperature that fits the normal daily situation.
When you use the rule to turn on Central Heating from the previous example, it will automatically turn on the heating when needed.
To turn it off:

    IF $pilight-thermostaat-woonkamerwireless.temperature > ($TemperatuurInstelling+ $ThermostaatMarge) and warmte is turned on
    THEN turn heat off

As you may notice, the rule also uses a variable called $ThermostaatMarge. This is a variable that contains the value of 0.2 and is used to prevent toggling the on and off to much.

In all my Central Heating rules I make use of a $BlockHeat variable. Whenever this value is 1 or higher, Central Heating is cut off immediately. Turning on is only allowed when it is 0 for at least 5 minutes.
When it is spring, and you open the door to the garden for fresh air you living room may getting colder then desired (according to the rules). Therefor I set $Blockheat to +1 the moment it detects opening the door. If it was already heating, it is turned down. When the door is closed again, it needs to be closed for 5 minutes before heating is allowed. If it is still to cold, but the temperature is still rising (see earlier example) it still will not turn on heating.

The switch Today as Sunday is used to tell pimatic to follow the rules for a Sunday (usually a day that you will be home the entire day), so you can flip that switch when you decide to stay the day at home.
