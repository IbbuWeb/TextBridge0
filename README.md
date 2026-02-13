# TextBridge
TextBridge is a minimalist, real-time text synchronization tool designed to bridge the gap between devices. It provides a seamless "universal clipboard" experience, allowing users to type text on one device and instantly see it appear on another. Built as a Progressive Web App (PWA), TextBridge is installable, works offline, and offers a native-app-like experience directly from the browser.

The Problem
In a multi-device world, users often struggle to move small pieces of text between their phone, tablet, and computer. Traditional methods involve emailing oneself, using messy note-taking apps, or relying on platform-specific ecosystems (like Apple's copy/paste). TextBridge solves this by providing a single, shared text space accessible from any modern browser.

Key Features
Real-Time Synchronization: Powered by Firebase Realtime Database, every keystroke is synchronized instantly across all connected devices (tabs, phones, computers) with near-zero latency.
Smart Cursor Management: The app intelligently detects if a user is currently editing. It suppresses incoming updates while the user is typing to prevent the cursor from "jumping" to the end of the text, ensuring a smooth typing experience.
Progressive Web App (PWA):
Installable: Users can install TextBridge on their home screen or desktop.
Offline Support: Utilizes a Service Worker to cache the app shell, ensuring the interface loads instantly even without an internet connection.
Local Persistence: The app uses localStorage to save text locally. If a user closes the tab or refreshes, their text remains on the screen.
Modern UI/UX:
Theme Toggle: Supports a beautiful Light and Dark mode, respecting user preference and system settings.
QR Code Integration: A built-in QR code generator allows users to quickly open the app on a mobile device by scanning the code from a desktop screen.
Minimalist Design: Built with the Inter font family and a focus on whitespace, the interface is distraction-free.
Tech Stack
Frontend: HTML5, CSS3, JavaScript (ES Modules)
Backend/Database: Google Firebase Realtime Database
PWA: Web App Manifest, Service Workers (sw.js)
Libraries:
QRCode.js for generating QR codes.
Google Fonts (Inter).
How It Works
Data Flow: When a user types, the input event listener captures the text and sends it to a shared node in the Firebase Realtime Database.
Subscriptions: All open instances of the app subscribe to that database node using onValue.
Conflict Resolution: When new data arrives from the database, the app checks if the text area is currently focused (document.activeElement). If it is, the update is ignored to prevent interrupting the user; otherwise, the text area updates with the new content.
Offline Handling: If the app is opened offline, the Service Worker serves the cached HTML/CSS, and localStorage restores the last known text state.
Installation & Setup
To run this project locally or deploy your own version:

Clone the repository.
Firebase Setup:
Create a project in the Firebase Console.
Enable Realtime Database.
Update the firebaseConfig object in index.html with your own API keys.
Important: Set your Realtime Database rules to allow read/write access (for testing, set .read and .write to true).
Serve: Deploy to any static hosting service (Firebase Hosting, GitHub Pages, Vercel) or run on a local server (e.g., VS Code Live Server).
Future Roadmap
Encryption: Implement client-side encryption to ensure that even Firebase administrators cannot read the shared text.
Room System: Generate unique URLs (e.g., textbridge.app/room/xyz) to allow multiple users to have private rooms rather than one global text area.
History: Add an "Undo" feature to revert recent changes.
License
This project is open source and available under the MIT License.
