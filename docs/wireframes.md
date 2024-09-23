# **Wireframes**

## **Wireframe 1: Add Song Page**
This page allows the learner to:
- **Select a song** from the available list.
- View the **current note** being played.
- **Start, pause, or reset** the song.
- View **performance data** after playing the song.

### **Layout Details**:

1. **Header**:
   - Title: “IoT Piano Visualizer”
   - Navigation Links: “Add Song” and “View Songs”
   - Mobile Menu (Hamburger icon for small screens)

2. **Main Content**:
   - **Song Selection Field**: A dropdown menu labeled “Select Song” where the learner chooses a song to practice.
   - **Note Display**: An area showing the current musical note being played, synced with the LED strip visualization.
   - **Action Buttons**:
     - "Start" button to begin playing the song.
     - "Pause" button to pause the song.
     - "Reset" button to reset the song to the beginning.

3. **Performance Table**: Displays the user’s performance details (song name, score, and timestamp) after each song, dynamically updated after each play session.

4. **Save Button**: Saves the performance data to the database.

**Add Song Page**:

![SongPage](img/song1.png)

**Song Selection Modal**:

![SongModal](img/song2.png)

**Performance Notification**:

![Performance](img/song3.png)

---

## **Wireframe 2: View Songs Page**
This page displays the list of all saved songs in the system, including the song name and duration, with data fetched from the server.

### **Layout Details**:

1. **Header**:
   - Title: “IoT Piano Visualizer”
   - Navigation Links: “Add Song” and “View Songs”

2. **Main Content**:
   - **Song List Table**:
     - A table with two columns: 
       - **Song Name**: Name of the song.
       - **Duration**: Length of the song in minutes and seconds.
     - Dynamically populated from the database with a list of saved songs.
   
   - **Scrollable Table**: Supports overflow for handling a large number of song entries.

3. **Buttons**:
   - Navigation links to other pages (e.g., back to Add Song page).

**View Songs Page**:

![ViewSongs](img/song4.png)

---

### **Explanation of Wireframes**

1. **Responsive Design**:
   - The layout is designed to be responsive, ensuring a seamless experience across devices of all sizes. This is achieved using **Tailwind CSS** for flexible design patterns.
   - For mobile users, the navigation collapses into a hamburger menu for better usability, while on larger screens, the full navigation menu remains visible.

2. **Modal Design** (for selecting songs):
   - When the user clicks the **Select Song** button on the "Add Song" page, a modal opens showing the list of available songs.
   - Inside the modal, learners can select a song or add a new one if necessary. Upon selecting a song, the modal closes, and the song is populated in the form for playback.
