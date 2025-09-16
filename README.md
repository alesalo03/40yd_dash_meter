# 40yd_dash_meter
A repository that describes how to build a simple 40yd dash meter using two esp32 boards that communicates through ESP NOW.

WHAT YOU NEED:

Components:
- 2xESP32 boards (it is important these can use the ESP NOW protocol)
- 1xlcd1602 module (I used this but also a 7 segment led module with at least 4 numbers should work)
- 1xgreen led
- 1xred led
- 1x10kΩ trimmer
- 1x10kΩ resistor
- 2x330Ω resistor
- 1xHC-SR501 PIR Motion Sensor

To solder:
- 1xsoldering station
- soldering iron
- 2xPCB boards
- a lot of PCB jumper cables

Other:
- 2xboxes to contain the two PCB boards
- materials to build the pressure plate (I used wood but even plastic should work)

Description of the project:
1. the first board is positioned at the start line, it is connected to the two leds and the pressure plate. The two leds are used to signal when it's possible to start and when the station is unable to measure. When the green light is on the athlete can put pressure on the board, when the hand is lifted form the plate teh first board sends a START message using the ESP NOW protocol.
2. the second board is connected to the motion sensor and the lcd display. The sensor has time limits:
   - it needs 1 minute to setup
   - it needs 3 seconds between measurements
The second board when it's plugged in sends a message to the first one and starts a 60 seconds timer, this message is used to synchronize the two boards, this way the first board knows when to light the green light. After the 60 seconds the sensor is ready, the first board sends the START message and the second one start the clock, when the sensor detects motion the clock is stopped and the time is shown on the lcd display. After 3 second the sensor is ready for a new measurement.

The wiring diagram is the following:

The code for the two boards can be found in this repository.

To build the pression plate I used two square wood pieces, at the center of both I put some soldering iron and connected these with two cables to the first board. Between the two wood pieces I put some sponge pieces, this way when there is no pression the two soldering iron don't touch and the circuit is open. Here is a grafic explanation:

  
  

