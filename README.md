# 🎵 AI Hand Gesture Volume Controller

An interactive web application that allows users to control media volume using **hand gestures through their webcam**.

The system uses a **machine learning model trained with Google Teachable Machine** and runs entirely in the browser using **TensorFlow.js**, enabling real-time gesture recognition without requiring any backend server.

---

# 🚀 Live Demo

Try the project here:

👉 https://nr-music-handgesture.netlify.app/

---

# 📌 Project Overview

This project demonstrates how **machine learning models can be integrated into web applications** to create interactive user interfaces.

Instead of using traditional buttons or sliders, users can control media playback using **hand gestures detected by the webcam**.

The application processes webcam frames in real-time, sends them to a trained AI model, and performs actions such as adjusting the volume based on the detected gesture.

---

# ⚙️ How It Works

1. Click **Start Camera** to activate the webcam.
2. Upload an **audio file** from your device.
3. Show the trained **hand gestures** in front of the camera.
4. The AI model detects the gesture.
5. The application adjusts the **media volume accordingly**.

All processing happens directly in the browser using **TensorFlow.js**, ensuring fast and privacy-friendly execution.

---

# ✨ Features

- Real-time **AI gesture recognition**
- Webcam-based interaction
- Gesture-controlled **volume adjustment**
- Audio playback support
- Works completely in the browser
- No server or backend required
- Easy to extend with additional gestures

---

# 🎥 Video Playback Support

The project currently controls the volume of an **audio element**.  
However, it can also control **video playback** with a small modification.

### Steps to enable video control:

1. Replace the `<audio>` element with a `<video>` element in the HTML.
2. Change the file input to accept video files.
3. The gesture logic will continue to work because both media types use the `.volume` property in JavaScript.

Example:

```html
<video id="mediaPlayer" controls></video>
