# Automatic Sanitizer Dispenser

An Arduino-based contactless hand sanitizer dispenser developed using IR sensor and servo motor.

## 🧾 Project Description

This project is a **contactless automatic hand sanitizer dispenser** designed and implemented using an **Arduino Uno**, **IR sensor**, and **servo motor**. The dispenser detects the presence of a hand using the IR sensor and activates a servo motor to press a sanitizer bottle pump, dispensing a small amount of sanitizer without any physical touch.

## 🔧 Components Used
- Arduino Uno
- IR Sensor
- Servo Motor
- Jumper Wires
- Sanitizer Bottle

## 💡 How It Works
The IR sensor detects a nearby hand. When detection is made, the Arduino triggers the servo motor to rotate, pressing the sanitizer pump and dispensing liquid.

## 📜 Arduino Code
```cpp
#include <Servo.h>
Servo servo;
int irSensor = 2;
int value = 0;

void setup() {
  servo.attach(9);
  pinMode(irSensor, INPUT);
  servo.write(0);
}

void loop() {
  value = digitalRead(irSensor);
  if (value == 0) {
    servo.write(90);
    delay(1000);
    servo.write(0);
    delay(2000);
  }
}

