<h2><strong>Arduino Control using ESP8266 Web Server</strong></h2>

This project provides a Web Server Framework supporting http requests to access Arduino resources.

Setup:

1. Copy the web_server folder to your Arduino sketch folder.
2. Copy the UtilityFunctions folder to your Arduino libraries folder.
3. Copy the webserver folder to your Arduino libraries folder.
4. Change the following in the web_server sketch to match your network settings:

const char* ssid = "YOURWIFISSID";
const char* password = "YOURWIFIPASSWORD";
const IPAddress ipadd(192,168,0,132);     
const IPAddress ipgat(192,168,0,1); 

define SVRPORT 9701

5. Server Setting

5.1 To use the standard Arduino Web Server library, which polls for connections, use this define in the sketch:

define SVR_TYPE SVR_HTTP_LIB

5.2 To use the EspressIf SDK Web Server API, which uses event callbacks, use this define in the sketch:

define SVR_TYPE SVR_HTTP_SDK

Operation:

The ESP8266 performs as a server, receiving URL commands and forwarding them to an Arduino via the serial
interface.

In order to test this, the ESP8266 Tx needs to be connected to an Arduino Rx.
Likewise, the ESP8266 Rx needs to be connected to an Arduino Tx.

The subject Arduino should have the sketch "ArduinoHomeAutomation.ino" installed and running.
This sketch uses the Arduino software serial interface using digital pins 10 and 11. It was
tested using an Arduino nano. Using an Arduino with more serial ports, such as a MEGA can be used
and utilize the built-in hardware serial port. This would require some adjustment to the sketch.

Web Server test:

With both the Arduino and ESP8266 connected and running,

Enter the following URL in a web browser (adjust IP & port to your settings):

http://192.168.0.132:9701/?arduino=GetDigital&chan=04

The returned value in the web browser should be:

Digital Channel 04 is LO

Now set the channel HI by entering the following URL:

http://192.168.0.132:9701/?arduino=SetDigital&chan=04&state=1

The returned value in the web browser should be:

Digital Channel 04 is HI

And if something is connected to the Arduino channel 4, such as an LED, it should illuminate with this command.

Expansion:

Simply add the input/output configuration in your Arduino sketch setup() function to enable
additional digital control.



