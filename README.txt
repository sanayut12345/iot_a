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


//เฉลย workshop 5

#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd(0x27,16,2);

int echoPin =12;
int trigPin  = 13;

float duration, distance;
void setup() {
  Serial.begin (9600);
  lcd.begin(16,2);
  lcd.backlight();
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

  distance = duration / 58.2;
  lcd.print(distance);
  lcd.print(" cm");
  delay(1000);
  lcd.clear();
  delay(100);
}

//blynk  // button

#define BLYNK_PRINT Serial


#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>

// Blynk Auth Token
char auth[] = "xxx";

// WiFi
char ssid[] = "xxx";
char pass[] = "xxx";

void setup()
{
  Serial.begin(9600);

  Blynk.begin(auth, ssid, pass);
}

void loop()
{
  Blynk.run();
}


//blynk dht
#define BLYNK_PRINT Serial
#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>
#include "DHT.h"
DHT dht;

// You should get Auth Token in the Blynk App.
// Go to the Project Settings (nut icon).
char auth[] = "รหัส Token จาก email";

// Your WiFi credentials.
// Set password to "" for open networks.
char ssid[] = "ชื่อ wifi ที่จะเชื่อมต่อ";
char pass[] = "รหัส wifi";

void setup()
{
  // Debug console
  Serial.begin(9600);

  Blynk.begin(auth, ssid, pass);
  // You can also specify server:
  //Blynk.begin(auth, ssid, pass, "blynk-cloud.com", 80);
  //Blynk.begin(auth, ssid, pass, IPAddress(192,168,1,100), 8080);
  Serial.println();
  Serial.println("Status\tHumidity (%)\tTemperature (C)\t(F)");
  dht.setup(2); // data pin 2
}

void loop()
{
  delay(dht.getMinimumSamplingPeriod());
  float humidity = dht.getHumidity(); // ดึงค่าความชื้น
  float temperature = dht.getTemperature(); // ดึงค่าอุณหภูมิ
  Serial.print(dht.getStatusString());
  Serial.print("\t");
  Serial.print(humidity, 1);
  Serial.print("\t\t");
  Serial.print(temperature, 1);
  Serial.print("\t\t");
  Serial.println(dht.toFahrenheit(temperature), 1);
  Blynk.run();
  delay(100);
  Blynk.virtualWrite(V0, temperature);
  Blynk.virtualWrite(V1, humidity);

}

//### DHT for nodemcu//
#include "DHT.h"

#define DHTPIN D5
#define DHTTYPE DHT11
float h,t;
DHT dht(DHTPIN,DHTTYPE);

void setup(){
  Serial.begin(115200);
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
