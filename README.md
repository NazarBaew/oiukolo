#define TRIGGER_PIN1 2
#define ECHO_PIN1 3
#define TRIGGER_PIN2 4
#define ECHO_PIN2 5
#define TRIGGER_PIN3 6
#define ECHO_PIN3 7
#define TRIGGER_PIN4 8
#define ECHO_PIN4 9

#define BUZZER_PIN 10

void setup() {
  Serial.begin(9600);
  
  pinMode(TRIGGER_PIN1, OUTPUT);
  pinMode(ECHO_PIN1, INPUT);
  pinMode(TRIGGER_PIN2, OUTPUT);
  pinMode(ECHO_PIN2, INPUT);
  pinMode(TRIGGER_PIN3, OUTPUT);
  pinMode(ECHO_PIN3, INPUT);
  pinMode(TRIGGER_PIN4, OUTPUT);
  pinMode(ECHO_PIN4, INPUT);
  
  pinMode(BUZZER_PIN, OUTPUT);
}

void loop() {
  long distance1 = measureDistance(TRIGGER_PIN1, ECHO_PIN1);
  long distance2 = measureDistance(TRIGGER_PIN2, ECHO_PIN2);
  long distance3 = measureDistance(TRIGGER_PIN3, ECHO_PIN3);
  long distance4 = measureDistance(TRIGGER_PIN4, ECHO_PIN4);
  
  if(distance1 < 30) {
    playTone(1000, 500);
  }
  if(distance2 < 30) {
    playTone(2000, 500);
  }
  if(distance3 < 30) {
    playTone(3000, 500);
  }
  if(distance4 < 30) {
    playTone(4000, 500);
  }
  
  delay(100);
}

long measureDistance(int triggerPin, int echoPin) {
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  
  long duration = pulseIn(echoPin, HIGH);
  long distance = duration * 0.034 / 2;
  
  return distance;
}

void playTone(int frequency, int duration) {
  tone(BUZZER_PIN, frequency, duration);
  delay(duration);
  noTone(BUZZER_PIN);
}
