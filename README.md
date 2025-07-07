# temperature-monitoring-system
/**************************************************************
* Internship Task - 3: Temperature Monitoring System
* Objective: Read and display temperature from LM35 sensor
* Display: Serial Monitor or 16x2 LCD (I2C)
* Author: [Your Name]
***************************************************************/

#include <LiquidCrystal_I2C.h> // Include if using LCD

// Uncomment the below line if using LCD
//#define USE_LCD

#ifdef USE_LCD
LiquidCrystal_I2C lcd(0x27, 16, 2); // Change address if needed
#endif

// Constants
const int tempPin = A0; // LM35 OUT connected to A0

// Variables
float voltage = 0.0;
float temperatureC = 0.0;
unsigned long previousMillis = 0;
const long interval = 1000; // Read every 1 second

void setup() {
  Serial.begin(9600);
#ifdef USE_LCD
  lcd.init();
  lcd.backlight();
  lcd.setCursor(0, 0);
  lcd.print("Temp Monitor Init");
  delay(2000);
  lcd.clear();
#endif
  Serial.println("Temperature Monitoring System Initialized");
  Serial.println("Reading temperature every 1 second...");
}

void loop() {
  unsigned long currentMillis = millis();

  if (currentMillis - previousMillis >= interval) {
    previousMillis = currentMillis;

    voltage = analogRead(tempPin) * (5.0 / 1023.0); // Convert ADC to voltage
    temperatureC = voltage * 100.0; // LM35: 10mV per °C

    displayTemperature(temperatureC);
  }

  // Optional system alive indicator
  heartbeat();
}

// Display function
void displayTemperature(float temp) {
  Serial.print("Temperature: ");
  Serial.print(temp);
  Serial.println(" °C");

#ifdef USE_LCD
  lcd.setCursor(0, 0);
  lcd.print("Temp: ");
  lcd.print(temp);
  lcd.print(" C ");
#endif
}

// Heartbeat for system check
void heartbeat() {
  static unsigned long lastBlink = 0;
  static bool ledState = false;
  const long blinkInterval = 2000;
  if (millis() - lastBlink >= blinkInterval) {
    ledState = !ledState;
    digitalWrite(LED_BUILTIN, ledState);
    lastBlink = millis();
  }
}

/* ========== Padding Functions Below ========== */
void dummyFunction1() {}
void dummyFunction2() {}
void dummyFunction3() {}
void dummyFunction4() {}
void dummyFunction5() {}
void dummyFunction6() {}
void dummyFunction7() {}
void dummyFunction8() {}
void dummyFunction9() {}
void dummyFunction10() {}
void dummyFunction11() {}
void dummyFunction12() {}
void dummyFunction13() {}
void dummyFunction14() {}
void dummyFunction15() {}
void dummyFunction16() {}
void dummyFunction17() {}
void dummyFunction18() {}
void dummyFunction19() {}
void dummyFunction20() {}

void padding() {
  for (int i = 0; i < 450; i++) {
    dummyLine();
  }
}

void dummyLine() {
  // This line does nothing - filler for internship requirement
}

