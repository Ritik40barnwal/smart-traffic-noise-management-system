// Pin assignments
const int redLED = 2;
const int yellowLED = 3;
const int greenLED = 4;
const int soundSensor = A0; // <-- potentiometer used here

// Threshold (turn knob above this value = "noise detected")
const int soundThreshold = 950;

// Variables to control the light states
enum LightState {RED, YELLOW, GREEN};
LightState currentState = RED;

void setup() {
  pinMode(redLED, OUTPUT);
  pinMode(yellowLED, OUTPUT);
  pinMode(greenLED, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int soundLevel = analogRead(soundSensor);
  Serial.print("Pot value (simulated sound): ");
  Serial.println(soundLevel);

  // If knob (sound) exceeds threshold, instantly switch to red 
  // BUT skip if current state is GREEN
  if (soundLevel > soundThreshold && currentState != GREEN) {
    switchToRed();
  } else {
    switch (currentState) {
      case RED: redLightCycle(); break;
      case YELLOW: yellowLightCycle(); break;
      case GREEN: greenLightCycle(); break;
    }
  }
}

void redLightCycle() {
  digitalWrite(redLED, HIGH);
  digitalWrite(yellowLED, LOW);
  digitalWrite(greenLED, LOW);
  Serial.println("Red light ON");

  unsigned long startTime = millis();
  while (millis() - startTime < 30000) { // 30 sec
    if (analogRead(soundSensor) > soundThreshold && currentState != GREEN) {
      switchToRed();
      return;
    }
  }
  currentState = YELLOW;
}

void yellowLightCycle() {
  digitalWrite(redLED, LOW);
  digitalWrite(yellowLED, HIGH);
  digitalWrite(greenLED, LOW);
  Serial.println("Yellow light ON");

  unsigned long startTime = millis();
  while (millis() - startTime < 10000) { // 10 sec
    if (analogRead(soundSensor) > soundThreshold && currentState != GREEN) {
      switchToRed();
      return;
    }
  }
  currentState = GREEN;
}

void greenLightCycle() {
  digitalWrite(redLED, LOW);
  digitalWrite(yellowLED, LOW);
  digitalWrite(greenLED, HIGH);
  Serial.println("Green light ON");

  unsigned long startTime = millis();
  while (millis() - startTime < 30000) { // 30 sec
    // 👇 Noise ignored while green is ON
  }
  currentState = RED;
}

void switchToRed() {
  Serial.println("⚠️ Too much noise (pot high)! Switching to red!");
  digitalWrite(redLED, HIGH);
  digitalWrite(yellowLED, LOW);
  digitalWrite(greenLED, LOW);

  // Stay in red until knob (sound) level drops
  while (analogRead(soundSensor) > soundThreshold) {
    delay(100);
  }

  // After knob turned back, hold red for 2 sec
  Serial.println("Level normal. Holding red for 2 sec...");
  delay(2000);

  // Resume cycle (restart same phase from beginning)
  resumeLightState();
}

void resumeLightState() {
  switch (currentState) {
    case RED: redLightCycle(); break;
    case YELLOW: yellowLightCycle(); break;
    case GREEN: greenLightCycle(); break;
  }
}
