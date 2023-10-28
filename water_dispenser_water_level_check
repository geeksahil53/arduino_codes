#include <LiquidCrystal.h>

const int waterLevelTrigPin = 7;   // Trigger pin of the water level ultrasonic sensor
const int waterLevelEchoPin = 6;   // Echo pin of the water level ultrasonic sensor
const int glassDetectionTrigPin = 9; // Trigger pin of the glass detection ultrasonic sensor
const int glassDetectionEchoPin = 8; // Echo pin of the glass detection ultrasonic sensor
const int relayPin = 4;             // Control pin of the relay for the water pump

const int tankCapacity = 2000; // Total tank capacity in cubic centimeters (2 liters)
int initialWaterLevel = 0;
int currentWaterLevel = 0;

LiquidCrystal lcd(12, 11, 5, 3, 2, 1); // LCD connections

bool glassDetected = false;

void setup() {
  pinMode(waterLevelTrigPin, OUTPUT);
  pinMode(waterLevelEchoPin, INPUT);
  pinMode(glassDetectionTrigPin, OUTPUT);
  pinMode(glassDetectionEchoPin, INPUT);
  pinMode(relayPin, OUTPUT);
  pinMode(ledPin, OUTPUT);
  digitalWrite(relayPin, LOW); 
  lcd.begin(16, 2);            
  lcd.clear();                 

  initialWaterLevel = measureWaterLevel();
  currentWaterLevel = initialWaterLevel;
}

void loop() {
  currentWaterLevel = measureWaterLevel();
  int percentage = map(currentWaterLevel, 0, tankCapacity, 100, 0);
  
  lcd.setCursor(0, 0);
  lcd.print("Water Level: ");
  lcd.print(currentWaterLevel);
  lcd.print(" cm");
  lcd.setCursor(0, 1);
  lcd.print("Percentage: ");
  lcd.print(percentage);
  lcd.print("%");

  if (glassDetectionDistance < 10) {
    glassDetected = true;
  }

 
  if (glassDetected) {
   
    digitalWrite(relayPin, HIGH);
    lcd.setCursor(0, 2);
    lcd.print("Dispensing Water");
  
    
    // Decrease the current water level 
    currentWaterLevel -= 1;
  } else {
    // Turn off the water pump using the relay
    digitalWrite(relayPin, LOW);
    lcd.setCursor(0, 2);
    lcd.print("Water OK        ");
    glassDetected = false; //flag
  }

  delay(1000); 
}

int measureWaterLevel() {
  long waterLevelDuration, waterLevel;
  digitalWrite(waterLevelTrigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(waterLevelTrigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(waterLevelTrigPin, LOW);
  waterLevelDuration = pulseIn(waterLevelEchoPin, HIGH);
  waterLevel = (waterLevelDuration / 2) / 29.1; //conversion to centimeters

  return waterLevel;
}
