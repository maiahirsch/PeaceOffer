// ROBOTIC FLOWER DRESS
// by Maia Hirsch

#include <Wire.h> // I2C communication. Allows multiple devices to communicate using SDA (to send data) and SCL (to synchronize communication)
#include <Adafruit_PWMServoDriver.h> // Designed to control the Adafruit 16-channel PWM/Servo driver. 

// Constants
const int TOUCH_PIN = 6; // Arduino pin connected to TTP223B Capacitive Touch Sensor's OUT pin
Adafruit_PWMServoDriver pwm = Adafruit_PWMServoDriver(); // Creates an instance (pwm) allowing communication with the PWM servo driver and control of the 16 PWM channels.

#define SERVOMIN 150   // This is the 'minimum' pulse length count (out of 4096)
#define SERVOMAX 600   // This is the 'maximum' pulse length count (out of 4096)
#define SERVO_FREQ 50  // Analog servos run at ~50 Hz updates

// Variables
bool isTouchActive = false; // Tracks the current state of the circuit

void setup() {
  Serial.begin(9600);
  pinMode(TOUCH_PIN, INPUT); // Set Arduino pin to input mode
  Serial.println("Robotic Dress Ready!");

  pwm.begin();
  pwm.setPWMFreq(SERVO_FREQ); // Analog servos run at ~50 Hz updates
}

void loop() {
  // Read the state of the touch sensor
  int touchState = digitalRead(TOUCH_PIN); // HIGH = circuit closed, LOW = circuit open

  if (touchState == HIGH) {
    // Circuit closed: Rotate the motors
    if (!isTouchActive) {
      rotateMotors(); // Function to move the motors
      isTouchActive = true; // Update state to prevent re-triggering
    }
  } else {
    // Circuit open: Stop the motors
    if (isTouchActive) {
      stopMotors(); // Function to stop the motors
      isTouchActive = false; // Update state
    }
  }

  delay(50); // Small delay to avoid rapid state changes
}

// Function to rotate the motors
void rotateMotors() {
  for (int pos = 110; pos < 320; pos += 1) {
    pwm.setPWM(0, 0, pos);
    pwm.setPWM(1, 0, pos);
    pwm.setPWM(2, 0, pos);
    pwm.setPWM(3, 0, pos);
    Serial.println("Motors Rotating...");
    delay(10);
  }
}

// Function to stop the motors
void stopMotors() {
  pwm.setPWM(0, 0, SERVOMIN); // Set servos to minimum position
  pwm.setPWM(1, 0, SERVOMIN);
  pwm.setPWM(2, 0, SERVOMIN);
  pwm.setPWM(3, 0, SERVOMIN);
  Serial.println("Motors Stopped.");
}
