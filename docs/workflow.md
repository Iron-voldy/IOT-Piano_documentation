## User Workflow

1. **Learner Selects Song**: The learner selects a song from the list provided in the web interface.
2. **Song Playback with LED Visualization**: The system begins playing the selected song, and the corresponding notes are visualized using the RGB LED strip.
3. **Learner Performance**: As the learner follows along with the visual feedback, their performance (timing and accuracy) is tracked by the system.
4. **Performance Data Saving**: After the song is completed, the system saves the learner's performance data (song name, score, and mode) in the backend server's database.

---

## Data Workflow

- **Song Selection**: The learner selects a song from the available options stored in the database.
- **Performance Tracking**: The system tracks the learner's performance as they play the selected song, capturing timing and accuracy data.
- **Data Storage**: The learner's performance data (song name, score, and mode) is sent to the backend server via HTTP POST and stored in a MySQL database.
- **Data Retrieval**: The system retrieves the learner's past performance records from the database, which are displayed on the web interface for review.