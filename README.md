# Car Metrics Monitoring System with IoT Integration

This project uses an **ESP32** microcontroller to monitor various vehicle-related metrics, including **humidity**, **distance** (from obstacles), and **obstacle detection**. The system is designed for real-time feedback, offering both visual and audible alerts for the driver. Additionally, data is sent to **ThingSpeak** for remote monitoring and logging of vehicle conditions.

## Features:
- **Humidity Monitoring**: Using the **DHT11 sensor**, this system tracks the humidity inside the vehicle, providing alerts when humidity exceeds predefined levels.
- **Distance Measurement**: An **ultrasonic distance sensor** helps measure the proximity to objects, assisting with parking and collision avoidance.
- **Obstacle Detection**: Detects objects in the vehicle’s path using a dedicated sensor.
- **LED Indicators**: Visual feedback using a set of **5 LEDs** that represent the proximity of obstacles (distance), and hazard lights that flash when humidity is high.
- **Audible Alerts**: A **buzzer** provides audible warnings when the vehicle is near an obstacle or when other alert conditions (like high humidity) are met.
- **LCD Display**: A **16x2 LCD screen** displays real-time data such as distance and humidity levels.
- **IoT Integration (ThingSpeak)**: The system sends data to **ThingSpeak**, allowing remote monitoring of vehicle conditions over WiFi.

## Requirements:
- **Hardware**:
  - ESP32 microcontroller
  - DHT11 Humidity Sensor
  - Ultrasonic Distance Sensor (HC-SR04)
  - Obstacle Detection Sensor
  - 5x LEDs for visual indicators
  - Buzzer for audible alerts
  - 16x2 LCD (I2C interface)
  - Breadboard and jumper wires

- **Software**:
  - Arduino IDE or PlatformIO
  - Libraries:
    - `LiquidCrystal_I2C` for LCD display
    - `DHT` for humidity sensor
    - `WiFi` for ESP32 WiFi connectivity
    - `HTTPClient` for HTTP requests to ThingSpeak

## Wiring:
- **DHT11**: Connect to pin `32` of the ESP32.
- **Ultrasonic Sensor**: 
  - **Trigger Pin**: Pin `5`
  - **Echo Pin**: Pin `4`
- **Obstacle Detection Sensor**: Pin `18`
- **LEDs**: Pins `2`, `14`, `27`, `26`, and `25` (for the LED bar).
- **Buzzer**: Pin `19`
- **LCD**: I2C interface connected to `SDA` (pin `21`) and `SCL` (pin `22`).

## Setup:
1. **Install Arduino Libraries**:
   - Install the **DHT sensor library** and **LiquidCrystal_I2C library** using the Library Manager in the Arduino IDE.
   
2. **WiFi Configuration**:
   - Replace the `ssid` and `password` in the code with your Wi-Fi credentials.
   
3. **ThingSpeak Setup**:
   - Create a ThingSpeak account and set up a channel for your vehicle metrics.
   - Replace the `API_KEY` and `THINGSPEAK_URL` in the code with your ThingSpeak API key and URL.

4. **Upload Code to ESP32**:
   - Open the Arduino IDE, select your ESP32 board, and upload the provided code to the ESP32.

## Code Overview:
- **Distance Measurement**: The ultrasonic sensor sends a pulse, and the ESP32 measures the time it takes for the pulse to bounce back, calculating the distance to nearby objects.
- **Humidity Measurement**: The **DHT11 sensor** reads the humidity level inside the vehicle. If the humidity exceeds the defined threshold (60%), hazard lights are activated by flashing LEDs.
- **Obstacle Detection**: The system continuously checks if an obstacle is present in front of the vehicle and provides alerts on the LCD screen, LED indicators, and the buzzer.
- **LED Bar**: Based on the distance to an obstacle, a number of LEDs are lit to provide a visual representation of how close the vehicle is to the obstacle.
- **Remote Monitoring**: The system sends the collected data (humidity, distance, and obstacle status) to **ThingSpeak** via WiFi every time it loops.

## Remote Monitoring (ThingSpeak):
You can monitor the collected data on **ThingSpeak**. The system sends three data fields:
- **Field 1**: Humidity value (%)
- **Field 2**: Distance value (cm)
- **Field 3**: Obstacle status (1 for obstacle detected, 0 for no obstacle)

You can visualize the data using ThingSpeak’s built-in plotting and analysis tools.

## Applications:
- **Parking Assistance**: The ultrasonic distance sensor and LEDs help the driver park the vehicle safely by providing feedback on distance to obstacles.
- **Vehicle Climate Monitoring**: Monitoring the humidity helps avoid potential issues like window fogging or mildew buildup in the cabin.
- **Safety Warnings**: The obstacle detection system and buzzer provide immediate alerts when something is blocking the vehicle's path, improving safety.
- **Fleet Management**: Fleet managers can remotely monitor the environmental conditions of their vehicles using ThingSpeak, helping to detect potential issues early on.

## Example of Data Display on LCD:
- **Distance**: The LCD will display the current distance to objects (in cm) in real-time.
- **Humidity**: The LCD will display the humidity level inside the vehicle.

## Known Issues:
- **DHT11 Sensor Accuracy**: The DHT11 sensor is not highly accurate and can sometimes fail to provide readings. Consider using the DHT22 for more accurate humidity readings if needed.
- **WiFi Connectivity**: Ensure a stable Wi-Fi connection for uninterrupted data transfer to ThingSpeak.

## Future Improvements:
- Add a temperature sensor to monitor the internal temperature of the vehicle.
- Integrate a camera or more sensors for enhanced collision avoidance.
- Implement a mobile app or web interface to receive real-time notifications and view metrics.

## License:
This project is open-source and can be modified or redistributed according to your needs.

---

Feel free to contribute, suggest improvements, or ask questions by opening an issue or pull request on this repository!
