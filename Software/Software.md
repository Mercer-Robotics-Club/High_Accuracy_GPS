# Software

This section will address the following:
- All the software being used for the project
- How to set up all software
- Version required for all software
- Bugs, issues, reminders when working with the software

## Mission Planner

### Version & Download (MP)

The software we used, Ardupilot Mission Planner (Version 1.3.76 build 1.3.8029.15962) can be found and downloaded <a href = https://firmware.ardupilot.org/Tools/MissionPlanner/archive/> here </a>. Just click the download button and complete setup.

*NOTE: The version of Mission Planner that we used is version !!!!!! but newer versions should still work in this setup. The location of certain items in Mission Planner may be moved, changed, or renamed. Please research the user documentation or online help in that case*

### Setup (MP)

To install firmware on the Pixhawk, a wired connection is required, with the MavLink disconnected. Connect the Pixhawk to the computer using USB. This should power the rover on. Do not connect using MavLink. Navigate to the SETUP tab on Mission Planner in the top left of the application window, select "Install Firmware", and follow the instructions using the Rover type. Once finished, the rover can be disconnected from the computer.


We connect Mission Planner to the Pixhawk Microcontroller using the mRo Radio 915 MHz Telemetry Kit. Simply connect the one of the two radios to the computer using USB, and connect the other to the Pixhawk (see <a href="https://github.com/Mercer-Robotics-Club/High_Accuracy_GPS/blob/main/Hardware/Hardware.md#Rover_Communication_with_Base-Station/User">Hardware</a>). With the rover powered on, you can select the appropriate COM port (use Windows Device Manager to identify COM number) on Mission Planner in the top right of the application window, and click CONNECT. Once connected, the DATA tab of Mission Planner (see top left of the application window) should update in real time with rover information.

Navigate to the SETUP tab of Mission Planner, and select "Mandatory Hardware" on the left of the application window. To use the rover, the Pixhawk Microcontroller usually requires a GPS to be connected, and the following hardware must be calibrated:

- Frame Type
- Accel Calibration
- Compass
- Servo Output
- ESC Calibration

Control of the rover can be operated by the user using Mission Planner on the computer. If a remote controller is used instead, then the other hardware may also need to be calibrated. We also did not need to calibrate the "Servo Output" and "ESC Calibration". With our motor setup, the Servo Output should only have two outputs: "ThrottleLeft" and "ThrottleRight". Note that the pin numbers correspond to the pin outputs on the Pixhawk Microcontroller that connect to the Sabertooth motor controller, which should configure the output by without any need for calibration.

To calibrate the accelerometer, there are two or more calibrations needed. One involves leaving the rover flat and level; the other requires orienting the each face of the rover down (ie. front, back, top, bottom, left, right). The compass calibration requires performing a similar method after selecting the compasses you wish to use.

See <a href="https://ardupilot.org/copter/docs/configuring-hardware.html">Mandatory Hardware Configuration</a> for more information about hardware configuration.

Note that other hardware can be configured using the "Optional Hardware" section in the left of the application window. In particular, the "RTK/GPS Inject" section, is required when using the C94-M8P. In this section, a base station module can be connected using the appropriate COM port, and a survey in can be conducted, saved, and used in later operations. Once the base station module is connected and a fixed position is selected, Mission Planner will automatically attempt to inject RTK GPS RTCM correction messages for the Pixhawk Microcontroller to use.

Once properly configured, with the rover powered on, the rover can be armed in the DATA tab on Mission Planner in the top left of the application window. On the left side of the application window, many tabs are available; in particular, "Actions" and "Messages" will most likely be used frequently by the user. In the "Actions" tab, select "Arm/Disarm" to attempt to arm the rover (if not already armed).

Once configured correctly, the rover can be controlled using either a romote controller or by uploading a mission plan using the PLAN tab on Mission Planner in the top left of the application window. !!!!

### Bugs, Issues, Reminders (MP)

Understand that specific bugs and issues may require broader research using online resources. Pixhawk Microcontroller parameters can be found in the "Standard Params", "Advanced Params", or "Full Parameter List" sections in the CONFIG tab on Mission Planner in the top left of the application window. The user can use these sections to properly address any issues, including those involving the serial ports, servo outputs, arming requirements, remote control requirements, or navigation of the rover. More information can be found in the Ardupilot documentation or online forum.

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
