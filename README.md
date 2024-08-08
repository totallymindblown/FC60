# **FC60**
A simple Feeder Controller for electric SMT-Feeders.
![FC60 Feeder Controller](/hardware/fc60.png)
## Specifications
* reliable Atmel SAMC21N18A MCU
* single 24V Power Supply
* max. 60 Feeders can be controlled with one Board
* CAN-FD Interface (compatible with MB6HC, MB6XD, etc.)
* optional RS485 Interface
## Hardware
The board has been designed with [Kicad 8.0.4](https://www.kicad.org).  
All schematics, design-files, gerbers and bom can be found in [hardware](/hardware/).
## Software
A Bootloader and Firmware for use with e.g. RFF 3.5 can be found in [Releases](http://github.com/totallymindblown/FC60/releases/latest).  

First the bootloader needs to be programmed with a suitable programmer (e.g. ATMEL-ICE, SEGGER J-Link, etc.) using the SWD-Interface J61 (10-pin 50mil connector), then the firmware can be uploaded from the mainboard. Since the MCU runs with 5V, the programmer must support this target voltage.
## How to Use
The feeders are each connected using connector J1..J60 and supplied with 24V. The trigger signal is provided by a short pulse (1 ms) to the control input of the feeder.
An appropriately dimensioned 24V switching power supply is connected to J64.

To be able to trigger the feeders, a single GPIO pin must be created for the FC60 using the following gcode example. The port number and CAN address are selected according to the application.

*_create Port 12 on FC60 with CAN address 24 :_* <b>`M950 P12 C"24.feeder"`</b>

The feeder is selected using <b>M42</b> with the <b>S</b> parameter, but it has here nothing to do with PWM. It is just a simple way on the FC60 to circumvent the RFF GPIO limit.  

*_trigger feeder number 1 :_* <b>`M42 P12 S1`</b>  

*_trigger feeder number 60 :_* <b>`M42 P12 S60`</b>  

The default CAN address of the FC60 is 124 which can be reset using JP2 (__CAN-RES__).  
CAN bus termination can be set with jumper JP1 (__TERM.__).
