# Rover Hardware

This document is used to show how the hardware is setup on the rover module. Based on your use case, you can follow some of our steps when implementing the RTK-GPS system into your project.

## Rover Chassis

<p align>
The rover chassis was already built and setup when we first got onto the project. We were able to find the rover chassis from <a href = https://www.generationrobots.com/en/401506-wild-thumper-6x6-chassis-with-75-1-motors.html> this website </a>. Specs of the rover, dimensions, and motor specifications are in the website.
</p>

<p align ="center">
  <img src = "https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Images/Screenshot%20from%202022-03-28%2014-20-21.png" />
</p>


## Rover Motors

Our chassis came with motors geared 75:1 and all specifications we know of can be found <a href = https://www.generationrobots.com/en/401506-wild-thumper-6x6-chassis-with-75-1-motors.html> here </a>

## Rover Motor Controller

The motor controller is used to power the 6 motors on the rover as well as send signals for when to rotate clockwise, counter-clockwise, or turn off. The specific motor controller that was already set in the rover can be found <a href = "https://www.dimensionengineering.com/products/sabertooth2x25">here</a>

<p align = "center">
  <img src = "https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Images/Screenshot%20from%202022-03-28%2014-46-53.png" />
</p>
  
Preface that the motor controller has 2 outputs. Each side of the rover corresponds to 1 output on the motor controller so all motors on one side of the rover all rotate together in the same fashion (Each side refers to 3 motors left and right of main body like left and right side of a car).

## Rover Batteries
The rover batteries we used are 2 LiPo Batteries which are both 5200 mAh at 7.4 V and 35 C. A picture of one of the batteries is shown below. 

<p align = "center">
  <img src = "https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Images/20220331_130618.jpg" />
</p>

We did not do any testing on whether these batteries we best for our application as these were already included in the Rover setup when given to us. They worked right from powering on and we decided not to do any more research/changes on the battery.

## Rover Wiring
In terms of wiring on the rover, I have included a graphic showing the different components of the rover wired together below. (!!! include wiring setup for the low accuracy testing and high accuracy testing --Real pictures and diagrams for both!!!!)

## Pixhawk Microcontroller

The 3DR Pixhawk 1 Flight Controller (Currently Discontinued) is the main brain of the operation. It loads up the current mission set and takes in current GPS location to determine route the rover must take. The Pixhawk then controls the rover motor controller to move the rover in the route direction while live updating position and route. The Pixhawk also connects to our base-station laptop to see live update on the mission and communicate commands to the Pixhawk.

All other specifications on the Pixhawk Microcontroller as well as the different inputs, outputs, and guide to implement can be found <a href = "https://docs.px4.io/master/en/flight_controller/pixhawk.html">here</a> as well as throughout the PX4 User guide on the same webpage.

<p align = "center">
  <img src = "https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Images/Screenshot%20from%202022-03-28%2014-50-32.png" />
</p>

## Rover Low Accuracy GPS Module
The low accuracy GPS module we used in our low accuracy testing is the 3DR uBlox GPS With Compass. A picture of it is shown below and the GPS module can be found and bought <a href = https://uavsystemsinternational.com/products/3dr-ublox-gps-with-compass> here </a>.

<p align = "center">
  <img src = "https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Images/GPS_TopAndSide.jpg" />
</p>

Documentation on how to use it, in combination with the Pixhawk can be found <a href = https://ardupilot.org/copter/docs/common-installing-3dr-ublox-gps-compass-module.html> here </a>. This GPS module comes with a compass which we utilized, in combination with the compass built in to the Pixhawk, for direction. This compass setup was used in our low accuracy and high accuracy GPS testing. Wiring for this setup was different in each situation and included in the [Rover Wiring][Hardware.md#Rover_Wiring] section. Setup for both compasses is included in the (!!!Include which software section for compass setup!!!).

This low accuracy GPS module worked great in testing (Based on performance in intial README) and was included in the rover setup when it was given to us. In high accuracy testing the module was only used for it's compass as we saw it perform better in combination with the Pixhawk built-in compass.

## Rover RTK GPS Modules

## Rover communication with Base-Station/User

