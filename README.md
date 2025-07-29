# Automatic Hand Sanitizer Dispenser

An Arduino-based contactless hand sanitizer dispenser using an ultrasonic sensor for hand detection and a potentiometer to control the quantity of sanitizer dispensed through a relay-controlled motor.

---

## 🧾 Project Description

This project implements a fully automatic and contactless sanitizer dispenser using **Arduino Uno**, **ultrasonic sensor**, **potentiometer**, **relay**, and **DC motor**. The ultrasonic sensor detects the user's hand near the dispenser, and based on the potentiometer setting, the system controls how much sanitizer is dispensed.

---

## 🔧 Components Used

- Arduino Uno  
- Ultrasonic Sensor (HC-SR04)  
- Potentiometer  
- Relay Module  
- DC Motor / Pump  
- Jumper Wires  
- Sanitizer Bottle  
- Power Supply (Battery or Adapter)

---

## 💡 How It Works

1. The **ultrasonic sensor** continuously measures the distance in front of it.
2. When a hand is detected within a certain range (e.g., < 10 cm), the **Arduino** triggers the **relay** to activate the **DC motor**.
3. The **potentiometer** is used to control the dispensing time, i.e., how long the motor runs (and hence, the quantity of sanitizer).
4. After the set duration, the motor turns off automatically.

---

## 📜 Arduino Code

```cpp
#define TRIG 9
#define ECHO 8
#define RELAY 7
#define POT A0

void setup() {
  pinMode(TRIG, OUTPUT);
  pinMode(ECHO, INPUT);
  pinMode(RELAY, OUTPUT);
  pinMode(POT, INPUT);
  digitalWrite(RELAY, LOW);
  Serial.begin(9600);
}

void loop() {
  long duration;
  int distance;
  int potValue = analogRead(POT);             // Read potentiometer
  int dispenseTime = map(potValue, 0, 1023, 500, 3000); // Map to 0.5 to 3 seconds

  // Trigger ultrasonic
  digitalWrite(TRIG, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG, LOW);

  duration = pulseIn(ECHO, HIGH);
  distance = duration * 0.034 / 2;

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.print(" cm  |  Dispense Time: ");
  Serial.println(dispenseTime);

  if (distance > 0 && distance < 10) {
    digitalWrite(RELAY, HIGH);     // Turn on motor
    delay(dispenseTime);           // Based on potentiometer
    digitalWrite(RELAY, LOW);      // Turn off motor
    delay(2000);                   // Wait before next detection
  }

  delay(100);
}

## 🎓 Academic Information

- 🔬 **Semester**: 4th Semester (Minor Project)
- 🏫 **College**: Aditya Engineering college
- 🎓 **Branch**: Electronics and Communication Engineering
- 👨‍💻 **Developed by**: Mohan Pulla
## these are the images and project assemble and testing videos


https://github.com/user-attachments/assets/b6aeeeee-961c-48c1-9786-5c259d464351

![maxresdefault](https://github.com/user-attachments/assets/fd7a6888-ed66-41ba-a55d-dc6d3b6fbc9f)



