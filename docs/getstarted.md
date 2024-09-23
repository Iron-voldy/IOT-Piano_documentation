# Get Started

Welcome to the **IoT Piano LED Visualizer System**. This guide will walk you through setting up the system, from configuring the hardware to deploying the web interface and backend. Follow the steps below to get started.

## 1. Hardware Setup

### Required Components:
- **Casio SA-45 Keyboard**
- **RGB LED Strip (WS2812B)**
- **ESP32 Microcontroller**
- **Push Button Sensors**
- **LCD 16x2 Display**

### Step-by-Step Guide:
1. **Assemble the Hardware**:
   - Connect the RGB LED strip to the ESP32 microcontroller.
   - Wire the push button sensors to the designated GPIO pins of the ESP32.
   - Wire the LCD display using the I2C interface.
   
2. **Connect the LED Strip**:
   - **Data Pin (DIN)** → ESP32 GPIO pin (e.g., D4)
   - **Power (5V) and Ground (GND)** connections to ESP32.

3. **Push Button and LCD Wiring**:
   - **Push Button Pins** → ESP32 GPIO pins (as per your configuration).
   - **LCD Display** connected to ESP32 via I2C.

4. **Power Up**: Once everything is connected, power on your ESP32.

### Testing the Hardware:
- Use basic Arduino sketches to test the LED strip, buttons, and LCD for proper functionality before proceeding with software setup.

---

## 2. Software Setup

### Prerequisites:
- **Node.js** (for frontend setup)
- **Vite.js** (for frontend development)
- **PHP** (for backend API)
- **MySQL** (for the database)

### Step 1: Frontend Setup

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-repo/iot-piano-visualizer.git
   ```

2. **Navigate to the Frontend Directory**:
   ```bash
   cd iot-piano-visualizer/frontend
   ```

3. **Install Dependencies**:
   ```bash
   npm install
   ```

4. **Run the Development Server**:
   ```bash
   npm run dev
   ```
   The application will be served at `http://localhost:3000`.

5. **Build for Production**:
   To create a production build, run:
   ```bash
   npm run build
   ```

### Step 2: Backend Setup

1. **Navigate to the Backend Directory**:
   ```bash
   cd iot-piano-visualizer/backend
   ```

2. **Configure the Database**:
   - Set up a MySQL database with the following structure:
     ```sql
     CREATE TABLE performance (
       id INT AUTO_INCREMENT PRIMARY KEY,
       song_name VARCHAR(255),
       score DECIMAL(5,2),
       timestamp DATETIME DEFAULT CURRENT_TIMESTAMP
     );
     ```

3. **Update the Database Credentials** in the `config.php` file:
   ```php
   $servername = "your_server";
   $dBUsername = "your_username";
   $dBPassword = "your_password";
   $dBName = "your_database_name";
   ```

4. **Run PHP Server**:
   If you're using a local server (e.g., XAMPP, MAMP):
   - Place the backend files in the `htdocs` or appropriate directory.
   - Ensure your server is running and the backend API is accessible.

---

## 3. Connecting Frontend and Backend

Once both the frontend and backend are running:

1. **Frontend API Configuration**:
   - Update the frontend configuration to point to your backend API.
   - Edit the `frontend/src/config.js` file to reflect your backend server URL:
     ```javascript
     export const API_BASE_URL = "http://localhost/your-backend-directory/";
     ```

2. **Testing the Connection**:
   - Navigate to the homepage in the frontend.
   - Test the "Play Song" and "Submit Notes" features, which should interact with the backend API.

---

## 4. First Use

### Step 1: Playing Notes
- Power on the system and connect to the web interface.
- Enter the song name, musical notes, and durations in the input fields.

### Step 2: Playing the Song
- Select the desired mode (Tutorial or Play Mode) and hit the "Play Selected Song" button to start the visual LED display.

### Step 3: Viewing Performance Data
- Once a session is complete, the performance data is saved and can be viewed on the **Performance** page in a graphical format.

---

## 5. Deploying the Project

### Frontend Deployment:
- Host the frontend build on a static file server such as **Netlify** or **Vercel**.
- Follow the deployment instructions for **Vite.js** projects.

### Backend Deployment:
- Deploy the PHP backend on any server that supports PHP (e.g., **Heroku**, **DigitalOcean**, or a shared hosting provider).
- Ensure the MySQL database is properly connected.

---

## 6. Troubleshooting

- **No LED Response**: Check the connections between the ESP32 and the LED strip and ensure the correct GPIO pins are used.
- **Frontend Not Connecting to Backend**: Ensure the correct API URL is set in the frontend configuration.
- **Database Connection Issues**: Verify that your database credentials are correct and the server is running.

---

Follow these steps to set up the **IoT Piano LED Visualizer System** and start using it. For further assistance, check the **Contact Us** page on the website.

---