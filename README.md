
# Digital-Sensors-
Report on the Design and Programming of Digital and Analog Sensors Using Arduino

Introduction:
This report provides an analysis, design, and programming approach for digital and analog sensors using the Arduino microcontroller. The project focuses on integrating multiple sensors to control light and sound signals based on the measured values. The ultrasonic sensor (HC-SR04) was utilized, alongside optical and audio outputs such as light-emitting diodes (LEDs) and a buzzer.


Project Objectives:
Digital Sensors 
1. To measure distance using the ultrasonic sensor.
2. To activate light and sound signals based on the measured distance.
3. To achieve dynamic control over digital and analog outputs.
----
Materials and Components:

1. Arduino Uno microcontroller.
2. Ultrasonic sensor (HC-SR04).
3. Buzzer.
4. Light-emitting diodes (LEDs) in three colors: Green, Yellow, and Red.
5. Various resistors of different values.
6. Connecting wires and breadboard.

---


Methodology:

1. Distance Measurement Using the Ultrasonic Sensor:

   The ultrasonic sensor operates by emitting a pulse through the "Trigger" pin and receiving the reflected sound wave through the "Echo" pin. The distance is calculated using the time difference between the pulse emission and reception, applying the following equation:

2. Control of Light and Sound Signals:

   Based on the measured distance, the following actions are performed:
   - If the distance exceeds 154.94 cm, the red LED is activated.
   - If the distance is between 78.74 and 154.94 cm, the yellow LED is activated, and the buzzer emits a tone at 300 Hz.
   - If the distance is between 2.54 and 78.74 cm, the green LED is activated, and the buzzer emits a tone at 700 Hz.
   - If the distance is less than 2.54 cm, the green LED is activated, and the buzzer is turned off.

---

Code Implementation:

```cpp
int buzzer = 8;
int cm = 0;
int inches = 0;

long readUltrasonicDistance(int triggerPin, int echoPin) {
  pinMode(triggerPin, OUTPUT);
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  pinMode(echoPin, INPUT);
  return pulseIn(echoPin, HIGH);
}

void setup() {
  Serial.begin(9600);
  pinMode(2, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(buzzer, OUTPUT);
}

void loop() {
  cm = 0.01723 * readUltrasonicDistance(6, 7);
  inches = (cm / 2.54);
  Serial.print(cm);
  Serial.print("cm, ");
  Serial.print(inches);
  Serial.println("in");

  if (cm >= 154.94) {
      digitalWrite(2, LOW);
      digitalWrite(3, LOW);
      digitalWrite(4, HIGH);
      noTone(buzzer);
  } else if (cm >= 78.74) {
      digitalWrite(2, LOW);
      digitalWrite(3, HIGH);
      digitalWrite(4, LOW);
      tone(buzzer, 300);
  } else if (cm >= 2.54) {
      digitalWrite(2, HIGH);
      digitalWrite(3, LOW);
      digitalWrite(4, LOW);
      tone(buzzer, 700);
  } else {
      digitalWrite(2, HIGH);
      digitalWrite(3, LOW);
      digitalWrite(4, LOW);
      noTone(buzzer);
  }
  delay(100);
}
Expected Outcomes:

- Proper activation of the LEDs and buzzer based on the measured values.
- Accurate distance measurement with optimized response time.

Conclusion:
The project successfully designed and programmed digital and analog sensors using the Arduino platform. It achieved the desired functionality, meeting the objectives of controlling light and sound outputs based on sensor readings. The design can be enhanced further by integrating additional sensors for improved accuracy and implementing intelligent control mechanisms. This system shows promising potential for applications in robotics and smart environments.
-- 
