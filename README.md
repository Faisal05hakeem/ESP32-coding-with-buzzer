# ESP32-coding-with-buzzer
coding for my project (wokwi)

// Define pins for ultrasonic sensor
#define TRIG_PIN 5
#define ECHO_PIN 18

// Define pin for buzzer
#define BUZZER_PIN 15

long duration;
float distanceCm;
const float thresholdDistance = 20.0; // Threshold distance in cm to trigger buzzer

void setup() {
  Serial.begin(115200);
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(BUZZER_PIN, OUTPUT);
  digitalWrite(BUZZER_PIN, LOW);
}

void loop() {
  // Clear the trigPin
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);

  // Trigger the sensor by setting the trigPin HIGH for 10 microseconds
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  // Read the echoPin, returns the sound wave travel time in microseconds
  duration = pulseIn(ECHO_PIN, HIGH);

  // Calculate the distance
  distanceCm = (duration * 0.0343) / 2.0;

  Serial.print("Distance: ");
  Serial.print(distanceCm);
  Serial.println(" cm");

  if (distanceCm > 0 && distanceCm <= thresholdDistance) {
    // Obstacle is near - beep buzzer
    digitalWrite(BUZZER_PIN, HIGH);
  } else {
    // No obstacle near - turn off buzzer
    digitalWrite(BUZZER_PIN, LOW);
  }

  delay(100);
}
