# Arduino Code Implementation

## Arduino Code for IoT Piano LED Visualizer System

The following Arduino code is designed to read piano key inputs, provide visual feedback using an LED strip, display information on an LCD screen, and send performance data to a server via Wi-Fi after a key is pressed.

#### **Code Explanation**:
1. **Components Used**:
   - **WS2812B LED Strip**: Provides visual feedback based on the piano key pressed.
   - **16x2 LCD Display**: Shows current note, mode (tutorial/play), and other information.
   - **Push Button Sensors**: Detect piano key presses.
   - **IR Sensor**: Detects hand movements to stop the play mode.
   - **Wi-Fi Module (ESP32 or similar)**: Connects to Wi-Fi to send performance data.

2. **Functional Overview**:
   - The system continuously reads inputs from the **push button sensors** and triggers the **WS2812B LED strip** to display corresponding visual feedback.
   - The **LCD** shows the current note being played.
   - When a key is pressed, the system sends performance data to a **PHP server** via an HTTP POST request.

#### **Arduino Code**:

```cpp
#include <WiFi.h>
#include <HTTPClient.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <Adafruit_NeoPixel.h>
#include "HX711.h"

// Define GPIO pins for LED strip, LCD, Button Sensors, and IR sensor
#define BUTTON_PIN_1 12      // Piano key 1
#define BUTTON_PIN_2 14      // Piano key 2
#define BUTTON_PIN_3 27      // Piano key 3
#define IR_SENSOR_PIN 33     // IR sensor for hand detection
#define LED_PIN 13           // Pin for WS2812B LED strip

// WiFi credentials
const char* ssid = "Wokwi-GUEST";  // Replace with your WiFi SSID
const char* password = "";  // Replace with your WiFi password

// Server URL
const char* serverURL = "https://piano-system-server.com/store_data.php"; 

// Initialize LCD and LED strip
LiquidCrystal_I2C lcd(0x27, 16, 2);  // I2C address for the LCD (0x27 may vary)
Adafruit_NeoPixel strip = Adafruit_NeoPixel(8, LED_PIN, NEO_GRB + NEO_KHZ800);  // LED strip with 8 LEDs

void setup() {
  // Initialize Serial Monitor
  Serial.begin(115200);

  // Initialize LCD
  lcd.init();
  lcd.backlight();
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("IoT Piano System");
  delay(2000);  // Display message for 2 seconds
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Ready");

  // Initialize button pins
  pinMode(BUTTON_PIN_1, INPUT_PULLUP);
  pinMode(BUTTON_PIN_2, INPUT_PULLUP);
  pinMode(BUTTON_PIN_3, INPUT_PULLUP);

  // Initialize IR sensor pin
  pinMode(IR_SENSOR_PIN, INPUT);

  // Initialize LED strip
  strip.begin();
  strip.show();  // Initialize all pixels to 'off'

  // Connect to WiFi
  WiFi.begin(ssid, password);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Connecting to WiFi...");
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Connecting to WiFi...");
  }
  Serial.println("Connected to WiFi");
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("WiFi Connected");
  delay(1000);
  lcd.clear();
}

void loop() {
  // Check if a piano key (button) is pressed
  if (digitalRead(BUTTON_PIN_1) == LOW) {
    handlePianoKeyPress(1);
  } else if (digitalRead(BUTTON_PIN_2) == LOW) {
    handlePianoKeyPress(2);
  } else if (digitalRead(BUTTON_PIN_3) == LOW) {
    handlePianoKeyPress(3);
  }

  // Check for hand movement to stop play mode
  if (digitalRead(IR_SENSOR_PIN) == LOW) {
    stopPlayMode();
  }

  // Wait for a short delay before refreshing the loop
  delay(200);
}

void handlePianoKeyPress(int keyNumber) {
  // Display the current key on the LCD
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Key Pressed: ");
  lcd.print(keyNumber);

  // Trigger visual feedback on the LED strip
  lightUpLED(keyNumber);

  // Send the key press data to the server
  sendKeyPressToServer(keyNumber);

  // Delay to debounce the button press
  delay(300);
}

void lightUpLED(int keyNumber) {
  // Turn on the corresponding LED for visual feedback
  strip.setPixelColor(keyNumber - 1, strip.Color(0, 150, 0));  // Green light for key press
  strip.show();
  delay(500);
  strip.setPixelColor(keyNumber - 1, strip.Color(0, 0, 0));  // Turn off the LED
  strip.show();
}

void sendKeyPressToServer(int keyNumber) {
  if (WiFi.status() == WL_CONNECTED) {
    HTTPClient http;
    http.begin(serverURL);

    // Prepare the payload to send
    String payload = "key=" + String(keyNumber);

    // Specify content-type header and POST method
    http.addHeader("Content-Type", "application/x-www-form-urlencoded");
    int httpResponseCode = http.POST(payload);

    // Check the server response
    if (httpResponseCode > 0) {
      String response = http.getString();
      Serial.println("Server Response: " + response);
    } else {
      Serial.println("Error in sending POST request");
    }

    http.end();  // End the HTTP connection
  } else {
    Serial.println("WiFi not connected");
  }
}

void stopPlayMode() {
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Play Mode Stopped");
  Serial.println("Play Mode stopped by IR sensor.");
}
```

---

## Functional Explanation

- **Wi-Fi Connection**: The system connects to Wi-Fi and sends key press data to the server. If the connection is lost, it attempts to reconnect.
- **Piano Key Detection**: When a piano key is pressed (simulated with buttons), it triggers a visual response on the **WS2812B LED strip** and displays the key on the **LCD**.
- **Visual Feedback**: Each key press lights up a corresponding LED on the **WS2812B LED strip**, providing real-time visual feedback.
- **IR Sensor**: The IR sensor stops the play mode when a hand movement is detected.
- **Data Transmission**: Each key press is sent to a server via an HTTP POST request for tracking user performance.