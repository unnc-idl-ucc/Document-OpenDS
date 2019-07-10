# Model

<br>
This is the **model's declaration and setting code** in OpenDS.

<!--te-->
<br>
<br>

Model
-----
<br>
<font size=4.5>    1. Traffic light </font>

<br>
<br>
The traffic light model is set in the “assets\DrivingTasks\Projects\*
\scene.xml” file, including the model’s id, mass, visibility, collision shape, scale, rotation, translation (position), user can change the model property by changing this file’s content.
<br>
<br>

(Note: **“*”** means any project name such as “Paris”.)

Code example is here:
```bash
<model id="TrafficLight.00_01" key="Models/TrafficLight/trafficlight.scene" ref="">
    <mass>0</mass>
    <visible>true</visible>
    <collisionShape>meshShape</collisionShape>
    <scale>
        <vector jtype="java_lang_Float" size="3">
           <entry>1</entry>
           <entry>1</entry>
           <entry>1</entry>
        </vector>
    </scale>
    <rotation quaternion="false">
        <vector jtype="java_lang_Float" size="3">
            <entry>0</entry>
            <entry>-86.9</entry>
            <entry>0</entry>
        </vector>
    </rotation>
    <translation>
        <vector jtype="java_lang_Float" size="3">
            <entry>406</entry>
            <entry>0</entry>
            <entry>193</entry>
        </vector>
    </translation>
</model>		
```

As the code shows, this traffic light model’s property is:


mass|	0
:- | :-
visibility|	Visible
Collision shape|	Mesh shape
Scale in 3 dimensions	|(1, 1, 1)
Rotation in 3 dimensions	|(0, -86.9, 0)
Translation in 3 dimensions	|(406, 0, 193)

<br>
The interaction between traffic lights and the intersection setting is set in “assets\DrivingTasks\Projects\*\scenario.xml” file. Each intersection contains several traffic lights, the states of these traffic lights (e.t. red, yellow, green, off) in one moment as a “phase”, the specific phase duration. Moreover, the traffic light has several shapes, such as left narrow, circular, right narrow, when some traffic lights are green, some specific traffic lights must be red (to avoid the traffic lights in different direction are green simultaneously). These also should be set in “assets\DrivingTasks\Projects\*\scenario.xml” file.
<br>
<br>

(Note: **“*”** means any project name such as “Paris”.)

Code example is here:

```bash
<intersection id="Intersection0" mode="trigger">
    <phases>				
        <phase id="02" duration="50" state="rrrx"/>
        <phase id="03" duration="50" state="rrry"/>
        <phase id="04" duration="300" state="rrrg"/>
    </phases>
    <trafficLights>
        <trafficLight id="TrafficLight.00_01" phasePosition="1">
            <initialState>red</initialState>
            <direction>none</direction>
            <requiresRed>TrafficLight.00_03,TrafficLight.00_04</requiresRed>
        </trafficLight>
        <trafficLight id="TrafficLight.00_02" phasePosition="2">
          <initialState>red</initialState>
          <direction>none</direction>
          <requiresRed>TrafficLight.00_03,TrafficLight.00_04</requiresRed>
        </trafficLight>
        <trafficLight id="TrafficLight.00_03" phasePosition="3">
            <initialState>red</initialState>
            <direction>none</direction>
            <requiresRed>TrafficLight.00_01,TrafficLight.00_02</requiresRed>
        </trafficLight>
        <trafficLight id="TrafficLight.00_04" phasePosition="4">
            <initialState>red</initialState>
            <direction>none</direction>
            <requiresRed>TrafficLight.00_01,TrafficLight.00_02</requiresRed>
        </trafficLight>
    </trafficLights>
</intersection>

```
<br>

As the code shows, this intersection has 4 traffic light: “TrafficLight.01_01”, “TrafficLight.01_02”, “TrafficLight.01_03”, “TrafficLight.01_04”, the  former id “01” is intersection id, the latter id is traffic light id in this intersection. In addition, there are 3 declared phase state: “04”, “05”, “06”, each phase has duration and specific traffic light states. Moreover, every traffic light
declared in there has a phase position, a direction shape which point to the light’s corresponding turning direction and the traffic light set which must be red when this light is green.

1 | 2 | 3
:- | :- | :-
Phase 04|	Duration: 50 ms	|4 traffic light states: “red, red, red, yellow&red”
Phase 05|	Duration: 50 ms	|4 traffic light states: “red, red, red, yellow”
Phase 06|	Duration: 50 ms	|4 traffic light states: “red, red, red, green”
Traffic light “01_01”	|Direction:	no direction|	Required red traffic light set: “01_03”, “01_04”
Traffic light “01_02”	|Direction:	no direction	|Required red traffic light set: “01_03”, “01_04”
Traffic light “01_03”|	Direction:	no direction|	Required red traffic light set: “01_01”, “01_02”
Traffic light “01_04”	|Direction:	no direction	|Required red traffic light set: “01_01”, “01_02”



The green light trigger is set in “assets\DrivingTasks\Projects\*
\interaction.xml” file. These is a trigger model in the scenario, when the traffic objects touch this trigger model (unless this object mass is 0), the corresponding traffic light will turn green in specific time. The trigger model is set in “assets\DrivingTasks\Projects\*\scene.xml” file.
(Note: **“*”** means any project name such as “Paris”.) The example code is here:



<br>
<font size=4.5>    2.	Automatic driving car and pedestrian </font>

<br>
<br>
The car model, pedestrian model and its properties are declared in “assets\DrivingTasks\
Projects\*\scenario.xml”, the car automaticly driving by following the route of these way points with specific speed. The way point position can be set either in “assets\DrivingTasks\Projects\*\scene.xml” or “assets\ DrivingTasks\Projects\*\scenario.xml”.
Code example is here:

```bash
<vehicle id="car3">
    <modelPath>Models/Cars/drivingCars/AudiS6/Car.j3o</modelPath>
    <mass>800</mass>
    <acceleration>20</acceleration>
    <decelerationBrake>8.7</decelerationBrake>
    <decelerationFreeWheel>2.0</decelerationFreeWheel>
    <engineOn>true</engineOn>
    <maxDistanceFromPath>3.0</maxDistanceFromPath>
    <curveTension>0.05</curveTension>
    <pathIsCycle>false</pathIsCycle>
    <pathIsVisible>true</pathIsVisible>
    <startWayPoint>207</startWayPoint>
    <wayPoints>
        <wayPoint ref="200"><speed>50</speed></wayPoint>					
        <wayPoint ref="201"><speed>50</speed></wayPoint>
        <wayPoint ref="202"><speed>50</speed></wayPoint>
        <wayPoint ref="203"><speed>50</speed></wayPoint>
        <wayPoint ref="204"><speed>120</speed></wayPoint>					
        <wayPoint ref="205"><speed>120</speed><trafficLight>TrafficLight.03_04</trafficLight></wayPoint>
        <wayPoint ref="206"><speed>120</speed></wayPoint>
        <wayPoint ref="207"><speed>120</speed></wayPoint>					
    </wayPoints>
</vehicle>
```
The vehicle property is:

1 | 2
:- | :-
Vehicle model path:	|Models/Cars/drivingCars/citroenC4/Car.j3o
Vehicle mass:|	800 kg
Vehicle acceleration:|	20 m/s2
Vehicle	deceleration brake:	|8.7 m/s2
Free wheel number when	vehicle	is decelerated:	|2.0
Initial engine state:|	On
Maximum	distance from path:	|3 meters
Curve	tension	of waypoint:|	0.05
Whether	the waypoint	path	is cycle:|	False
Path visibility:|	True
Starting waypoint:|	Waypoint “207”
Waypoint set：|	------------------
Speed limit between Waypoints: |25km/h  **Or**   120km/h

<br>
<br>
Pedestrian is quite similar with the auto-driving car. Besides, the pedestrian animation (walking posture, stand posture) can be set.
The code example is here:


```bash
<pedestrian id="pedestrian01">
    <modelPath>Models/Humans/male/male.scene</modelPath>
    <mass>50</mass>
    <animationStand>Stand</animationStand>
    <animationWalk>WalkBaked</animationWalk>
    <scale>0.9</scale>
    <maxDistanceFromPath>1.1</maxDistanceFromPath>
    <curveTension>0.1</curveTension>
    <pathIsCycle>true</pathIsCycle>
    <pathIsVisible>false</pathIsVisible>
    <startWayPoint>WayPoint_1</startWayPoint>
    <wayPoints>
        <wayPoint id="WayPoint_1"><translation><vector jtype="java_lang_Float" size="3"><entry>650</entry><entry>0</entry><entry>913</entry></vector></translation><speed>3</speed></wayPoint>
        <wayPoint id="WayPoint_2"><translation><vector jtype="java_lang_Float" size="3"><entry>708</entry><entry>0</entry><entry>913</entry></vector></translation><speed>3</speed><trafficLight>TrafficLight.02_01</trafficLight></wayPoint>
        <wayPoint id="WayPoint_3"><translation><vector jtype="java_lang_Float" size="3"><entry>800</entry><entry>0</entry><entry>913</entry></vector></translation><speed>3</speed></wayPoint>
        <wayPoint id="WayPoint_4"><translation><vector jtype="java_lang_Float" size="3"><entry>721</entry><entry>0</entry><entry>913</entry></vector></translation><speed>3</speed><trafficLight>TrafficLight.02_01</trafficLight></wayPoint>					
    </wayPoints>											
</pedestrian>
```

The pedestrian property is:

1 | 2
:- | :-
pedestrian model path:	|Models/Humans/female/female.scene
Pedestrian mass:|	50 kg
Stand	animation type:|	"Stand"
Walk animation type:	|"WalkBaked"
Scale: | 0.9
Maximum	distance from path:|	1.1 meter
Curve	tension	of waypoint:|	0.1
Whether	the waypoint	path	is cycle:	|True
Path visibility:|	False
Starting waypoint:|	Waypoint “WayPoint_1”
Waypoint set：|	------------------
Speed limit between Waypoints: |3km/h
Traffic Light to be waited for:| TrafficLight.02_01


<br>
