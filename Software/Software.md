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

User guide for u-center can be found <a href = https://www.u-blox.com/sites/default/files/u-center_Userguide_UBX-13005250.pdf> here </a>

*NOTE: The version of u-center that we used is version 22.02 but newer version should still work in this setup. The location of certain items in u-center may be moved, changed, or renamed. Please research the user documentation or online help in that case*

### Setup (UBX)

Note that much of the following information was taken directly from the [C94-M8P Application Board Setup Guide](C94-M8P-Appboard-Setup_QuickStart_(UBX-16009722).pdf).

An RTK GPS system requires two modules, one to act as a base station at a known fixed position, while the other is located on the rover and uses measurements from the base station to correct its own measurements. Both C94-M8P modules need to be set up independently in u-center.

For each board, attach the radio antenna to the UHF port, and attach the GNSS antenna to the GNSS port (see figure below).

#### Connecting to the C94 M8P board
After connecting the C94-M8P application board to the Windows computer with u-center installed using a Micro-USB cable, communication can be established by connecting to the appropriate serial port in the u-center application (Found in the Ports section of Device Manager on Windows) and setting the baud rate (usually, this should be 9,600). See the figure below to set the appropriate COM port and buad rate. Afterwards, any status windows open on the application should automatically update with information from the board.

#### Setting up the base station module
Once connection has been established, configuration and receiving status is done by sending and receiving messages using the Messages View (see figure below).

The base station must be set to TIME mode. To do this, navigate to the UBX-CFG-TMODE3 message (see figure below). From here, two modes are available:
- If a fixed position with known coordinates is already available, set the appropriate coordinates in the Fixed Position section.
- Otherwise, a Survey-In can be conducted. Place the rover module antenna in the desired position and ensure it does not move for the duration of the survey, then specify the minimum observation time (in seconds) and required accuracy (in meters).

Once appropriate message fields are specified, click Send to send the message to the rover (see figure below).

The Survey-In can be monitored by polling the UBX-NAV-SVIN message. Note that messages may not update automatically, and may need to be manually polled in order to receive information in real time. 

Once the survey is completed, the correct communication protocols should be configured using the UBX-CFG-PRT message (see figure below). For the base station, ensure only RTCM messages are sent to the rover using UART1, and specify the baud rate (usually, this should be 19200). Click Send.

Finally, enable the following RTCM signals on UART1 using the UBX-CFG-MSG message (see figure below):
- F5-05 RTCM3.2 1005 enabled on UART1 (set to 1)
- F5-4D RTCM3.2 1077 enabled on UART1 (set to 1)
- F5-57 RTCM3.2 1087 enabled on UART1 (set to 1)
- F5-E6 RTCM3.2 1230 enabled on UART1 (set to 10)
For each message, click Send.

Once the base station module is successfully configured, the Fix Mode should automatically update to TIME mode (see figure below).

#### Setting up the rover module

After connecting the u-center application to the rover module, only the UBX-CFG-PRT message needs to be sent (see figure below). Ensure that only RTCM messages from the base station are being received using UART1, and specify the same baud rate used by the base station. Click Send.

Once the rover module is successfully configured, the Fix Mode should automatically update from 3D/GNSS to 3D/GNSS/FLOAT (see figure below). After some time, the rover may be able to resolve carrier ambiguities and move to 3D/GNSS/FIXED mode with higher accuracy. Previous tests were unable to achieve FIXED mode on the rover.

### Notes (UBX)

Many messages can be polled to view status information. These include:
- Survey In: UBX-NAV-SVIN
- Satellite Information: UBX-NAV-SVINFO
- Position: UBX-NAV-POSECEF and UBX-NAV-POSLLH
