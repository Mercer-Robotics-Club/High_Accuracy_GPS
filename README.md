# High Accuracy GPS Implementation
A repository that hosts information for the High Accuracy GPS Implementation project.

## Project Info
This project is from William Del Barrio's and Peter Richardson's Senior Design Project at Mercer University. We were tasked with...
1. Developing a high-accuracy GPS system
2. Implementing it into a [common use case](README.md#use-case)
3. Documenting the process for open-source use on how to possibly implement it into your project

## Client
Our client is Dr. Anthony Choi from Mercer University.

## Use Case
We implemented the GPS system in an autonmous rover as pictured below. This rover system, ie. many of its hardware components, was adopted from a previous project under Dr. Choi.
<p align="center">
  <img src="https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Images/Senior%20Design%20High%20Accuracy%20GPS%20Update.jpg" />
</p>
<p>
  More information on how to set the hardware and electronics can be found in <a href="https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Hardware.md#Rover_Hardware">Hardware</a>.

## Supporting Hardware
For the rover, we utilized a variety of hardware and electronics together in it's current design.
<p>
  - <a href="https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Hardware.md#Rover_Chassis">Rover Chassis</a>
  <br>
  - <a href="https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Hardware.md#Rover_Motors">Rover Motors</a>
  <br>
  - <a href="https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Hardware.md#Rover_Motor_Controller">Rover Motor Controller</a>
  <br>
  - <a href="https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Hardware.md#Rover_Batteries">Rover Batteries</a>
  <br>
  - <a href="https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Hardware.md#Rover_Microcontroller">Rover Microcontroller</a>
  <br>
  - <a href="https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Hardware.md#Rover_Low_Accuracy_GPS_Module">Rover Low Accuracy GPS Module</a>
  <br>
  - <a href="https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Hardware.md#Rover_RTK_GPS_Modules">Rover RTK GPS Modules</a>
  <br>
  - <a href="https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Hardware.md#Rover_Power Management">Rover Power Management</a>
  <br>
  - <a href="https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Hardware.md#Rover_Communication_with_Base-Station/User">Rover Communication with Base-Station/User</a>
</p>

## Supporting Software

We use the Ardupilot Mission Planner application to configure the Pixhawk Microcontroller as well as plan and control missions. We use uBlox's u-center application to configure and test the C94-M8P RTK GPS system.

<p>
  - <a href="https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Software/Software.md#mission-planner">Mission Planner</a>
  <br>
  - <a href="https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Software/Software.md#ublox-u-center">uBlox U-Center</a>
</p>

## Results

### C94-M8P

The quality assurance test was to have the RTK-GPS system run by itself and to move the rover module to specific locations while taking measurements of its GPS location over time. We use a meter stick for reference. Using the U-Blox software, it was able to measure these GPS locations as ECEF X, Y, Z coordinates. We placed the base station module at one location and the rover module on the ground. We would then move the rover module specific distances and record its location multiple times with a few seconds apart for each measurement. The figure below includes the setup we used for this test as well as our results. Included after is Table 1 and Figure 10 detailing the results from this test.

| Actual Distance(m) | Measured Average (m) | Standard Deviation (m) |
| ------------------ | -------------------- | ---------------------- |
| 0 | 0.1160 | 0.0511 |
| 0.05 | 0.1027 | 0.0215 |
| 0.1 | 0.2225 | 0.0235 |
| 0.2 | 0.3451 | 0.0249 |
| 0.4 | 0.7532 | 0.0560 |
| 0.8 | 1.2021 | 0.0189 |
| 1.0 | 1.4254 | 0.0035 |
| 1.5 | 1.9892 | 0.0125 |
| 2.0 | 2.4576 | 0.0513 |

<p align="center">
  <img src="https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Images/rtk-gps-test.png" />
</p>
<p>

From our results from the test, one can see that the distances measured have an error of as much as 50 centimeters, much more than the marketed accuracy of the C94-M8P module. Despite this, the measurements at each position deviate very little, only as much as 5 centimeters. This implies that although moving the RTK-GPS can cause substantial error, the measurements are very stable when the module is stationary or going back to a specific position, even after moving the module, on repeated tests. The C94-M8P module has two defined “levels” of accuracy when using RTK GPS: a FLOAT mode, and a FIXED mode. The FLOAT mode is the level achieved by setting up the RTK GPS system successfully. However, the system cannot fully eliminate the carrier ambiguities it is designed to eliminate. Once it can eliminate these ambiguities, it will move into FIXED mode. We were never able to achieve FIXED mode; our tests were all conducted with the C94-M8P modules in the less-accurate FLOAT mode.

### Rover

Our second test, the performance test, included performing multiple missions for testing the low-accuracy GPS system and high-accuracy RTK-GPS system. The rover would do the missions and accuracy/deviation results were to be measured. We tested each system as follows. First, we developed a mission plan that consisted of 3-4 waypoints the rover must travel to. The waypoints were defined visually (ie. specific GPS coordinates were not determined for each waypoint) using the Mission Planner mapping utility. We chose to use the parking lot outside the Science and Engineering Building (SEB) for our testing field. After reaching each point, we would mark its position and measure its coordinates with reference to the waypoint. We conducted 3 tests for each system, with 3-4 waypoints for each test. Shown below are graphs showing the coordinates measured for each test.

To better understand our results, we calculated two measurements, which we called precision and accuracy. For each waypoint, we averaged the points and then calculated the distance from each point to this average; this is an assessment of the precision of the system (in other words, how effective the system is at going to the same location every time). Next, for each coordinate pair, we calculated the distance from it to the waypoint and averaged these together; this is an assessment of the accuracy of the system (in other words, how effective the system is at going to the exact location the user desires). 

For these tests, there is an inherent amount of inaccuracy introduced by the waypoints themselves. Because we can not possibly know the exact location of each waypoint, we define these waypoints visually by picking a point on a map provided by Mission Planner, which uses various mapping tools such as Google Maps. Thus, the error in accuracy we state here measures not just the error in the system, but the error in planning and choosing waypoints.

Regular GPS

| Waypoint | Precision (cm) | Accuracy (cm) |
| -------- | -------------- | ------------- |
| 1        | 49.32736504    | 63.36096951   |
| 2        | 19.20970203    | 63.2474278    |
| 3        | 16.13190012    | 66.87970434   |
| Average  | 28.22298906    | 64.49603388   |

Regular GPS with RTK inject
| Waypoint | Precision (cm) | Accuracy (cm) |
| -------- | -------------- | ------------- |
| 1        | 44.2587823     | 53.93808805   |
| 2        | 13.08477178    | 76.12145744   |
| 3        | 64.68303541    | 73.06779175   |
| Average  | 40.67552983    | 67.70911241   |

RTK GPS with just 1 Compass
| Waypoint | Precision (cm) | Accuracy (cm) |
| -------- | -------------- | ------------- |
| 1        | 93.12111256    | 77.55532349   |
| 2        | 161.8520985    | 125.1212556   |
| 3        | 94.66340198    | 94.66340198   |
| Average  | 116.5455377    | 99.11332701   |

RTK GPS with 2 compasses
| Waypoint | Precision (cm) | Accuracy (cm) |
| -------- | -------------- | ------------- |
| 1        | 127.7120678    | 109.8804867   |
| 2        | 135.5486878    | 109.9140873   |
| 3        | 216.3684996    | 216.3684996   |
| Average  | 154.7407746    | 138.9348904   |

  <p align="center">
  <img src="https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Images/rover-test.png" />
</p>
<p>

Our tests show that while the C94-M8P can achieve reasonably accurate measurements of position within 50 centimeters, once implemented into the Pixhawk rover, the RTK-GPS seems to have a significantly decreased accuracy, with an error of a meter or more on average.

Our main goal was two-fold: 1) Configure and operate the C94-M8P, with the purpose of integrating it into the Pixhawk rover system, and 2) Demonstrate that the RTK GPS implementation provided a higher accuracy solution to the navigation of the rover. While we were able to use the C94-M8P to measure position and integrate the C94-M8P into the Pixhawk rover system, we could not demonstrate that the C94-M8P had a higher accuracy than the regular GPS implementation. There are multiple possible reasons for this:
  - The limited accuracy of the survey-in process. The RTK system uses the base station’s GPS location to do real-time corrections to the rover’s GPS location. An inaccurate base station location will add inaccuracies throughout the testing results.
  - Communication of data could be limited between the base station and rover. With such a large amount of crucial data being communicated between the rover and base station, long latency (the amount of time it takes for data to be sent between the base station and rover) will cause RTK corrections to be sent at a slower rate. This will cause live GPS location to be calculated at a slower rate and reduce both accuracy and precision. Additionally, our form of communication, radio waves, may be interrupted by parts on the rover or the environment.
  - The C94-M8P does not have an integrated compass like the 3DRU GPS. An integrated compass could provide much better compass direction which, while testing, we identified as a crucial part of reaching higher accuracy and precision.
