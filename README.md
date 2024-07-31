# Line-tracing-robots
This code is a basic example and might need adjustments based on your specific hardware and requirements. Ensure your motor driver and sensors are correctly connected and calibrated for your robot’s environment.
// Motor pins
const int motorAForward = 5;
const int motorABackward = 6;
const int motorBForward = 9;
const int motorBBackward = 10;

// Sensor pins
const int leftSensor = A0;
const int rightSensor = A1;

void setup() {
  // Initialize motor pins as outputs
  pinMode(motorAForward, OUTPUT);
  pinMode(motorABackward, OUTPUT);
  pinMode(motorBForward, OUTPUT);
  pinMode(motorBBackward, OUTPUT);
  
  // Initialize sensor pins as inputs
  pinMode(leftSensor, INPUT);
  pinMode(rightSensor, INPUT);
}

void loop() {
  int leftValue = analogRead(leftSensor);
  int rightValue = analogRead(rightSensor);

  // Define threshold value to distinguish line from background
  int threshold = 512;

  if (leftValue < threshold && rightValue < threshold) {
    // Both sensors are on the line (move forward)
    moveForward();
  } else if (leftValue < threshold) {
    // Left sensor is on the line (turn right)
    turnRight();
  } else if (rightValue < threshold) {
    // Right sensor is on the line (turn left)
    turnLeft();
  } else {
    // Both sensors are off the line (stop)
    stop();
  }
}

void moveForward() {
  digitalWrite(motorAForward, HIGH);
  digitalWrite(motorABackward, LOW);
  digitalWrite(motorBForward, HIGH);
  digitalWrite(motorBBackward, LOW);
}

void turnLeft() {
  digitalWrite(motorAForward, LOW);
  digitalWrite(motorABackward, LOW);
  digitalWrite(motorBForward, HIGH);
  digitalWrite(motorBBackward, LOW);
}

void turnRight() {
  digitalWrite(motorAForward, HIGH);
  digitalWrite(motorABackward, LOW);
  digitalWrite(motorBForward, LOW);
  digitalWrite(motorBBackward, LOW);
}

void stop() {
  digitalWrite(motorAForward, LOW);
  digitalWrite(motorABackward, LOW);
  digitalWrite(motorBForward, LOW);
  digitalWrite(motorBBackward, LOW);
}
