<img width="955" height="619" alt="image" src="https://github.com/user-attachments/assets/6d2b7ce7-9c78-4139-a6aa-74b0785e7686" />


## 🧑‍💻 Introduction

The demand for effective and user-friendly monitoring systems is always rising in our technologically driven era. One such project is the development of a Bluetooth-enabled wireless temperature and humidity monitoring system, which makes use of **MIT App Inventor’s** ease of use and adaptability. This project makes use of an Arduino Uno, DHT-11 sensor, HC-05 Bluetooth module, and a few other necessary parts to enable you to easily monitor environmental conditions. Come along on this adventure as we explore the nuances of developing a reliable temperature and humidity monitoring system.

---

## 🔧 Components Required

- Solderless Breadboard  
- Arduino UNO  
- HC-05 Bluetooth Module  
- DHT-22 Temperature & Humidity Sensor  
- 16×2 LCD Display  
- 100Ω Resistor  
- 4.7kΩ Resistor  
- 1kΩ Resistor  
- Male-to-Male Jumper Wires  
- Battery Clip  
- 9V Battery  

---

## 🧪 Proteus Simulation

It’s advisable to use Proteus to simulate the circuit before beginning the actual construction. Prior to implementing the hardware, this process verifies that the connections are accurate and aids in locating and resolving any possible problems.

Open the simulation file on Proteus 8. Here, Arduino UNO is used as a microcontroller. A **HC-05 Bluetooth** module is used. A **16×2 LCD** is used as a display. DHT11 temperature and humidity sensor is used. The data pin of the sensor is connected to the A0 pin of the Arduino UNO. Virtual terminal is used that will receive the data by Bluetooth. Run the code and copy hex file address. Then place the hex file address in Arduino UNO and run the simulation. The values of temperature and humidity will be shown on the LCD. The virtual terminal will shoe the received values by Bluetooth.

<img width="977" height="577" alt="image" src="https://github.com/user-attachments/assets/2abc34d4-ae3e-4426-b233-04b019356fb1" />

---

## 🔌 Circuit Diagram

A clear and well-structured circuit diagram is essential for constructing the monitoring system accurately.  
The schematic should illustrate how each component—such as the **Arduino UNO**, **DHT11 sensor**, **16×2 LCD display**, and **HC-05 Bluetooth module**—is connected, ensuring that anyone building the project can follow it easily.

In this circuit:

- A **9V battery** is used as the main power source.
- The **DHT11 sensor** measures both temperature and humidity.
  - Its **output pin is connected to the A0 pin** of the Arduino UNO.
- The **HC-05 Bluetooth module** is used to establish a wireless connection with the mobile application.
  - **RX → Pin 9** of Arduino UNO  
  - **TX → Pin 8** of Arduino UNO
- A **16×2 LCD** is included to display real-time temperature and humidity values.

This circuit layout ensures proper data flow from the sensor to the microcontroller, then to the LCD and Bluetooth module for monitoring and wireless communication.

<img width="1072" height="776" alt="image" src="https://github.com/user-attachments/assets/0d36abd3-99ed-466d-b6e1-b57dce07bf9d" />

---

## 📱 MIT App Inventor

**MIT App Inventor** is a visual, block-based programming environment that simplifies the process of creating Android applications.  
For this project, it plays a crucial role in enabling easy interaction between the user and the wireless monitoring system.

Using MIT App Inventor, you can:

- Create a clean and user-friendly mobile interface.
- Add a **Bluetooth Connect** button to pair the smartphone with the **HC-05 Bluetooth module**.
- Receive real-time **temperature and humidity data** sent from the Arduino.
- Display the received values in a structured and readable format on the app.

App Inventor works seamlessly with the HC-05 Bluetooth module, ensuring a smooth and reliable wireless connection.  
By combining the app with the hardware setup, users can monitor environmental conditions directly from their mobile devices anytime, anywhere.


<img width="966" height="529" alt="image" src="https://github.com/user-attachments/assets/f403fe77-f07f-4f10-b1d4-950e33e726ee" />

<img width="429" height="715" alt="image" src="https://github.com/user-attachments/assets/3fd29121-248a-4070-83a9-eab12d385149" />

---

## 🔧 Arduino IDE Code

The following Arduino code reads temperature and humidity values from the **DHT11 sensor**, displays them on a **16×2 LCD**, and sends the data via **HC-05 Bluetooth** to the MIT App Inventor mobile application.

## 🔧 Arduino IDE Code

The following Arduino code reads temperature and humidity values from the **DHT11 sensor**, displays them on a **16×2 LCD**, and sends the data via **HC-05 Bluetooth** to the MIT App Inventor mobile application.

```cpp
#include <SoftwareSerial.h>
SoftwareSerial bt(8, 9); // RX, TX

#include <LiquidCrystal.h>
#include "dht.h"

#define dataPin A0
LiquidCrystal lcd(2, 3, 4, 5, 6, 7);
dht DHT;

int temp;
int hum;

void setup() {

  Serial.begin(9600);
  bt.begin(9600);
  Serial.println("Ready");

  lcd.begin(16,2);
  lcd.setCursor(0,0);
  lcd.print(" WELCOME To  My ");
  lcd.setCursor(0,1);
  lcd.print("YouTube  Channel");
  delay(2000);
  lcd.clear();
}

void loop() {
  int readData = DHT.read11(dataPin);

  hum = DHT.humidity;
  temp = DHT.temperature;

  lcd.setCursor(0,0);
  lcd.print("Humidity: ");
  lcd.print(hum);
  lcd.print("% ");

  lcd.setCursor(0,1);
  lcd.print("Temp: ");
  lcd.print(temp);
  lcd.print((char)223); // degree symbol
  lcd.print("C ");

  bt.print(temp);   // send temperature to MIT App
  bt.print(";");
  bt.print(hum);    // send humidity to MIT App
  bt.println(";");

  delay(1000);
}
```
---

## 📝 Explanation

The Arduino code begins by including two important libraries:  
- **LiquidCrystal** – used to interface with the 16×2 LCD display  
- **SoftwareSerial** – used to create a software-based serial port for communicating with the HC-05 Bluetooth module  

Two variables, `temp` and `hum`, are used to store the temperature and humidity readings obtained from the **DHT11 sensor**.

### 🔧 setup() Function
In the `setup()` function:
- Serial communication is initialized at **9600 baud** for debugging.
- The Bluetooth module is also started at **9600 baud** using SoftwareSerial.
- The LCD is initialized, and a welcome message is displayed for two seconds.
- After the delay, the LCD screen is cleared and becomes ready to show live sensor data.

### 🔄 loop() Function
Inside the `loop()` function:
- The DHT11 sensor is read, and the temperature and humidity values are updated.
- These values are displayed on the 16×2 LCD in real time.
- The same data is sent to the MIT App Inventor through the HC-05 Bluetooth module.
- Semicolons (`;`) are used to separate the temperature and humidity values, making it easy for the mobile app to parse the incoming data.
- The entire cycle repeats every **1 second**.

### 📡 Summary
This code:
- Reads temperature and humidity from the **DHT11 sensor**  
- Displays the readings on a **16×2 LCD**  
- Sends the data wirelessly using the **HC-05 Bluetooth module**  
- Provides a structured Bluetooth output suitable for integration with **MIT App Inventor** for live monitoring  

---

## 🧹 Hardware Testing

<img width="968" height="571" alt="image" src="https://github.com/user-attachments/assets/070375a3-6266-4f08-a3c6-5edf350d4f64" />

<img width="963" height="559" alt="image" src="https://github.com/user-attachments/assets/54ab803a-33f7-407b-b78b-18abb2bf06d4" />


Once the circuit has been assembled and the Arduino code uploaded, the system is ready for hardware testing. This stage ensures that all components work correctly in real-world conditions and that the system performs as expected.

During testing, verify the following:

- **Sensor Accuracy:**  
  Check that the DHT11 sensor accurately detects temperature and humidity values.

- **LCD Display:**  
  Confirm that the measured values are displayed clearly on the 16×2 LCD.

- **Bluetooth Communication:**  
  Ensure the HC-05 module successfully pairs with your smartphone.

- **MIT App Inventor App:**  
  Verify that the mobile application receives the transmitted temperature and humidity values via Bluetooth.

Once connected, the sensed temperature and humidity readings should appear on the mobile app in real time. This confirms that the entire monitoring system—sensor, Arduino, LCD, Bluetooth module, and app—is working seamlessly together.

<img width="955" height="619" alt="image" src="https://github.com/user-attachments/assets/33c53620-708a-4714-8f06-a0cff045d3e2" />

---

## 🏁 Conclusion

To sum up, the Wireless Temperature and Humidity Monitoring System provides an easy-to-use and entertaining method of monitoring ambient conditions. With the help of the Arduino, DHT-11 sensor, HC-05 Bluetooth module, and **MIT App Inventor**, this project opens up a world of monitoring and automation possibilities. This project may be used for educational or personal reasons, and it provides an introduction to the exciting realm of DIY electronics and the Internet of Things.


