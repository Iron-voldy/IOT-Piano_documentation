# Introduction

The **IoT Piano LED Visualizer System** is designed to revolutionize piano learning by providing immediate visual feedback through LED lights, enhancing the learning process for beginners and advanced learners alike. By integrating IoT technology with music education, the system offers a fun, engaging, and interactive platform that helps learners understand musical notes and timing in real-time.

## Purpose of the Project

Learning to play the piano can be challenging, especially when it comes to understanding the timing and sequence of notes. Traditional methods of learning often lack immediate feedback, making it difficult for learners to identify mistakes and improve their technique. The **IoT Piano LED Visualizer System** addresses these challenges by offering:
- **Real-time visual feedback** using an RGB LED strip that lights up according to the notes being played.
- **An intuitive learning experience** with two modes: Tutorial Mode, which guides learners through songs, and Play Mode, where learners can practice independently.
- **Interactive data management**, allowing users to track their progress and improve their piano skills more effectively.

## Key Objectives

The system is designed to:
- **Provide visual feedback** in real-time by lighting up LEDs corresponding to the notes being played.
- **Display current notes and modes** on an LCD screen for easier learning.
- **Track and store user performance** in a database, providing insights and feedback to improve over time.
- **Allow users to toggle between Tutorial Mode and Play Mode**, offering flexibility in the learning experience.

## Project Goals

- **Interactive Learning**: Make piano learning more engaging by providing immediate visual feedback with an RGB LED strip.
- **Customization**: Allow users to input custom songs, notes, and durations for personalized practice.
- **Real-Time Feedback**: Offer instant feedback to help learners correct their mistakes as they practice.
- **User-Friendly Interface**: Ensure the system is easy to use with a web-based interface for controlling the song selection, modes, and playback.

## System Overview

The **IoT Piano LED Visualizer System** consists of three key components:

1. **Hardware Setup**:
   - **RGB LED Strip** connected to an ESP32 microcontroller for providing visual feedback.
   - **Push button sensors** to detect piano key presses.
   - **LCD display** to show the current note and mode.

2. **Web Interface**:
   - A responsive web-based frontend built with **Vite.js** and **Tailwind CSS**.
   - Features for entering musical notes, selecting songs, and controlling modes (Tutorial and Play Mode).

3. **Backend & Database**:
   - A **PHP**-based backend that handles user data, song input, and performance storage.
   - A **MySQL** database to store performance records, allowing users to track progress and access performance data.

---

## Benefits of the System

1. **Enhanced Learning**: Provides learners with immediate, interactive feedback, making it easier to learn piano.
2. **Customization**: Allows users to input custom songs, giving them the freedom to practice music they enjoy.
3. **Progress Tracking**: The system records and stores performance data, enabling learners to monitor their improvement over time.
4. **Flexible Learning Modes**: Offers both Tutorial Mode for guided learning and Play Mode for independent practice.

---

## Conclusion

The **IoT Piano LED Visualizer System** is a cutting-edge solution that enhances traditional piano learning by integrating visual feedback and real-time data tracking. By combining hardware automation with a web-based interface, the system creates an engaging, interactive learning environment that improves the efficiency and enjoyment of piano practice for learners of all levels.