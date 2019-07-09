# Trigger
<br>

This is the model's declaration and setting code in OpenDS.

<br>
<br>


Trigger
-----------
<br>
The declaration and setting of trigger is set in "assets\DrivingTasks\Projects\*
\interaction.xml" file.

<br>
<br>
<font size=4.5> 1. “moveTraffic” activity and trigger</font>


When the traffic object touches this trigger, the specific traffic object (including car, pedestrian) will be set in specific way point position. This trigger is used to implement the appearance of overtaking, low-speed vehicles.


The example code is here:

```bash
<activity id="activity08_1">
    <action id="moveTraffic" delay="0" repeat="4">
        <parameter name="trafficObjectID" value="car3" />
        <parameter name="wayPointID" value="201" />
    </action>
</activity>
```

The activity property is:

1 | 2 | 3 | 4
:- | :- | :- | :-
Activity action id:| moveTraffic	|Delay time: 0 ms|	Repeat number: 4
Parameter id:	|Traffic object id	|The parameter value:|	Traffic object “car3”
Parameter id:|Waypoint id	|The parameter value:	|Waypoint “201”

This trigger's code is here:
```bash
<trigger id="collideWithResetBox1" priority="1">			
    <activities>
        <activity ref="activity08_1"/>
        <activity ref="activity08_9"/>
        <activity ref="activity08_13"/>				
        <activity ref="activity08_15"/>
        <activity ref="activity08_27"/>
    </activities>						
    <condition>collideWith:triggerBox2</condition>
</trigger>

```

The trigger's property is:

1 | 2
:- | :-
Activity reference:|	“activity08_1”,<br> “activity08_9”,<br> “activity08_13”,<br> “activity08_15”,<br> “activity08_27”
Trigger condition:|	One object collides with the model called “triggerBox2”

**<font size=4>
Note: The setting of other activities's trigger are same as this trigger.</font>**
<br>
<br>
<font size=4.5> 2. "requestOffTrafficLight" activity</font>

<br>
<br>
When the traffic object touches this trigger, the specific traffic light will turn to off state. This trigger is used to implement the green-blinking state when the traffic light is turning from green light to yellow light.

The example code is here:


```bash
<activity id="activity21">
    <action id="requestOffTrafficLight" delay="0" repeat="0">
        <parameter name="trafficLightID" value="TrafficLight.00_04" />
    </action>
</activity>

```
This activity's property is :

1 | 2 | 3 | 4
:- | :- | :- | :-
Activity action id:| requestOffTrafficLight	|Delay time: 0 s|	Repeat number: 0
Parameter id:	|Traffic light id	|The parameter value:|	TrafficLight.00_04


<br>
<font size=4.5> 3. "setGreenTrafficLight" activity</font>

<br>
<br>
When the traffic object touches this trigger, the specific traffic light will turn to green state. This trigger is used to set the specific traffic light turn to green immediately.

The example code is here:


```bash
<activity id="activity30">
    <action id="setGreenTrafficLight" delay="0.5" repeat="0">
        <parameter name="trafficLightID" value="TrafficLight.00_04" />
    </action>
</activity>

```
This activity's property is :

1 | 2 | 3 | 4
:- | :- | :- | :-
Activity action id:| setGreenTrafficLight	|Delay time: 0.5 s|	Repeat number: 0
Parameter id:	|Traffic light id	|The parameter value:|	TrafficLight.00_04


<br>
<font size=4.5> 4. "requestGreenTrafficLight" activity</font>

<br>
<br>
When the traffic object touches this trigger, the specific traffic light will turn to green state if the required-red traffic lights of this traffic light are red state in the current state. If the some required-red traffic lights aren't red state now, these traffic light will be set to red state immediately. This trigger is used to let the specific traffic light turn to green and make sure the traffic lights at the same intersection do not conflict.

The example code is here:


```bash
<activity id="activity20">
    <action id="requestGreenTrafficLight" delay="0" repeat="0">
        <parameter name="trafficLightID" value="TrafficLight.00_04" />
    </action>
</activity>

```

This activity's property is basicly same as the "setGreenTrafficLight" activity.

<br>
<font size=4.5> 5. "startRecording" activity</font>

<br>
<br>
When the traffic object touches this trigger, the simulator will automaticly start to record the steering car's behaviour.

he example code is here:


```bash
<activity id="activity00">
    <action id="startRecording" delay="0" repeat="4">
        <parameter name="track" value="1" />
    </action>
</activity>

```
This activity's property is :

1 | 2 | 3 | 4
:- | :- | :- | :-
Activity action id:| startRecording	|Delay time: 0 s|	Repeat number: 4
Parameter id:	|Track	|The parameter value:|	1
