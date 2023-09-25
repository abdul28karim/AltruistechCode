# AltruistechCode
Climate Tech &amp; Environmental Conservation Awareness: Public Accountability by Enhancing Compliance Information Sharing through Robotics and Beaming Light Technology in Rwanda
#include "thingProperties.h"
#include "DHT.h"
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SH110X.h>

#define CO2_MIN 0
#define CO2_MAX 1023
#define CO2_PPM_MIN 400
#define CO2_PPM_MAX 5000
#define i2c_Address 0x3c // Initialize with the I2C addr 0x3C (eBay OLED's)
#define SCREEN_WIDTH 128 // OLED display width, in pixels
#define SCREEN_HEIGHT 64 // OLED display height, in pixels
#define OLED_RESET -1    // QT-PY / XIAO

#define DHTTYPE DHT11   // DHT 11
#define DHTPIN 3
#define CO2_ANALOG_PIN A0
#define airQualitySensor A1
#define sensorSound A3 // Analog input pin that the Sensor is attached to



int redLed = 4;
int greenLed = 7;
int blueLed = 8;
int airQualityValue;
int displayVal;
int displayCO2;
int co2Concentration;
float temperatureValue;
float humidityValue;
int soundValue;
int temperatureVal;
int humidityVal;

DHT dht(DHTPIN, DHTTYPE);
Adafruit_SH1106G display = Adafruit_SH1106G(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);


void setup() {
  Serial.begin(9600);
  delay(1500);

  initProperties();
  dht.begin();
  ArduinoCloud.begin(ArduinoIoTPreferredConnection);
  setDebugMessageLevel(2);
  ArduinoCloud.printDebugInfo();


  pinMode(sensorSound, INPUT);
  pinMode(redLed, OUTPUT);
  pinMode(greenLed, OUTPUT);
  pinMode(blueLed, OUTPUT);

  //setting up OLED display
  display.begin(i2c_Address, true);
  display.clearDisplay();
  display.setTextSize(1.4);
  display.setTextColor(SH110X_WHITE);
  display.setCursor(0, 0);
}

int def_airQuality() {
  airQualityValue = analogRead(airQualitySensor);
  if (airQualityValue >= 1 && airQualityValue <= 150) {
    displayVal = 1;
  }
  else if (airQualityValue >= 151 && airQualityValue <= 250) {
    displayVal = 2;

  }
  else if (airQualityValue >= 251 && airQualityValue <= 350) {
    displayVal = 3;
  }
  else if (airQualityValue >= 351 && airQualityValue <= 450) {
    displayVal = 4;
  }
  else if (airQualityValue >= 451 && airQualityValue <= 600) {
    displayVal = 5;
  }
  else if (airQualityValue >= 601 && airQualityValue <= 750) {
    displayVal = 6;
  }
  else if (airQualityValue >= 751 && airQualityValue <= 850) {
    displayVal = 7;
  }
  else if (airQualityValue >= 851 && airQualityValue <= 950) {
    displayVal = 8;
  }
  else if (airQualityValue >= 951 && airQualityValue <= 1200) {
    displayVal = 9;
  }
  else if (airQualityValue >= 1200) {
    displayVal = 10;
  }
  return displayVal;
}

int def_co2Concentration() {
  int co2Value = analogRead(CO2_ANALOG_PIN);
  co2Concentration = map(co2Value, CO2_MIN, CO2_MAX, CO2_PPM_MIN, CO2_PPM_MAX);

  if (co2Concentration >= 1 && co2Concentration <= 150) {
    displayCO2 = 1;
  }
  else if (co2Concentration >= 151 && co2Concentration <= 250) {
    displayCO2 = 2;

  }
  else if (co2Concentration >= 251 && co2Concentration <= 350) {
    displayCO2 = 3;
  }
  else if (co2Concentration >= 351 && co2Concentration <= 450) {
    displayCO2 = 4;
  }
  else if (co2Concentration >= 451 && co2Concentration <= 600) {
    displayCO2 = 5;
  }
  else if (co2Concentration >= 601 && co2Concentration <= 750) {
    displayCO2 = 6;
  }
  else if (co2Concentration >= 751 && co2Concentration <= 850) {
    displayCO2 = 7;
  }
  else if (co2Concentration >= 851 && co2Concentration <= 950) {
    displayCO2 = 8;
  }
  else if (co2Concentration >= 951 && co2Concentration <= 1200) {
    displayCO2 = 9;
  }
  else if (co2Concentration >= 1200) {
    displayCO2 = 10;
  }
  return displayCO2;
}

int def_sound() {
  soundValue = analogRead(sensorSound);

  if (soundValue >= 1 && soundValue <= 30) {
    sound = 1;
  }
  else if (soundValue >= 31 && soundValue <= 60) {
    sound = 2;

  }
  else if (soundValue >= 61 && soundValue <= 90) {
    sound = 3;
  }
  else if (soundValue >= 91 && soundValue <= 120) {
    sound = 4;
  }
  else if (soundValue >= 121 && soundValue <= 150) {
    sound = 5;
  }
  else if (soundValue >= 151 && soundValue <= 180) {
    sound = 6;
  }
  else if (soundValue >= 181 && soundValue <= 210) {
    sound = 7;
  }
  else if (soundValue >= 211 && soundValue <= 240) {
    sound = 8;
  }
  else if (soundValue >= 241 && soundValue <= 270) {
    sound = 9;
  }
  else if (soundValue >= 271) {
    sound = 10;
  }
  return sound;
}

int def_temperature() {
  temperatureValue = dht.readTemperature();
  if (temperatureValue >= 1 && temperatureValue <= 10) {
    temperatureVal = 1;
  }
  else if (temperatureValue >= 11 && temperatureValue <= 20) {
    temperatureVal = 2;

  }
  else if (temperatureValue >= 21 && temperatureValue <= 30) {
    temperatureVal = 3;
  }
  else if (temperatureValue >= 31 && temperatureValue <= 40) {
    temperatureVal = 4;
  }
  else if (temperatureValue >= 41 && temperatureValue <= 50) {
    temperatureVal = 5;
  }
  else if (temperatureValue >= 51 && temperatureValue <= 60) {
    temperatureVal = 6;
  }
  else if (temperatureValue >= 61 && temperatureValue <= 70) {
    temperatureVal = 7;
  }
  else if (temperatureValue >= 71 && temperatureValue <= 80) {
    temperatureVal = 8;
  }
  else if (temperatureValue >= 81 && temperatureValue <= 90) {
    temperatureVal = 9;
  }
  else if (temperatureValue >= 91) {
    temperatureVal = 10;
  }
  return temperatureVal;
}

int def_humidity() {
  humidityValue = dht.readHumidity();

  if (humidityValue >= 1 && humidityValue <= 10) {
    humidityVal = 1;
  }
  else if (humidityValue >= 11 && humidityValue <= 20) {
    humidityVal = 2;

  }
  else if (humidityValue >= 21 && humidityValue <= 30) {
    humidityVal = 3;
  }
  else if (humidityValue >= 31 && humidityValue <= 40) {
    humidityVal = 4;
  }
  else if (humidityValue >= 41 && humidityValue <= 50) {
    humidityVal = 5;
  }
  else if (humidityValue >= 51 && humidityValue <= 60) {
    humidityVal = 6;
  }
  else if (humidityValue >= 61 && humidityValue <= 70) {
    humidityVal = 7;
  }
  else if (humidityValue >= 71 && humidityValue <= 80) {
    humidityVal = 8;
  }
  else if (humidityValue >= 81 && humidityValue <= 90) {
    humidityVal = 9;
  }
  else if (humidityValue >= 91) {
    humidityVal = 10;
  }
  return humidityVal;
}

void loop() {
  ArduinoCloud.update();
  

  displayVal = def_airQuality();
  Serial.print("Air Quality: ");
  Serial.print( displayVal);
  Serial.println(" ppm");


  displayCO2 = def_co2Concentration();
  Serial.print("CO2 Concentration: ");
  Serial.print(displayCO2);
  Serial.println(" ppm");

  sound = def_sound();
  Serial.print("Sound value: ");
  Serial.println(sound);

  temperature = def_temperature();
  Serial.print("Temperature: ");
  Serial.println(temperature);

  humidity = def_humidity();
  Serial.print("Humidity: ");
  Serial.println(humidity);
  
  
  int industrial_waste = (humidity + temperature) / 2;
  int sum_val = displayCO2 + displayVal + industrial_waste + sound;
  int avg_val = sum_val / 4;
  displayData(displayCO2, displayVal, humidity, temperature, sound, avg_val);
  LedLightsControl(avg_val);

  delay(1000);
}



// Function to display data on the OLED display
void displayData(int co2, int airQuality, int humidity, int temperature, int sound, int scale) {
  display.clearDisplay();
  display.setCursor(0, 0);
  display.println("--Air Monitoring--");

  display.print(" Compliance Scale: ");
  display.println(scale);
  
  display.println();
  display.print("CO2:         ");
  display.println(co2);
  display.print("Air Quality: ");
  display.println(airQuality);
  display.print("Humidity:    ");
  display.println(humidity);
  display.print("Temperature: ");
  display.println(temperature);
  display.print("Noise:       ");
  display.println(sound);
  display.display();
  
}

void LedLightsControl(int avg_val) {
  
  if (avg_val >= 1 && avg_val <= 4) {
    digitalWrite(greenLed, HIGH);
    digitalWrite(redLed, LOW);
    digitalWrite(blueLed, LOW);
  }
  
  else if (avg_val >= 5 && avg_val <= 7) {
    digitalWrite(blueLed, HIGH);
    digitalWrite(greenLed, LOW);
    digitalWrite(redLed, LOW);
  }
  
  else if (avg_val >= 8 && avg_val <= 10) {
    digitalWrite(redLed, HIGH);
    digitalWrite(greenLed, LOW);
    digitalWrite(blueLed, LOW);
  }
}

void onHumidityChange(){
  //code here
}
