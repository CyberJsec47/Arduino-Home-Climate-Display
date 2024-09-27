## Arduino Home climate display

---

### The goal of this project is to create an indoor and outdoor climate monitor.
#### The monitor will be build using Arduino and various sensors to display the following:

- **Temperature**
- **Humidity** 
- **Pressure** 
- **Wind Speed**
- **Direction**
- **Rainfall**


#### This readings will be sent real time via a wireless protocol to a Raspberry Pi which will then give a live display of the readings in a GUI interface. 

---

### Progress

The project currently consists of an Arduino UNO and a DHT11 sensor and can display the temperature in C (or F) and the humidity in %.<br>
It displays the readings on a 16x2 LCD screen in the format:<br><br>Temp: 20.0 C<br>Humidity 60.00%<br>


It also uses a HC-SR04 ultrasonic turn the LCD on and off depending on if somebody is present to see it. This is to safe on battery life.


--- 

### Current Equipment 

- **Arduino UNO**
- **HC-SR04 Ultrasonic Sensor**
- **DHT11 Temperature and Humidity Sensor**
- **I2C 16x2 Arduino LCD** 
---

### Communication

The data from the outdoor weather station will need to be sent to the Pi inside over a short distance.<br> I am looking at two weather stations from [DFRobot](https://thepihut.com/products/weather-station-kit-with-anemometer-wind-vane-rain-bucket) and a second from [SparkFun](https://thepihut.com/products/sparkfun-arduino-iot-weather-station). The SparkFun comes with a ESP32 board for wireless communication. The DF Robot station comes with a serial board which can connect to a module of my choice for comms.<br>I have an Arduino nano esp32 so either kit I will be able to use WiFi or Bluetooth for wireless Comms


My initial idea for data communication is to use the MQTT protocol. The choice for this is based on my own knowledge and interests. I don't have much of an interest in web development so using  HTTP or TCP to communicate data could involve having to work with development tools such as Node.js

using MQTT will be a more straightforward tool that suits IoT more. For this I'll need an MQTT broker, such as Mosquitto. 

---

### Displaying the data


The data will be sent from the outside weather station inside to my [Raspberry Pi 5](https://www.raspberrypi.com/products/raspberry-pi-5/) to take in the data and display in a suitable way.<br> To recieve the data from the station via Wi-Fi I am planning to set the RaspPi up as its own private access point and connect the ESP32 to it. 

Once the pi has the data I am thinking of creating either a Python program to proccess and display using a GUI such as [Flet](https://flet.dev/) and use [MatLab](https://uk.mathworks.com/products/matlab.html) to graph out the data to display in charts for live and trends of climate.<br> or a second option using the same methods but as a web page running on the Pi. Both have positive and negatives to look into. These are future goals once the station is built and working.


--- 


### Current Wiring diagram 

![Schematic](https://github.com/CyberJsec47/Arduino-Home-Climate-Display/blob/main/Schematic.png)


--- 
### Future goals

- **Set up outside weather station**<br>This will involve purchasing either one of the stations, finding a suitable place in my garden to set up and then connecting the wiring and testing the data locally
- **Create RasPi access point**<br> Set up the Raspberry Pi as a private access point for the ESP32 to connect to.
- **Establish wireless communication**<br> When the previous two goals are met I can start to send the data to the Pi before working on implementing a GUI to display data.
- **RasPi GUI**<br>Either using Flet, Figma or another Python GUI module create a way to display the data live on a small home display.
---
### Future extended goals

- **individual room temperature control**<br> Once the initial setup is complete and working I want to create individual temperature modules that can be placed in each room of my house.<br> Each room has an electric radiator which I will connect a smart plug too which can be controlled via the Pi or an external app such as home assistance.<br> Monitoring each room I can choose to turn a radiator on and off by the plug allowing me to set the temperature of specific rooms, for example once I finish work I can turn on the living room radiator and once I am home the room is warm.<br> I can also create a script that automates this process to turn on and off at certain temperatures. This is because my radiators are old and lack a timer or any controls for this.
