# PHP Scripts

## Script for Saving Played Songs (save_played_song.php)

This PHP script receives data about the song that has been played, including the song ID and mode (Tutorial or Play), and stores it in the `played_songs` table. Additionally, it updates a flag to signal new data availability.

#### **Functional Overview**:
- Receives the `song_id` and `mode` via POST request.
- Saves the song details in the `played_songs` table.
- Updates a flag in the `fetch_flag` table to signal new data.

### **PHP Code**:

```php
<?php
// Enable error reporting for debugging
ini_set('display_errors', 1);
ini_set('display_startup_errors', 1);
error_reporting(E_ALL);

// Set CORS headers
header("Access-Control-Allow-Origin: *");
header("Access-Control-Allow-Methods: POST");
header("Access-Control-Allow-Headers: Content-Type");

// Database connection parameters
$servername = "localhost";
$dBUsername = "root";
$dBPassword = "";
$dBName = "piano_system_db";

// Create connection to MySQL
$conn = new mysqli($servername, $dBUsername, $dBPassword, $dBName);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Check if song data is received via POST request
if (isset($_POST['song_id']) && isset($_POST['mode'])) {
    $song_id = intval($_POST['song_id']);
    $mode = $_POST['mode'];

    // Prepare the SQL query
    $stmt = $conn->prepare("INSERT INTO played_songs (song_id, mode, timestamp) VALUES (?, ?, NOW())");
    $stmt->bind_param("is", $song_id, $mode);

    // Execute the query
    if ($stmt->execute()) {
        // Update the flag in the fetch_flag table
        $conn->query("UPDATE fetch_flag SET flag = 1 WHERE id = 1");

        echo "Song played data saved successfully";
    } else {
        echo "Error: " . $stmt->error;
    }

    // Close the statement
    $stmt->close();
} else {
    echo "No song data received";
}

// Close the connection
$conn->close();
?>
```

---

### **Explanation**:

1. **Error Reporting**: 
   - Debugging is enabled for development purposes using `ini_set()` and `error_reporting()`.

2. **CORS Headers**: 
   - Allows cross-origin requests from any domain and accepts POST requests.

3. **Database Connection**: 
   - The script establishes a connection to the MySQL database.

4. **POST Request Handling**: 
   - The script checks if `song_id` and `mode` are received via POST request and processes the data.

5. **Prepared Statement**: 
   - A prepared statement is used to securely insert the song's play data into the `played_songs` table, preventing SQL injection.

6. **Update Fetch Flag**: 
   - After the song data is saved, the fetch flag is updated in the `fetch_flag` table to signal that new data is available.

7. **Response**: 
   - Success and error messages are returned based on the result of the data insertion.

---

## Script for Saving Performance Data (save_performance.php)

This script saves the user's performance data after a song has been played, including the song name, score, and mode (Tutorial or Play), to the `performance_data` table.

#### **Functional Overview**:
- Receives the song name, score, and mode from the frontend.
- Inserts this performance data into the `performance_data` table.

### **PHP Code**:

```php
<?php
// Enable error reporting for debugging
ini_set('display_errors', 1);
ini_set('display_startup_errors', 1);
error_reporting(E_ALL);

// Set CORS headers
header("Access-Control-Allow-Origin: *");
header("Access-Control-Allow-Methods: POST");
header("Access-Control-Allow-Headers: Content-Type");

// Database connection parameters
$servername = "localhost";
$dBUsername = "root";
$dBPassword = "";
$dBName = "piano_system_db";

// Create connection to MySQL
$conn = new mysqli($servername, $dBUsername, $dBPassword, $dBName);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Check if performance data is received via POST request
if (isset($_POST['song_name']) && isset($_POST['score']) && isset($_POST['mode'])) {
    $song_name = $_POST['song_name'];
    $score = floatval($_POST['score']);
    $mode = $_POST['mode'];

    // Prepare the SQL query
    $stmt = $conn->prepare("INSERT INTO performance_data (song_name, score, mode, timestamp) VALUES (?, ?, ?, NOW())");
    $stmt->bind_param("sds", $song_name, $score, $mode);

    // Execute the query
    if ($stmt->execute()) {
        echo "Performance data saved successfully";
    } else {
        echo "Error: " . $stmt->error;
    }

    // Close the statement
    $stmt->close();
} else {
    echo "No performance data received";
}

// Close the connection
$conn->close();
?>
```

---

### **Explanation**:

1. **POST Data**: 
   - Receives the `song_name`, `score`, and `mode` from the frontend after a song is played.

2. **Prepared Statement**: 
   - A prepared statement is used to securely insert performance data into the `performance_data` table.

3. **Response**: 
   - Returns success or error messages based on the result of the data insertion.

---

## Script for Fetching Performance Data (get_performance_data.php)

This script retrieves all saved performance data from the `performance_data` table and sends it back as a JSON response.

#### **Functional Overview**:
- Retrieves all performance data, including song name, score, and mode.
- Returns the data in JSON format.

### **PHP Code**:

```php
<?php
// Enable error reporting for debugging
ini_set('display_errors', 1);
ini_set('display_startup_errors', 1);
error_reporting(E_ALL);

// Set CORS headers
header("Access-Control-Allow-Origin: *");
header("Content-Type: application/json; charset=UTF-8");

// Database connection parameters
$servername = "localhost";
$dBUsername = "root";
$dBPassword = "";
$dBName = "piano_system_db";

// Create connection to MySQL
$conn = new mysqli($servername, $dBUsername, $dBPassword, $dBName);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Retrieve performance data
$sql = "SELECT song_name, score, mode, timestamp FROM performance_data ORDER BY timestamp DESC";
$result = $conn->query($sql);

// Prepare data for JSON response
$performanceData = array();
if ($result->num_rows > 0) {
    while($row = $result->fetch_assoc()) {
        $performanceData[] = $row;
    }
}

// Output the data in JSON format
echo json_encode($performanceData);

// Close the connection
$conn->close();
?>
```

---

### **Explanation**:

1. **Data Retrieval**: 
   - Fetches all performance data from the `performance_data` table, ordered by timestamp.

2. **JSON Response**: 
   - Returns the fetched data as a JSON response, which is then used by the frontend to display user performance.

---

## Script for Fetching Songs (get_songs.php)

This script retrieves the list of available songs from the `songs` table and sends it back as a JSON response.

#### **Functional Overview**:
- Retrieves all songs from the `songs` table.
- Returns the song names and IDs in JSON format.

### **PHP Code**:

```php
<?php
// Enable error reporting for debugging
ini_set('display_errors', 1);
ini_set('display_startup_errors', 1);
error_reporting(E_ALL);

// Set CORS headers
header("Access-Control-Allow-Origin: *");
header("Content-Type: application/json; charset=UTF-8");

// Database connection parameters
$servername = "localhost";
$dBUsername = "root";
$dBPassword = "";
$dBName = "piano_system_db";

// Create connection to MySQL
$conn = new mysqli($servername, $dBUsername, $dBPassword, $dBName);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Retrieve songs
$sql = "SELECT id, song_name FROM songs ORDER BY song_name ASC";
$result = $conn->query($sql);

// Prepare data for JSON response
$songData = array();
if ($result->num_rows > 0) {
    while($row = $result->fetch_assoc()) {
        $songData[] = $row;
    }
}

// Output the data in JSON format
echo json_encode($songData);

// Close the connection
$conn->close();
?>
```

---

### **Explanation**:

1. **Data Retrieval**: 
   - Retrieves the list of all available songs from the `songs` table.

2. **JSON Response**: 
   - Returns the song data (song name and ID) as a JSON response for the frontend to display in the song selection list.

---

This structure should now provide a clear overview of how

 each PHP script integrates into the **IoT Piano LED Visualizer System** for song management, performance tracking, and status monitoring.