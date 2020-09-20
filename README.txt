# iot_a

//###Lcd and arduino###
#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd(0x27,16,2);
void setup(){
  lcd.begin(16,2);
  lcd.backlight();
  }

void loop(){
  lcd.setCursor(5,0);
  lcd.print("Hello");
  delay(1000);
  lcd.clear();
  delay(1000);
  }

//###LDR and Arduino###

int analogPin = 1;
int value = 0;
void setup(){
  Serial.begin(9600);
}
void loop(){
  value = analogRead(analogPin);
  Serial.print("Light intensity = ");
  Serial.println(value);
  delay(500);
}

//workshop4

//###Ultrasonic####
int echoPin = 12;
int trigPin = 13;

float duration, distance;
void setup() {
  Serial.begin (9600);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);

  //Calculate the distance (in cm) based on the speed of sound.
  distance = duration / 58.2;
  Serial.print("Distance = ");
  Serial.print(distance);
  Serial.println("cm");
  delay(100);
}

//###DHT###

#include "DHT.h"

#define DHTPIN 8
#define DHTTYPE DHT11
float h,t;
DHT dht(DHTPIN,DHTTYPE);

void setup(){
  Serial.begin(9600);
  dht.begin();
}

void loop(){
  h = dht.readHumidity();
  t = dht.readTemperature();
  
  Serial.print("Humidity : ");
  Serial.print(h);
  Serial.print(" %\t");
  Serial.print("Temperature : ");
  Serial.print(t);
  Serial.println(" *c");
  delay(500);
}





