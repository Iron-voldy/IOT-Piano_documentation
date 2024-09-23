# Test Cases for IoT Piano LED Visualizer System

Test cases are essential to ensure that the **IoT Piano LED Visualizer System** works as expected. Below are critical test cases covering various aspects of the system, including hardware, data flow, and frontend functionality.

## **Functional Test Cases**

### **Test Case 1: Play Notes and Visualize on LED Strip**
- **Description**: Ensure that the system correctly plays the selected notes and lights up the corresponding LEDs on the LED strip.
- **Preconditions**: The system is powered on, and a song is selected.
- **Test Steps**:
  1. Select a song in the web interface.
  2. Play the song in Play Mode.
- **Expected Result**: The LED strip should light up in sync with the notes being played, providing visual feedback.

---

### **Test Case 2: Toggle Between Tutorial and Play Mode**
- **Description**: Validate that switching between Tutorial Mode and Play Mode works correctly.
- **Preconditions**: A song is loaded, and the system is running.
- **Test Steps**:
  1. Select a song and start playing it in Tutorial Mode.
  2. Switch to Play Mode and continue the song.
- **Expected Result**: The system should smoothly switch between modes, and the LEDs should respond accordingly.

---

### **Test Case 3: Save User Performance Data**
- **Description**: Ensure that the user's performance data (song, score, mode) is saved correctly.
- **Preconditions**: The system is connected to Wi-Fi and the user has completed a song.
- **Test Steps**:
  1. Complete a song in either mode.
  2. Check the database or logs for saved performance data.
- **Expected Result**: The system should save the song, mode, and score into the database, and a confirmation should be shown.

---

### **Test Case 4: View Saved Performance Records**
- **Description**: Verify that the saved performance records are displayed correctly in the frontend.
- **Preconditions**: The database has stored performance data.
- **Test Steps**:
  1. Navigate to the "Performance" page.
  2. Check the performance records displayed.
- **Expected Result**: The table should display correct song names, scores, modes, and timestamps.

---

## **Error Handling Test Cases**

### **Test Case 5: Handle Missing Wi-Fi Connection**
- **Description**: Ensure that the system handles the absence of a Wi-Fi connection gracefully.
- **Preconditions**: The system is powered on without Wi-Fi connectivity.
- **Test Steps**:
  1. Power on the system with no Wi-Fi network available.
  2. Try to send performance data.
- **Expected Result**: The system should continuously try to reconnect to the Wi-Fi network and display an error message on the serial monitor or frontend.

---

### **Test Case 6: Handle Invalid Song Selection**
- **Description**: Verify that the system handles invalid or missing song selections gracefully.
- **Preconditions**: The song list is loaded, but no song is selected.
- **Test Steps**:
  1. Attempt to play without selecting a song.
  2. Monitor the system’s response.
- **Expected Result**: The system should display an error message indicating that a song must be selected.

---

### **Test Case 7: Invalid Note Value Handling**
- **Description**: Ensure that the system correctly handles invalid note values (e.g., notes outside the playable range).
- **Preconditions**: The system receives an invalid note value.
- **Test Steps**:
  1. Simulate sending an invalid note to the system.
  2. Try to play the song with invalid notes.
- **Expected Result**: The system should reject the invalid notes and display an error message.

---

## **Performance Test Cases**

### **Test Case 8: Time to Play Notes**
- **Description**: Measure how long it takes for the system to start playing a song after selecting it.
- **Preconditions**: The system is connected to Wi-Fi and functioning normally.
- **Test Steps**:
  1. Select a song and press play.
  2. Measure the time from selecting the song to the start of the LED display and audio output.
- **Expected Result**: The system should start playing the song within 1-2 seconds.

---

### **Test Case 9: Database Query Performance for Viewing Records**
- **Description**: Test how quickly the system retrieves performance records from the database.
- **Preconditions**: The database has a large number of saved records.
- **Test Steps**:
  1. Navigate to the "Performance" page.
  2. Measure the time taken to display the performance records.
- **Expected Result**: The records should be retrieved and displayed within a reasonable time frame.

---

## **User Interface (UI) Test Cases**

### **Test Case 10: Responsive Design of Frontend UI**
- **Description**: Ensure that the frontend is responsive and works well on different screen sizes.
- **Preconditions**: The frontend UI is deployed and accessible.
- **Test Steps**:
  1. Open the frontend on various devices (desktop, tablet, mobile).
  2. Check that the layout adjusts correctly on different screen sizes.
- **Expected Result**: The frontend should be fully responsive, with a usable layout on all device sizes.

---

## **Security Test Cases**

### **Test Case 11: Prevent SQL Injection**
- **Description**: Test that the system is protected against SQL injection attacks.
- **Preconditions**: The system should have a backend receiving performance data.
- **Test Steps**:
  1. Attempt to input malicious SQL code into the song or performance fields (e.g., `'; DROP TABLE performance_data; --`).
  2. Submit the form.
- **Expected Result**: The system should reject the input, and the database should remain unaffected.

---

## **Integration Test Cases**

### **Test Case 12: ESP32 to Backend Communication**
- **Description**: Ensure smooth communication between the ESP32 microcontroller and the backend server.
- **Preconditions**: The ESP32 and backend server are configured correctly.
- **Test Steps**:
  1. Play a song on the ESP32 and trigger data transmission.
  2. Check the backend server logs to ensure the data is received and processed.
- **Expected Result**: The performance data should be successfully transmitted to the backend without errors.

---

These test cases will help ensure that the **IoT Piano LED Visualizer System** operates as expected across its various functions, including note playback, performance tracking, UI responsiveness, and backend communication.