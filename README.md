==========================
SandCrab CNC Mill Firmware
==========================

Overview
========

Forked from Marlin 3D Printer Firmware, with additional content from GRBL CNC Firmware, SandCrab is CNC Mill Firmware specifically for the Arduino Mega 2560 and Ramps 1.4.

Features:
=========

*   Interrupt based movement with real linear acceleration
*   High steprate
*   Look ahead (Keep the speed high when possible. High cornering speed)
*   Interrupt based temperature protection
*   preliminary support for Matthew Roberts advance algorithm
    For more info see: http://reprap.org/pipermail/reprap-dev/2011-May/003323.html
*   Full endstop support
*   SD Card support
*   SD Card folders (works in pronterface)
*   SD Card autostart support
*   LCD support (ideally 20x4)
*   LCD menu system for autonomous SD card printing, controlled by an click-encoder.
*   EEPROM storage of e.g. max-velocity, max-acceleration, and similar variables
*   Arc support
*   Endstop trigger reporting to the host software.
*   Updated sdcardlib
*   Configurable serial port to support connection of wireless adaptors.
*   RC Servo Support, specify angle or duration for continuous rotation servos.

The default baudrate is 250000. This baudrate has less jitter and hence errors than the usual 115200 baud, but is less supported by drivers and host-environments.

Implemented G Codes:
====================

*  G0  -> G1
*  G1  - Coordinated Movement X Y Z E
*  G2  - CW ARC
*  G3  - CCW ARC
*  G4  - Dwell S<seconds> or P<milliseconds>
*  G28 - Home all Axis
*  G90 - Use Absolute Coordinates
*  G91 - Use Relative Coordinates
*  G92 - Set current position to cordinates given

M Codes
*  M0   - Unconditional stop - Wait for user to press a button on the LCD (Only if ULTRA_LCD is enabled)
*  M1   - Same as M0
*  M17  - Enable/Power all stepper motors
*  M18  - Disable all stepper motors; same as M84
*  M20  - List SD card
*  M21  - Init SD card
*  M22  - Release SD card
*  M23  - Select SD file (M23 filename.g)
*  M24  - Start/resume SD program
*  M25  - Pause SD program
*  M26  - Set SD position in bytes (M26 S12345)
*  M27  - Report SD program status
*  M28  - Start SD write (M28 filename.g)
*  M29  - Stop SD write
*  M30  - Delete file from SD (M30 filename.g)
*  M31  - Output time since last M109 or SD card start to serial
*  M32  - Select file and start SD print (Can be used when printing from SD card)
*  M42  - Change pin status via gcode Use M42 Px Sy to set pin x to value y, when omitting Px the onboard led will be used.
*  M80  - Turn on Power Supply
*  M81  - Turn off Power Supply
*  M82  - Set E codes absolute (default)
*  M83  - Set E codes relative while in Absolute Coordinates (G90) mode
*  M84  - Disable steppers until next move, or use S<seconds> to specify an inactivity timeout, after which the steppers will be disabled.  S0 to disable the timeout.
*  M85  - Set inactivity shutdown timer with parameter S<seconds>. To disable set zero (default)
*  M92  - Set axis_steps_per_unit - same syntax as G92
*  M112 - Emergency stop
*  M114 - Output current position to serial port
*  M115 - Capabilities string
*  M117 - display message
*  M119 - Output Endstop status to serial port
*  M126 - Solenoid Air Valve Open (BariCUDA support by jmil)
*  M127 - Solenoid Air Valve Closed (BariCUDA vent to atmospheric pressure by jmil)
*  M128 - EtoP Open (BariCUDA EtoP = electricity to air pressure transducer by jmil)
*  M129 - EtoP Closed (BariCUDA EtoP = electricity to air pressure transducer by jmil)
*  M201 - Set max acceleration in units/s^2 for print moves (M201 X1000 Y1000)
*  M202 - Set max acceleration in units/s^2 for travel moves (M202 X1000 Y1000) Unused in Marlin!!
*  M203 - Set maximum feedrate that your machine can sustain (M203 X200 Y200 Z300 E10000) in mm/sec
*  M204 - Set default acceleration: S normal moves T filament only moves (M204 S3000 T7000) im mm/sec^2  also sets minimum segment time in ms (B20000) to prevent buffer underruns and M20 minimum feedrate
*  M205 -  advanced settings:  minimum travel speed S=while printing T=travel only,  B=minimum segment time X= maximum xy jerk, Z=maximum Z jerk, E=maximum E jerk
*  M206 - set additional homeing offset
*  M207 - set retract length S[positive mm] F[feedrate mm/min] Z[additional zlift/hop], stays in mm regardless of M200 setting
*  M208 - set recover=unretract length S[positive mm surplus to the M207 S*] F[feedrate mm/min]
*  M209 - S<1=true/0=false> enable automatic retract detect if the slicer did not support G10/11: every normal extrude-only move will be classified as retract depending on the direction.
*  M218 - set hotend offset (in mm): T<extruder_number> X<offset_on_X> Y<offset_on_Y>
*  M220 S<factor in percent>- set speed factor override percentage
*  M221 S<factor in percent>- set extrude factor override percentage
*  M240 - Trigger a camera to take a photograph
*  M280 - Position an RC Servo P<index> S<angle/microseconds>, ommit S to report back current angle
*  M300 - Play beepsound S<frequency Hz> P<duration ms>
*  M301 - Set PID parameters P I and D
*  M302 - Allow cold extrudes
*  M303 - PID relay autotune S<temperature> sets the target temperature. (default target temperature = 150C)
*  M304 - Set bed PID parameters P I and D
*  M400 - Finish all moves
*  M401 - Lower z-probe if present
*  M402 - Raise z-probe if present
*  M500 - stores paramters in EEPROM
*  M501 - reads parameters from EEPROM (if you need reset them after you changed them temporarily).
*  M502 - reverts to the default "factory settings".  You still need to store them in EEPROM afterwards if you want to.
*  M503 - print the current settings (from memory not from eeprom)
*  M540 - Use S[0|1] to enable or disable the stop SD card print on endstop hit (requires ABORT_ON_ENDSTOP_HIT_FEATURE_ENABLED)
*  M600 - Pause for filament change X[pos] Y[pos] Z[relative lift] E[initial retract] L[later retract distance for removal]
*  M907 - Set digital trimpot motor current using axis codes.
*  M908 - Control digital trimpot directly.
*  M350 - Set microstepping mode.
*  M351 - Toggle MS1 MS2 pins directly.
*  M928 - Start SD logging (M928 filename.g) - ended by M29
*  M999 - Restart after being stopped by error


Configuring and compilation:
============================

Install the arduino software IDE/toolset v23 (Some configurations also work with 1.x.x)
   http://www.arduino.cc/en/Main/Software

Download the Marlin firmware
   https://github.com/ErikZalm/Marlin/tree/Marlin_v1
   Use the "Download Zip" button on the right.

For gen6/gen7 and sanguinololu the Sanguino directory in the Marlin dir needs to be copied to the arduino environment.
  copy ArduinoAddons\Arduino_x.x.x\sanguino <arduino home>\hardware\Sanguino

Start the arduino IDE.
Select Tools -> Board -> Arduino Mega 2560    or your microcontroller
Select the correct serial port in Tools ->Serial Port
Open Marlin.pde

Click the Verify/Compile button

Click the Upload button
If all goes well the firmware is uploading

That's ok.  Enjoy Silky Smooth Printing.

===============================================
Instructions for configuring Bed Auto Leveling
===============================================
Uncomment the "ENABLE_AUTO_BED_LEVELING" define (commented by default)

You will probably need a swivel Z-MIN endstop in the extruder. A rc servo do a great job.
Check the system working here: http://www.youtube.com/watch?v=3IKMeOYz-1Q (Enable English subtitles)
Teasing ;-) video: http://www.youtube.com/watch?v=x8eqSQNAyro

In order to get the servo working, you need to enable:

* \#define NUM_SERVOS 1 // Servo index starts with 0 for M280 command

* \#define SERVO_ENDSTOPS {-1, -1, 0} // Servo index for X, Y, Z. Disable with -1

* \#define SERVO_ENDSTOP_ANGLES {0,0, 0,0, 165,60} // X,Y,Z Axis Extend and Retract angles


The first define tells firmware how many servos you have.
The second tells what axis this servo will be attached to. In the example above, we have a servo in Z axis.
The third one tells the angle in 2 situations: Probing (165º) and resting (60º). Check this with command M280 P0 S{angle} (example: M280 P0 S60 moves the servo to 60º)

For RAMPS users:
----------------

By default, RAMPS have no power on servo bus (if you happen to have a multimeter, check the voltage on servo power pins).
In order to get the servo working, you need to supply 5V to 5V pin.. You can do it using your power supply (if it has a 5V output) or jumping the "Vcc" from Arduino to the 5V RAMPS rail.
These 2 pins are located just between the Reset Button and the yellow fuses... There are marks in the board showing 5V and VCC.. just connect them..
If jumping the arduino Vcc do RAMPS 5V rail, take care to not use a power hungry servo, otherwise you will cause a blackout in the arduino board ;-)


Next you need to define the Z endstop (probe) offset from hotend.
My preferred method:

* a) Make a small mark in the bed with a marker/felt-tip pen.
* b) Place the hotend tip as *exactly* as possible on the mark, touching the bed. Raise the hotend 0.1mm (a regular paper thickness) and zero all axis (G92 X0 Y0 Z0);
* d) Raise the hotend 10mm (or more) for probe clearance, lower the Z probe (Z-Endstop) with M401 and place it just on that mark by moving X, Y and Z;
* e) Lower the Z in 0.1mm steps, with the probe always touching the mark (it may be necessary to adjust X and Y as well) until you hear the "click" meaning the mechanical endstop was trigged. You can confirm with M119;
* f) Now you have the probe in the same place as your hotend tip was before. Perform a M114 and write down the values, for example: X:24.3 Y:-31.4 Z:5.1;
* g) You can raise the z probe with M402 command;
* h) Fill the defines bellow multiplying the values by "-1" (just change the signal)


* \#define X_PROBE_OFFSET_FROM_EXTRUDER -24.3
* \#define Y_PROBE_OFFSET_FROM_EXTRUDER 31.4
* \#define Z_PROBE_OFFSET_FROM_EXTRUDER -5.1


The following options define the probing positions. These are good starting values.
I recommend to keep a better clearance from borders in the first run and then make the probes as close as possible to borders:

* \#define LEFT_PROBE_BED_POSITION 30
* \#define RIGHT_PROBE_BED_POSITION 140
* \#define BACK_PROBE_BED_POSITION 140
* \#define FRONT_PROBE_BED_POSITION 30

A few more options:

* \#define XY_TRAVEL_SPEED 6000

X and Y axis travel speed between probes, in mm/min.
Bear in mind that really fast moves may render step skipping. 6000 mm/min (100mm/s) is a good value.

* \#define Z_RAISE_BEFORE_PROBING 10
* \#define Z_RAISE_BETWEEN_PROBINGS 10

The Z axis is lifted when traveling to the first probe point by Z_RAISE_BEFORE_PROBING value
and then lifted when traveling from first to second and second to third point by Z_RAISE_BETWEEN_PROBINGS.
All values are in mm as usual. 

That's it.. enjoy never having to calibrate your Z endstop neither leveling your bed by hand anymore ;-)




