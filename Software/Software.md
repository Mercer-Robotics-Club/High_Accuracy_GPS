# Software
This file is to layout...
- All the software being used for the project
- How to set up all software
- Version required for all software
- Bugs, issues, reminders when working with the software

## Mission Planner

### Version & Download (MP)

The software we used, Ardupilot Mission Planner (Version !!!!!!) can be found and downloaded <a href = https://firmware.ardupilot.org/Tools/MissionPlanner/archive/> here </a>. Just click the download button and complete setup.

User guide for u-center can be downloaded <a href = https://ardupilot.org/planner/> here </a>

*NOTE: The version of Mission Planner that we used is version !!!!!! but newer version should still work in this setup. The location of certain items in Mission Planner may be moved, changed, or renamed. Please research the user documentation or online help in that case*

### Setup (MP)

### Bugs, Issues, Reminders (MP)

## UBlox U-Center

### Version & Download (UBX)

The software we used, U-Blox u-center (Version V22.02) can be found and downloaded <a href = https://www.u-blox.com/en/product/u-center> here </a>. Just click the download button and complete setup. 

User guide for Mission Planner can be found <a href = https://www.u-blox.com/sites/default/files/u-center_Userguide_UBX-13005250.pdf> here </a>

*NOTE: The version of u-center that we used is version 22.02 but newer version should still work in this setup. The location of certain items in u-center may be moved, changed, or renamed. Please research the user documentation or online help in that case*

### Setup (UBX)

Note that much of the following information was taken directly from the [C94-M8P Application Board Setup Guide](C94-M8P-Appboard-Setup_QuickStart_(UBX-16009722).pdf).

An RTK GPS system requires two modules, one to act as a base station at a known fixed position, while the other is located on the rover and uses measurements from the base station to correct its own measurements. Both C94-M8P modules need to be set up independently in u-center.

#### Connecting to the C94 M8P board
After connecting the C94-M8P application board to the Windows computer with u-center installed using a Micro-USB cable, communication can be established by connecting to the appropriate serial port in the u-center application (Found in the Ports section of Device Manager on Windows) and setting the baud rate (usually, this should be 9,600). See the figure below to set the appropriate COM port and buad rate. Afterwards, any status windows open on the application should automatically update with information from the board.

#### Setting up the base station module
Once connection has been established, configuration and receiving status is done by sending and receiving messages using the Messages View (see figure below).

The base station must be set to TIME mode. To do this, navigate to the UBX-CFG-TMODE3 message (see figure below). From here, two modes are available:
- If a fixed position with known coordinates is already available, set the appropriate coordinates in the Fixed Position section.
- Otherwise, a Survey-In can be conducted. Place the rover module antenna in the desired position and ensure it does not move for the duration of the survey, then specify the minimum observation time (in seconds) and required accuracy (in meters).

Once appropriate message fields are specified, send the message to the rover (see figure below).

#### Setting up the rover module

### Bugs, Issues, Reminders (UBX)

