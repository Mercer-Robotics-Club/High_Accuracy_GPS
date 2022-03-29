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
  
## Rover Batteries
The rover batteries we used are *****

## Rover Wiring
In terms of wiring on the rover, I have included a graphic showing the different components of the rover wired together below. ***

## Pixhawk Microcontroller

The 3DR Pixhawk 1 Flight Controller (Currently Discontinued) is the main brain of the operation. It loads up the current mission set and takes in current GPS location to determine route the rover must take. The Pixhawk then controls the rover motor controller to move the rover in the route direction while live updating position and route. The Pixhawk also connects to our base-station laptop to see live update on the mission and communicate commands to the Pixhawk.

All other specifications on the Pixhawk Microcontroller as well as the different inputs, outputs, and guide to implement can be found <a href = "https://docs.px4.io/master/en/flight_controller/pixhawk.html">here</a> as well as throughout the PX4 User guide on the same webpage.

<p align = "center">
  <img src = "https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Images/Screenshot%20from%202022-03-28%2014-50-32.png" />
</p>

## Rover Low Accuracy GPS Module


## Rover RTK GPS Modules

## Rover Power Management

## Rover communication with Base-Station/User

