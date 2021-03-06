# Rover Hardware

This document is used to show how the hardware is setup on the rover module. Based on your use case, you can follow some of our steps when implementing the RTK-GPS system into your project.

- [Rover Chassis](Hardware.md#rover-chassis)
- [Rover Motors](Hardware.md#rover-motors)
- [Rover Motor Controller](Hardware.md#rover-motor-controller)
- [Rover Batteries](Hardware.md#rover-batteries)
- [Rover Microcontroller](Hardware.md#rover-microcontroller)
- [Rover Low Accuracy GPS Module](Hardware.md#rover-low-accuracy-gps-module)
- [Rover RTK GPS Modules](Hardware.md#rover-rtk-gps-modules)
- [Rover Power Management](Hardware.md#rover-power-management)
- [Rover Communication with Base-Station/User](Hardware.md#rover-communication-with-base-stationuser)
- [Rover Wiring](Hardware.md#rover-wiring)

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
### Sabertooth dual 25A motor driver

The motor controller is used to power the 6 motors on the rover as well as send signals for when to rotate clockwise, counter-clockwise, or turn off. The specific motor controller that was already set in the rover can be found <a href = "https://www.dimensionengineering.com/products/sabertooth2x25">here</a>

<p align = "center">
  <img src = "https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Images/Screenshot%20from%202022-03-28%2014-46-53.png" />
</p>
  
Preface that the motor controller has 2 outputs. Each side of the rover corresponds to 1 output on the motor controller so all motors on one side of the rover all rotate together in the same fashion (Each side refers to 3 motors left and right of main body like left and right side of a car).

## Rover Batteries
### 2S LiPo Batteries, 35 C, 5200 mAh

The rover batteries we used are 2 LiPo Batteries which are both 5200 mAh at 7.4 V and 35 C. A picture of one of the batteries is shown below. 

<p align = "center">
  <img src = "https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Images/20220331_130618.jpg" />
</p>

We did not do any testing on whether these batteries we best for our application as these were already included in the Rover setup when given to us. They worked right from powering on and we decided not to do any more research/changes on the battery.

## Rover Microcontroller
### 3DR Pixhawk 1 Flight Controller (Discontinued)

The 3DR Pixhawk 1 Flight Controller (Currently Discontinued) is the main brain of the operation. It loads up the current mission set and takes in current GPS location to determine route the rover must take. The Pixhawk then controls the rover motor controller to move the rover in the route direction while live updating position and route. The Pixhawk also connects to our base-station laptop to see live update on the mission and communicate commands to the Pixhawk.

All other specifications on the Pixhawk Microcontroller as well as the different inputs, outputs, and guide to implement can be found <a href = "https://docs.px4.io/master/en/flight_controller/pixhawk.html">here</a> as well as throughout the PX4 User guide on the same webpage.

<p align = "center">
  <img src = "https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Images/Screenshot%20from%202022-03-28%2014-50-32.png" />
</p>

## Rover Low Accuracy GPS Module
### 3DR uBlox GPS with Compass

The low accuracy GPS module we used in our low accuracy testing is the 3DR uBlox GPS With Compass. A picture of it is shown below and the GPS module can be found and bought <a href = https://uavsystemsinternational.com/products/3dr-ublox-gps-with-compass> here </a>.

<p align = "center">
  <img src = "https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Images/GPS_TopAndSide.jpg" />
</p>

Documentation on how to use it, in combination with the Pixhawk can be found <a href = https://ardupilot.org/copter/docs/common-installing-3dr-ublox-gps-compass-module.html> here </a>. This GPS module comes with a compass which we utilized, in combination with the compass built in to the Pixhawk, for direction. This compass setup was used in our low accuracy and high accuracy GPS testing. Wiring for this setup was different in each situation and included in the [Rover Wiring][Hardware.md#Rover_Wiring] section. Setup for both compasses is included in the (!!!Include which software section for compass setup!!!).

This low accuracy GPS module worked great in testing (Based on performance in intial README) and was included in the rover setup when it was given to us. In high accuracy testing the module was only used for it's compass as we saw it perform better in combination with the Pixhawk built-in compass.

## Rover RTK GPS Modules
### uBlox C94-M8P

The RTK GPS modules we used in our project is the C94-M8P RTK module sold by U-Blox and can be found <a href = https://www.u-blox.com/en/product/c94-m8p> here </a>. This page also includes downloads for quick user guide for setting up the RTK system, a data sheet on hardware specs of the module, and a product summary on the board's features. A picture of module is displayed below.

<p align = "center">
  <img src = "https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Images/Screenshot%20from%202022-03-29%2016-59-35.png" />
</p>

The RTK modules were supplied by our client from a past project trying to implement the board into the same rover setup. The RTK modules are featured to have "centimeter level accuracy in clear sky environments" and testing by our team was done, included in the main README, to measure relative accuracy and confirm these results. 

The RTK modules come in a pair of 2 (One set as the Base Station module would be at a fixed position during use and the other as the Rover module would be attached to the rover). Information on how to use software to setup the modules are found in the (!!! include link to section in software README for setting up RTK modules!!!) 

## Rover Power Management

## Rover communication with Base-Station/User
### mRo SiK Telemetry Radio V2 915Mhz

we utilize a 915 Mhz telemetry radio for communicating the Rover with the Base Station. The radio can be found <a href = "https://store.mrobotics.io/mRo-SiK-Telemetry-Radio-V2-915Mhz-p/m10013-rk.htm">here</a> and a picture of the radio is included below.

<p align = "center">
  <img src = "https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Images/M10013-RK-3T.jpg" />
</p>

This radio was used as it is said to have easy implementation for the Pixhawk micro-controller as well as Mission Planner and seemed to have good reviews.

*PREFACE: The radio used for communication between mission planner and the Pixhawk operates at the same frequency as the communication between the two C94-M8P boards (915 MHz). Thus, operating both at the same time could cause inteference. By removing the antennas on the C94-M8P boards and connecting the base station board to Mission Planner, the RTK system can be setup using communication between Mission planner and the rover, without direct communication between the two C94-M8P boards. The C94-M8P application board also has a pin that can be used to turn of the internal radios. In our experiments, simply disconnecting the antenna proved sufficient.*

I have included a diagram below to show how the Base Station is setup. The telemetry radio is included in the Rover wiring diagram as well as the diagram below.

## Rover Wiring
A graphic showing the different components of the rover wired together is included below. The connections should be fairly intuitive, with wiring for each component already grouped together in the correct order to connect to the Pixhawk.

<p align = "center">
  <img src = "https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Images/circuit-design.png" />
</p>

We use the J8 interface on the C94-M8P to connect to the GPS port on the Pixhawk Microcontroller. Information on the J8 interface can be found in the user guide, <a href = https://content.u-blox.com/sites/default/files/C94-M8P-AppBoard_UserGuide_%28UBX-15031066%29.pdf> here </a>. We connect voltage and ground normally, and connect pin 9 of the J8 interface (RXD_GNSS) to the CAN2 RX pin of the Pixhawk, and pin 10 (TXD_GNSS) on the C94-M8P to the CAN2 TX pin of the Pixhawk. Information of the pinouts of the Pixhawk can be found <a href = https://ardupilot.org/copter/docs/common-pixhawk-overview.html> here </a>.

<p align = "center">
  <img src = "https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Images/c94-m8p-connection.jpg" />
</p>

