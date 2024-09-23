# Debugging for IoT Piano LED Visualizer System

Debugging is a critical step in ensuring that the **IoT Piano LED Visualizer System** functions effectively by identifying and fixing issues within both the hardware and software components. Below are the key strategies and steps for effective debugging.

## **Common Debugging Issues**

### 1. **Wi-Fi Connection Issues**
   - **Symptoms**: The system fails to connect to the Wi-Fi network or loses the connection intermittently.
   - **Potential Causes**:
     - Incorrect Wi-Fi credentials.
     - Weak Wi-Fi signal strength.
     - Issues with the Wi-Fi module.
   - **Debugging Steps**:
     - Double-check the SSID and password for correctness.
     - Use the **Serial Monitor** to check connection status.
     - Position the system closer to the router to improve signal strength.
     - Add reconnection logic in the code to attempt reconnections if the connection is lost.

   **Example Code for Reconnection**:
   ```cpp
   if (WiFi.status() != WL_CONNECTED) {
       Serial.println("Reconnecting to WiFi...");
       WiFi.begin(ssid, password);
   }
   ```

### 2. **LED Feedback Not Working Properly**
   - **Symptoms**: The LED strip does not light up or shows the wrong colors when keys are pressed.
   - **Potential Causes**:
     - Incorrect wiring of the WS2812B LED strip.
     - Timing issues with the LED control code.
     - Power supply issues causing the LED strip to malfunction.
   - **Debugging Steps**:
     - Verify that the LED strip is correctly wired to the appropriate GPIO pin.
     - Use **Serial Monitor** to check if the correct commands are being sent.
     - Ensure the power supply is adequate for the number of LEDs used.

   **LED Control Code**:
   ```cpp
   strip.setPixelColor(keyNumber - 1, strip.Color(0, 150, 0));  // Green for key press
   strip.show();
   ```

### 3. **Failure to Send Key Press Data to Server**
   - **Symptoms**: The system is unable to send key press data to the server, or the server responds with an error.
   - **Potential Causes**:
     - Incorrect server URL or endpoint.
     - Network issues preventing the HTTP request from reaching the server.
     - Errors in the HTTP request format.
   - **Debugging Steps**:
     - Use the **Serial Monitor** to check HTTP error codes or server responses.
     - Confirm that the server URL is correct and accessible.
     - Add error handling to capture and retry failed requests.

   **Example Debug Code**:
   ```cpp
   int httpResponseCode = http.POST(payload);
   if (httpResponseCode > 0) {
       String response = http.getString();
       Serial.println("Server Response: " + response);
   } else {
       Serial.println("Error in sending POST request. HTTP Code: " + String(httpResponseCode));
   }
   ```

### 4. **Button Press Not Registered**
   - **Symptoms**: The system does not detect when a piano key (button) is pressed.
   - **Potential Causes**:
     - Incorrect wiring of the button.
     - Button debounce issues causing the system to register multiple presses.
   - **Debugging Steps**:
     - Ensure the button is wired correctly to the GPIO pin and ground.
     - Add a debounce mechanism in the code to prevent multiple registrations of the same press.

   **Example Debounce Code**:
   ```cpp
   if (digitalRead(BUTTON_PIN) == LOW) {
       delay(300);  // Debounce delay
       // Proceed with action
   }
   ```

### 5. **LCD Display Not Showing Data Correctly**
   - **Symptoms**: The LCD display shows garbled data, incorrect messages, or fails to display anything.
   - **Potential Causes**:
     - Incorrect I2C address or wiring of the LCD.
     - Errors in the code controlling the LCD.
   - **Debugging Steps**:
     - Verify that the I2C address and wiring match the specifications of the LCD.
     - Use **Serial Monitor** to check if the correct data is being sent to the LCD.

   **LCD Setup Code**:
   ```cpp
   lcd.init();
   lcd.backlight();
   lcd.setCursor(0, 0);
   lcd.print("IoT Piano System");
   ```

### 6. **Data Not Saved to the Database**
   - **Symptoms**: Data is sent to the server but does not appear in the database.
   - **Potential Causes**:
     - Server-side issues with the PHP script or database.
     - SQL errors preventing data from being inserted.
   - **Debugging Steps**:
     - Enable error reporting in the PHP script to catch any issues.
     - Log the SQL queries to check for errors.
     - Ensure the MySQL credentials are correct and the database table exists.

   **Example PHP Debugging Code**:
   ```php
   if ($stmt->execute()) {
       echo "Data recorded successfully";
   } else {
       echo "Error: " . $stmt->error;
   }
   ```

---

## **Tools for Debugging**

### 1. **Serial Monitor (Arduino IDE)**
   - Use the **Serial Monitor** to print out debug messages and monitor the program's flow.
   - Helpful for checking:
     - Wi-Fi connection status.
     - Button press detections.
     - LED and LCD behaviors.
     - HTTP request and server response details.

   **Example Serial Output**:
   ```cpp
   Serial.println("Connecting to WiFi...");
   Serial.println("Key Pressed: " + String(keyNumber));
   ```

### 2. **Server Logs**
   - Enable logging on the server to track incoming requests and database operations.
   - Useful for checking if the data is reaching the server and if there are any SQL errors.

### 3. **PHP Error Reporting**
   - Enable error reporting in PHP to catch and display server-side issues:
   ```php
   ini_set('display_errors', 1);
   error_reporting(E_ALL);
   ```

### 4. **Multimeter**
   - Use a **multimeter** to check the wiring and ensure proper voltages are supplied to the microcontroller, LED strip, and other components.

---

## **Debugging Workflow**

1. **Identify the Issue**:
   - Reproduce the issue consistently.
   - Document symptoms and potential causes.

2. **Check Logs and Outputs**:
   - Use the **Serial Monitor** or **server logs** to gather error messages.
   - Capture any relevant codes for further investigation.

3. **Isolate the Problem**:
   - Test individual components to isolate the issue (e.g., test the button separately, check Wi-Fi connections independently).

4. **Fix and Test**:
   - Apply the fix and test the system to ensure the issue is resolved.

5. **Document the Fix**:
   - Record the issue and fix for future reference.

---

## **Debugging Example: LED Feedback Issue**

### **Scenario**: The LED strip fails to provide visual feedback when a key is pressed.
1. **Symptom**: The LED strip does not light up when a key is pressed, but the button press is detected.
2. **Step-by-Step Debugging**:
   - **Check Wiring**: Ensure that the LED strip is wired correctly to the ESP32 and the power supply.
   - **Verify Code**: Use the **Serial Monitor** to confirm that the correct commands are being sent to the LED strip.

   **Example Debug Output**:
   ```cpp
   Serial.println("Key 1 Pressed: Lighting up LED 1");
   ```