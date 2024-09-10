# Robotic_Arm
To make a Robic Arm Operated by Wi-Fi at any part of the world.

Components : Arduino UNO and ESP32

Arduino Code:

#define BLYNK_TEMPLATE_ID "Your_Template_ID"
#define BLYNK_DEVICE_NAME "Your_Device_Name"
#define BLYNK_AUTH_TOKEN "Your_Blynk_Auth_Token"  // Enter your Blynk Auth Token here

// Libraries
#include <WiFi.h>
#include <BlynkSimpleEsp32.h>
#include <ESP32Servo.h>

// Your WiFi credentials
char ssid[] = "Your_SSID";      // Enter your WiFi SSID
char pass[] = "Your_PASSWORD";  // Enter your WiFi Password

// Define pins for servos
#define BASE_SERVO_PIN 18
#define SHOULDER_SERVO_PIN 19
#define ELBOW_SERVO_PIN 21
#define WRIST_SERVO_PIN 22
#define GRIPPER_SERVO_PIN 23

// Create Servo objects
Servo baseServo;
Servo shoulderServo;
Servo elbowServo;
Servo wristServo;
Servo gripperServo;

// Virtual pin numbers (as defined in Blynk app)
#define V0_BASE  V0
#define V1_SHOULDER  V1
#define V2_ELBOW  V2
#define V3_WRIST  V3
#define V4_GRIPPER  V4

void setup() {
  // Begin serial communication
  Serial.begin(115200);

  // Setup Blynk connection
  Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass);

  // Attach servos to respective pins
  baseServo.attach(BASE_SERVO_PIN);
  shoulderServo.attach(SHOULDER_SERVO_PIN);
  elbowServo.attach(ELBOW_SERVO_PIN);
  wristServo.attach(WRIST_SERVO_PIN);
  gripperServo.attach(GRIPPER_SERVO_PIN);
}

// Blynk slider controls (0 to 180 degrees for each servo)
// Base rotation
BLYNK_WRITE(V0_BASE) {
  int baseAngle = param.asInt();  // Get the angle from Blynk app slider
  baseServo.write(baseAngle);     // Move the base servo
  Serial.print("Base Angle: ");
  Serial.println(baseAngle);
}

// Shoulder movement
BLYNK_WRITE(V1_SHOULDER) {
  int shoulderAngle = param.asInt();  // Get the angle from Blynk app slider
  shoulderServo.write(shoulderAngle); // Move the shoulder servo
  Serial.print("Shoulder Angle: ");
  Serial.println(shoulderAngle);
}

// Elbow movement
BLYNK_WRITE(V2_ELBOW) {
  int elbowAngle = param.asInt();  // Get the angle from Blynk app slider
  elbowServo.write(elbowAngle);    // Move the elbow servo
  Serial.print("Elbow Angle: ");
  Serial.println(elbowAngle);
}

// Wrist movement
BLYNK_WRITE(V3_WRIST) {
  int wristAngle = param.asInt();  // Get the angle from Blynk app slider
  wristServo.write(wristAngle);    // Move the wrist servo
  Serial.print("Wrist Angle: ");
  Serial.println(wristAngle);
}

// Gripper control
BLYNK_WRITE(V4_GRIPPER) {
  int gripperAngle = param.asInt();  // Get the angle from Blynk app slider
  gripperServo.write(gripperAngle);  // Move the gripper servo
  Serial.print("Gripper Angle: ");
  Serial.println(gripperAngle);
}

void loop() {
  // Run Blynk
  Blynk.run();
}
