# Frontend UI for IoT Piano LED Visualizer System

The frontend UI for the **IoT Piano LED Visualizer System** provides users with an interactive interface for managing their piano learning sessions. Built using **HTML**, **Tailwind CSS**, and **JavaScript**, the frontend is designed to be simple, responsive, and user-friendly. It allows users to input notes, manage sessions, and track their performance progress.

### Key Features of the Frontend:
1. **Home Page (Notes Management)**: Allows users to input musical notes and durations, select songs to play, and toggle between tutorial and play modes.
2. **Performance Page**: Displays recent performance records and provides graphical representations of progress.
3. **Login Page**: Allows users to sign in or create an account.
4. **About and Contact Pages**: Offers information about the project and provides users with the ability to contact support.

Below is the design and implementation of the frontend UI, extracted and adapted from the provided files.

---

## **Home Page (Notes Management)**

This page enables users to input musical notes and durations, select a song to play, and toggle between tutorial and play modes.

#### **HTML Code for Home Page**:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IoT Piano LED Visualizer - Notes Management</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 font-sans flex flex-col min-h-screen">
    <nav class="bg-indigo-600 text-white shadow-lg">
        <div class="container mx-auto px-4 py-3">
            <div class="flex justify-between items-center">
                <a href="index.html" class="font-bold text-xl">IoT Piano Visualizer</a>
                <div class="hidden md:flex space-x-4">
                    <a href="index.html" class="hover:text-indigo-200">Home</a>
                    <a href="performance.html" class="hover:text-indigo-200">Performance</a>
                    <a href="about.html" class="hover:text-indigo-200">About</a>
                    <a href="#" class="hover:text-indigo-200" onclick="logout();">Log Out</a>
                </div>
                <button id="mobile-menu-button" class="md:hidden focus:outline-none">
                    <i class="fas fa-bars"></i>
                </button>
            </div>
        </div>
    </nav>

    <main class="flex-grow container mx-auto mt-4 px-4">
        <!-- Notes and Durations Section -->
        <div class="bg-white rounded-lg shadow-md p-4 mb-4">
            <h2 class="text-xl font-semibold mb-2">Type Your Notes and Durations</h2>
            <input type="text" id="song-name" class="w-full p-2 mb-2 border rounded" placeholder="Enter song name">
            <textarea id="typed-notes" rows="4" class="w-full p-2 border rounded" placeholder="Type notes here"></textarea>
            <textarea id="typed-durations" rows="4" class="w-full p-2 border rounded" placeholder="Type durations here"></textarea>
            <button onclick="submitTypedNotes();" class="mt-4 w-full bg-indigo-500 text-white py-2 rounded">Submit Notes</button>
            <p id="note-feedback" class="mt-2 text-sm text-gray-600"></p>
        </div>

        <!-- Select Song to Play Section -->
        <div class="bg-white rounded-lg shadow-md p-4">
            <h2 class="text-xl font-semibold mb-2">Select Song to Play</h2>
            <select id="song-list" class="w-full p-2 border rounded mb-4"></select>
            <div class="flex space-x-4">
                <label class="inline-flex items-center">
                    <input type="radio" id="tutorial-mode" name="mode" value="tutorial" checked class="form-radio">
                    <span class="ml-2">Tutorial Mode</span>
                </label>
                <label class="inline-flex items-center">
                    <input type="radio" id="play-mode" name="mode" value="play" class="form-radio">
                    <span class="ml-2">Play Mode</span>
                </label>
            </div>
            <button onclick="playSong();" class="mt-4 bg-indigo-500 text-white py-2 px-4 rounded">Play Selected Song</button>
            <p id="playback-feedback" class="mt-4 text-sm text-gray-600"></p>
        </div>
    </main>

    <footer class="bg-gray-800 text-white py-4">
        <div class="container mx-auto text-center text-sm">
            <p>&copy; 2024 IoT Piano LED Visualizer. All rights reserved.</p>
        </div>
    </footer>
</body>
</html>
```

### **Explanation**:
- **Song Name and Notes Input**: Allows the user to input the song's name, musical notes, and durations.
- **Mode Selection**: Users can toggle between Tutorial Mode and Play Mode.
- **Play Song**: Users can select a song from the list and play it.

---

## **Performance Page**

This page provides users with an overview of their recent performance and displays a graphical representation of their progress.

#### **HTML Code for Performance Page**:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IoT Piano LED Visualizer - Performance</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 font-sans flex flex-col min-h-screen">
    <nav class="bg-indigo-600 text-white shadow-lg">
        <div class="container mx-auto px-4 py-3">
            <div class="flex justify-between items-center">
                <a href="index.html" class="font-bold text-xl">IoT Piano Visualizer</a>
                <div class="hidden md:flex space-x-4">
                    <a href="index.html" class="hover:text-indigo-200">Home</a>
                    <a href="performance.html" class="hover:text-indigo-200">Performance</a>
                    <a href="about.html" class="hover:text-indigo-200">About</a>
                    <a href="#" class="hover:text-indigo-200" onclick="logout();">Log Out</a>
                </div>
                <button id="mobile-menu-button" class="md:hidden focus:outline-none">
                    <i class="fas fa-bars"></i>
                </button>
            </div>
        </div>
    </nav>

    <main class="flex-grow container mx-auto mt-4 px-4">
        <!-- Performance Overview -->
        <section class="bg-white rounded-lg shadow-md p-4 mb-4">
            <h2 class="text-xl font-semibold mb-2">Performance Overview</h2>
            <div class="overflow-x-auto">
                <table class="w-full text-sm">
                    <thead class="bg-gray-200 text-gray-600">
                        <tr>
                            <th class="py-2 px-3 text-left">Date</th>
                            <th class="py-2 px-3 text-left">Song</th>
                            <th class="py-2 px-3 text-left">Score</th>
                            <th class="py-2 px-3 text-left">Mode</th>
                        </tr>
                    </thead>
                    <tbody id="performance-data" class="text-gray-600">
                        <!-- Dynamic Data Loading -->
                    </tbody>
                </table>
            </div>
        </section>

        <!-- Performance Graph -->
        <section class="bg-white rounded-lg shadow-md p-4">
            <h2 class="text-xl font-semibold mb-2">Performance Graph</h2>
            <canvas id="performanceChart" class="w-full h-64"></canvas>
        </section>
    </main>

    <footer class="bg-gray-800 text-white py-4">
        <div class="container mx-auto text-center text-sm">
            <p>&copy; 2024 IoT Piano LED Visualizer. All rights reserved.</p>
        </div>
    </footer>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</body>
</html>
```

### **Explanation**:
- **Performance Table**: Displays performance data such as date, song, score, and mode.
- **Performance Graph**: Uses **Chart.js** to provide a graphical view of the user's progress over time.

---

## **Login Page**

The login page allows users to sign in to the system or create an account.

#### **HTML Code for Login Page**:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>IoT Piano Visualizer</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gradient-to-r from-primary to-secondary min-h

-screen flex flex-col justify-center items-center p-4">
    <div class="max-w-md w-full space-y-8 bg-white p-6 sm:p-10 rounded-xl shadow-lg">
        <div class="text-center">
            <h2 class="mt-6 text-3xl font-extrabold text-gray-900">IoT Piano Visualizer</h2>
            <p class="mt-2 text-sm text-gray-600">Sign in or create an account</p>
        </div>
        <div class="flex justify-center space-x-4 mb-6">
            <button class="text-gray-600 pb-2 border-b-2 hover:border-primary" onclick="toggleForm('login')">Login</button>
            <button class="text-gray-600 pb-2 border-b-2 hover:border-primary" onclick="toggleForm('signup')">Sign Up</button>
        </div>
        <form id="loginForm" class="space-y-6">
            <div class="rounded-md shadow-sm space-y-4">
                <input id="email-address" type="email" class="w-full px-3 py-3 border rounded" placeholder="Email address" required>
                <input id="password" type="password" class="w-full px-3 py-3 border rounded" placeholder="Password" required>
            </div>
            <button type="submit" class="w-full bg-primary py-3 text-white rounded">Sign in</button>
        </form>
    </div>
</body>
</html>
```

### **Explanation**:
- **Login Form**: A simple login form where users can enter their email and password to sign in.

---

### **Summary of the Frontend**

The frontend of the **IoT Piano LED Visualizer** system offers an interactive, user-friendly platform that enables users to manage their piano learning sessions, track performance, and more.