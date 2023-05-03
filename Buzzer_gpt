// Define constants
const int FSR_PIN = A0;  // Analog pin to read FSR sensor
const int BUZZER_PIN = 10;  // Digital pin to control buzzer
const int THRESHOLD = 500;  // Force threshold in grams

// Initialize buzzer object
void setup() {
  pinMode(BUZZER_PIN, OUTPUT);
}

// Main loop
void loop() {
  // Read force value from FSR sensor
  int force = analogRead(FSR_PIN);

  // Convert force value to grams
  force = map(force, 0, 1023, 0, 1000);

  // Check if force exceeds threshold
  if (force > THRESHOLD) {
    // Turn on buzzer
    digitalWrite(BUZZER_PIN, HIGH);
  } else {
    // Turn off buzzer
    digitalWrite(BUZZER_PIN, LOW);
  }

  // Wait for a short time to avoid spamming the buzzer
  delay(100);
}
