# IoT Enabled Landmine Detection Robotic Vehicle
**Note:**   1. This is a prototype model. \
            2. The code is written in C++, The entire design is developed in fusion 360 CAD tool.              
## Problem Overview
Developing an IoT-enabled robotic vehicle for efficient landmine detection and neutralization in hazardous environments, aiming to mitigate the risks and casualties associated with traditional detection methods. Challenges include achieving high detection accuracy while minimizing false positives, ensuring robust mobility over rugged terrains, implementing remote operation and real-time data processing through IoT connectivity, guaranteeing safety for operators and civilians, establishing reliable communication links, and optimizing cost-effectiveness for large-scale deployment. The solution must also adapt to various environmental conditions and incorporate fail-safe mechanisms to prevent accidental detonations or malfunctions.

## Existing system
In the existing manual demining process, human deminers often face significant risks while operating in mine-affected areas. These risks include the potential for injury or death from accidental detonations of landmines, as well as exposure to hazardous environmental conditions and psychological stress. EMF coil-based landmine detection systems offer a partial solution by providing a non-contact method for detecting landmines, thereby reducing direct physical contact with potentially explosive devices. However, despite this advantage, manual deminers using EMF coil-based systems still face risks associated with working in hazardous environments, such as uneven terrain, extreme weather conditions, and the presence of other explosive remnants of war. Furthermore, the effectiveness of EMF coil-based systems in detecting landmines can vary depending on factors such as soil composition, moisture levels, and the presence of metallic clutter, which may require deminers to spend extended periods in the field conducting thorough surveys. Overall, while EMF coil-based systems contribute to mitigating some of the risks associated with manual demining operations, they do not eliminate the need for human intervention entirely. Therefore, there remains a critical need for the development of advanced robotic solutions that can autonomously detect and neutralize landmines, reducing the reliance on manual deminers and minimizing human risk in mine-affected areas.

## Proposed system
The proposed system, IoT-enabled robotic vehicle designed for efficient and safe landmine detection and neutralization in hazardous environments. Key components and features of the proposed system include: \
**1. Robotic Vehicle:** A rugged and agile robotic vehicle equipped with sensors, actuators, and navigation systems capable of traversing challenging terrains commonly found in mine-affected areas. \
**2. Sensor Suite:** Integration of a diverse array of sensors, including proximity sensor, metal detectors, ground-penetrating radar, and possibly other technologies like thermal imaging or chemical sniffers, to accurately detect various types of landmines while minimizing false positives. \
**3. IoT Connectivity:** Incorporation of IoT devices for remote control, monitoring, and data transmission, enabling operators to oversee and manage the robotic vehicle's operations from a safe distance. \
**4. Real-time Data Processing:** Onboard processing capabilities algorithms to analyze sensor data in real-time, enhancing detection accuracy, and enabling prompt decision-making. \
**5. Communication and Localization:** Reliable communication links established between the robotic vehicle and the control center, along with accurate localization techniques for real-time tracking and navigation. \
**6. Long-range Communication:** Utilization of robust communication protocols and technologies, such as radio frequency (RF) or cellular connectivity, to ensure reliable data transmission over extended distances. \
**7. User-friendly Interface:** Ergonomic design with intuitive controls and a user-friendly interface, enabling operators to easily navigate and manipulate the robotic vehicle's movements and functions. 

## Scope
* Accurate and efficient detection of landmines in hazardous environments.
* Remote control and monitoring of the robotic vehicle's operations from a safe distance.
* Real-time decision-making through onboard processing and analysis of sensor data.
* Consideration for scalability to enable deployment in diverse operational scenarios.
* Optimization of costs to ensure affordability and sustainability.
* In addition to landmine detection and neutralization, the proposed system can be seamlessly integrated into rescue operations, enhancing its versatility and utility.

# Transmitter Code 
## Explanation
The transmitter circuit consists of Arduino Nano micro-controller, 2 ps2 joy sticks for control of the robot, 2 potentio meters for controlling the LED's and NRF2L01 module for transmitting the signal to receiver.
**In the setup() function:** \
Initializes serial communication at a baud rate of 4800 bits per second. \
Adds a delay of 100 milliseconds to allow the serial communication to stabilize. \
**In the loop() function:** \
Reads analog values from six different analog pins (A0 to A5) and stores them in variables (p1val, p2val, x1val, y1val, x2val, y2val). \
Checks the value of each sensor against certain thresholds (100 and 900) using conditional statements (if statements). \
Prints characters over serial communication (Serial.print()) based on the readings of each sensor. The characters printed correspond to the state of each sensor or input device. For example: \
'1' or '2' corresponds to the state of the sensor connected to pin A0 (p1val). \
'3' or '4' corresponds to the state of the sensor connected to pin A1 (p2val). \
'5' or '6' corresponds to the state of the sensor connected to pin A2 (x1val). \
'7' or '8' corresponds to the state of the sensor connected to pin A3 (y1val). \
'9' or '0' corresponds to the state of the sensor connected to pin A4 (x2val). \
'A' or 'B' corresponds to the state of the sensor connected to pin A5 (y2val). \
After printing the sensor states, there's a delay of 300 milliseconds (delay(300);) before the loop repeats. \

# Receiver Code \
## Explanation \
The receiver circuit consists of Arduino Uno, L298 motor driver, 4 12V DC gear motors, servo pan, tilt mount for controlling the camera module and NRF2L01 module for receiving data from transmitter. \
**In the setup() Function:** \
**Purpose:** This function is called once when the program starts. Its purpose is to set up the initial state of the hardware and peripherals. \
**Actions:** \
* Sets pin modes for motor control and servo motors as OUTPUT. \
* Initializes Serial communication at a baud rate of 4800. \
* Sets initial states for motor driver pins (in1, in2, in3, in4) to LOW. \
* Attaches and initializes servo motors (pan and tilt) to pins 3 and 4 respectively, and sets their initial positions to 90 degrees. \
**loop() Function:** \
**Purpose:** This function is called repeatedly after setup(). It's where the main program logic resides. \
**Actions:** \
* Checks if there's data available in the serial buffer. If data is available, it reads a single byte from the buffer into variable x. \
* The rest of the code inside this function handles different actions based on the value of x. \
**Serial Communication Commands:** \
**Purpose:** These commands control certain pins based on the received characters over serial communication. \
**Actions:** \
* If x is '1', it sets pin hb to HIGH. \
* If x is '2', it sets pin hb to LOW. \
* If x is '3', it sets pin lb to HIGH. \
* If x is '4', it sets pin lb to LOW. \
**Servo Motor Angle Adjustment:** \
**Purpose:** These commands adjust the angles of the servo motors (pan and tilt) based on the received characters. \
**Actions:** \
* If x is 'A', it increases ang1 by 5 (up to a maximum of 175). \
* If x is 'B', it decreases ang1 by 5 (down to a minimum of 5). \
* If x is '5', it increases ang2 by 5 (up to a maximum of 175). \
* If x is '6', it decreases ang2 by 5 (down to a minimum of 5). \
**Motor Control Commands:** \
**Purpose:** These commands control the direction of the robot's movement based on the received characters. \
**Actions:** \
* If x is '0', it moves the robot forward. \
* If x is '7', it turns the robot right. \
* If x is '8', it stops the robot. \
* If x is '9', it moves the robot backward. \
* If x is any other value, it stops the robot as a default case. \
# Landmine Detection Code \
## Explanation \
This circuit consists of ESP8266 wi-fi module, GPS, GSM, Proximity sensor for detection. \
**Note:** In this we are using metals(tretes as landmine) to show the detection process. \
**Libraries:** \
Several libraries related to WiFi communication, ThingSpeak integration, GPS parsing, and SoftwareSerial communication are included. \
**Global Variables:** \
Various global variables are declared, including pins for LED, buzzer, and the analog sensor, as well as variables for WiFi credentials, ThingSpeak fields, and GPS data. \
**read_gps() Function:** \
This function reads GPS data from the serial port and parses it using the TinyGPS library to obtain latitude and longitude coordinates. \
**setup() Function:** \
Initializes serial communication, pins for LED and buzzer, and starts the WiFi in station mode and begins communication with ThingSpeak. \
**loop() Function:** \
* Continuously checks the WiFi connection status. If not connected, it attempts to connect using the provided SSID and password. It blinks the LED while attempting to connect. \
* Reads the value from an analog sensor connected to pin A0, which presumably detects metal. It then prints this value over serial. \
* If the metal value exceeds a threshold (500 in this case), it turns on the buzzer. \
* Sets the fields on ThingSpeak with the metal value, latitude, and longitude. \
* Sends an SMS alert with the message "Medical detected" and the current GPS coordinates if kk is 0 (indicating it hasn't sent an SMS yet). \
* send_sms() function is responsible for sending an SMS. It sets up the modem and sends an AT command with the message content and recipient number. It includes the GPS coordinates in the message.

