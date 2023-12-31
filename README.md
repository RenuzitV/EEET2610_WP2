# PID Tuning Program for Inverted Pendulum

# Dependencies

Requires `platformio` to be installed on VSCode.

This program is designed to provide an efficient way to learn about PID controls in propellers and drones.

# The Setup

The setup requires an MPU 6050 (or any IMU) with 1 to 2 propellers attached to a straight beam where it can rotate freely, as shown below:

## Two propeller setup:

`^-------•-------^`

## One propeller setup:

`^ -------•`

`^` shows the propeller position, and `•` shows the pivot position along with the attached IMU.

# Usage

## Motor

**WARNING: IF THIS IS YOUR FIRST TIME RUNNING THIS PROGRAM, DO NOT ATTEMPT TO RUN THIS PROGRAM WITH BLADES ON YOUR MOTOR. THIS MAY RESULT IN SERIOUS INJURIES. EXERCISE CAUTION BEFORE ATTEMPTING TO PUT THE BLADES ON**

Two motor output groups are on ports `A9` and `A10` and can be adjusted in the `/lib/motor.cpp` declarations. These motor groups are assumed to be brushless (BLDC) motors, rotate opposite from one another, and can rotate freely. The calibration steps can be found in the same file, and is ran upon called from the main program. Users can adjust this process to their liking. The default calibration steps is:

- Set the ESC for that motor to be the maximum signal
- Asks the user to turn off the ESC power source, then on for two seconds.
- Set the ESC for that motor to be the minimum signal

Be sure that your motor requires calibration, and is **NOT ARMED** before running this calibration process. Google `arming BLDC motors` to learn more about this behavior.

## Sensors

As stated before, the sensor used for this program is the MPU 6050, and more details can be read in the `/lib/mpu files`. Since IMUs uses I2C communication, please follow your board's configuration to match the communication protocol of the IMU. There should be two wires connected to your board for data lines and two more for power and ground wires for a total of four for a typical IMU.

The current orientation used for the MPU is the Y axis. Adjust your physical MPU orientation or the code as you see fit. Read more in the `/src/main.cpp` file.

## Controls

Controlling the program can be done via Matlab, and is the recommended way to tune PID. Start the matlab program to be greeted with a plethora of controls and measurements for your system, and shortcuts (case sensitive) can be found as so:

-   `s` starts and stops the PID signal to your motors. Consider this as the emergency switch, or the kill switch.
-   `t` calibrates the MPU's gyro and degree readings.
-   `e` calibrates the __positive__ motor group's calibration
-   `r` calibrates the __negative__ motor group's calibration
-   `g` and `v` adjusts the `P` value of PID
-   `h` and `b` adjusts the `I` value of PID
-   `j` and `n` adjusts the `D` value of PID
-   `d` and `x` adjusts the minimum starting signal of the motors. only affects when the motor is started.
-   `w` and `q` adjusts the setpoint of the PID. Usee this to set a non-zero angle to balance.
-   `i`, `o`, `p` puts the __positive__, __negative__ or __both__ motor groups to 50% capacity. Press `s` to stop the motors.
-   `f` and `c` adjusts the overlap range of the signal. This is a test setting.

The program also uses serial communication to communicate with the microcontroller. Adjust the serial port to match the current port of your board.

# Example

https://youtube.com/shorts/cK_sDuXjam4?feature=share
