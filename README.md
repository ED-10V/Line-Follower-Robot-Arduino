# Line Follower Robot using Arduino

## 📌 Overview
A 2-wheel differential robot that follows a black line using IR sensors. Arduino reads sensor values and controls motors through L293D driver.

## 🛠 Components Used
- Arduino Uno  
- IR Sensor Module (2 nos)  
- L293D Motor Driver  
- BO Motors + Wheels  
- Chassis  
- 9V/12V Battery  

## ⚡ Features
- Autonomous movement  
- Easy logic implementation  
- Good beginner robotics project

## 📡 Sensor Logic
LEFT sensor detects the line → turn left  
RIGHT sensor detects the line → turn right  
BOTH HIGH → go straight  

## 📜 Code
// IR Sensor Pins
int leftIR  = 2;
int rightIR = 3;

// Motor driver pins
int motorLeftForward  = 5;
int motorLeftBackward = 6;
int motorRightForward = 9;
int motorRightBackward = 10;

void setup() {
  pinMode(leftIR, INPUT);
  pinMode(rightIR, INPUT);

  pinMode(motorLeftForward, OUTPUT);
  pinMode(motorLeftBackward, OUTPUT);
  pinMode(motorRightForward, OUTPUT);
  pinMode(motorRightBackward, OUTPUT);

  Serial.begin(9600);
}

void forward() {
  digitalWrite(motorLeftForward, HIGH);
  digitalWrite(motorLeftBackward, LOW);
  digitalWrite(motorRightForward, HIGH);
  digitalWrite(motorRightBackward, LOW);
}

void left() {
  digitalWrite(motorLeftForward, LOW);
  digitalWrite(motorLeftBackward, LOW);
  digitalWrite(motorRightForward, HIGH);
  digitalWrite(motorRightBackward, LOW);
}

void right() {
  digitalWrite(motorLeftForward, HIGH);
  digitalWrite(motorLeftBackward, LOW);
  digitalWrite(motorRightForward, LOW);
  digitalWrite(motorRightBackward, LOW);
}

void stopRobot() {
  digitalWrite(motorLeftForward, LOW);
  digitalWrite(motorLeftBackward, LOW);
  digitalWrite(motorRightForward, LOW);
  digitalWrite(motorRightBackward, LOW);
}

void loop() {
  int leftValue  = digitalRead(leftIR);
  int rightValue = digitalRead(rightIR);

  Serial.print(leftValue);
  Serial.print(" - ");
  Serial.println(rightValue);

  // BLACK line = LOW
  if(leftValue == LOW && rightValue == LOW) {
    forward();        // both on line → go straight
  }
  else if(leftValue == LOW && rightValue == HIGH) {
    left();           // left sensor on line
  }
  else if(leftValue == HIGH && rightValue == LOW) {
    right();          // right sensor on line
  }
  else {
    stopRobot();      // no line detected
  }
}

## 📷 Circuit Diagram
┌─────────────────────┐
                 │   IR Sensor (Left)  │
                 └──────────┬──────────┘
                            │
                 ┌──────────▼──────────┐
 Path Line ----> │      Arduino         │ ----> Motor Driver ----> Left Motor
                 │      (Controller)    │
                 └──────────▲──────────┘
                            │
                 ┌──────────┴──────────┐
                 │ IR Sensor (Right)    │
                 └──────────────────────┘


         Motor Driver Output:
         - Controls speed & direction  
         - Drives both motors

## 👨‍💻 Author
Ayan Bhattacharjee
