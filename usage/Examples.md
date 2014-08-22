---
title: Examples
layout: guide
tags: ['guide', page']
guideOrder: 1050
---

### How to make creative use of the features of pimatic and its plugin.

Using a Up/Down arrow device to lower or increase a value
First, implement a Screen or Shutter device in pimatic. This can be done by adding a Screen device pin Pilight (use a fake address). Now that we have Up and Down buttons, make a variable and some rules for it to use them.
Create a variable containing the value you want to change, let's call it $TemperatureSetting
After this, create the follwoing rules:

    IF position of pilight-screen = down
    THEN $TemperatureSetting = $TemperatureSetting - 1 AND stop pilight-screen

    IF position of pilight-screen = up
    THEN $TemperatureSetting = $TemperatureSetting + 1 AND stop pilight-screen

This will decrease and increase the value of $TemperatureSetting but also set the buttons to a stopped state (neutral stand).

Detect rising and falling of temperature to turn off central heating
When using Pimatic for central heating, you will find out it will just do what you tell the rules to do. When it is to cold, it will turn on the heat. Simple as that. With the following variables and rules, you can prevent pimatic from turning on the heat as long as the temperature is rising by itself - even if it is to cold. This example will asume you have a device called 'heat', to turn the central heating on or off.
Create the following variables: $PreviousTemp & $WarmsUp
Now create the following rules:

    IF $pilight-thermostaat-woonkamerwireless.temperature > $PreviousTemp and heat is turned off
    THEN $WamrsUp = 1 and $PreviousTemp = $pilight-thermostaat-woonkamerwireless.temperature

    IF $pilight-thermostaat-woonkamerwireless.temperature < $PreviousTemp and heat is turned off
    THEN $WamrsUp = 0 and $PreviousTemp = $pilight-thermostaat-woonkamerwireless.temperature

Now edit your rule responsible for turning the central heating on:

IF $pilight-thermostaat-woonkamerwireless.temperature < ($TemperatuurInstelling - $ThermostaatMarge) and heat is turned off and $WarmsUp = 0 and $BlockHeat = 0 for 5 minutes
THEN turn heat on

Offcourse, don't use the $WarmsUp in your rule to turn it off, because it will allways be heating up when the Central Heating is on ;)

### How to work with various timesets to change the desired temperature for heating.


When I started with Pimatic, I created a different rule for every time window to stop and start heating based on temperatures. Since the feature of variabels in Pimatic I have changed this way of regulating temperature.
Let me explain the way I control my Central Heating ..
  
  * First, create the following variable: $DesiredTemp
  * After that, create some normal on/off switches: RunProgram & TodaySunday
  * Now, create a set of rules for every time window you have. I will give a few of mine:


  IF it is before 06:00 and pilight-thermostaat-runprogram is on
  THEN $DesiredTemp = 18

  IF it is after 06:00 and before 07:30 and pilight-thermostaat-runprogram is on
  THEN $DesiredTemp = 18

  IF  it is monday or tuesday or thursday or friday and it is after 07:30 and before 14:00 and pilight-thermostaat-runprogram is on and pilight-thermostaat-sunday is off
  THEN $DesiredTemp = 18

  IF it is wednesday or saturday or sunday or pilight-thermostaat-sunday is turned on and it is after 07:30 and before 22:00 and pilight-thermostaat-runprogram is on
  THEN $DesiredTemp = 20

Now you have some rules that will change the desired temperature to the temperature that fits the normal daily situation.
When you use the rule to turn on Central HEating from the previous exmaple, it will automaticly turn on the heating when needed.
To turn off:

  IF $pilight-thermostaat-woonkamerwireless.temperature > ($TemperatuurInstelling+ $ThermostaatMarge) and warmte is turned on
  THEN turn heat off

As you may notice, a also use a variable called $ThermostaatMarge this is a variable that contains the value of 0.2 and is used to prevent togglig the on and off to much.

In all my Central Heating rules I make use of a $BlockHeat variable. Whenever this value is 1 or higher, Central Heating s cut off immediately. Turning on is only allowed when it is 0 for at least 5 minutes.
When it is spring, and you open the door to the garden for fresh air you living room meet getting colder then desired (according to the rules). Therefor I set $Blockheat to +1 the moment it detects opening the door. It is was allready heating, it is turned down. When the door is closed again, it needs to be closed for 5 minutes before heating is allowed. If it is still to cold, but the temperature is still rising (see earlier example) it still will not turn on heating.

The switch Today as Sunday is used to tell pimatic to follow the rules for a sunday (usualy a day that you will be home the entire day), so you can flip that switch when you deside to stay the day at home.





