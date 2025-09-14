# Driver Drowsiness Detection System 🚗💤

[![GitHub](https://img.shields.io/badge/Code-GitHub-black?logo=github)](https://github.com/nahid-10/driver_drowsiness)  
**Tools:** Python, OpenCV, Dlib, Deep Learning  

A real-time driver drowsiness detection system that uses facial landmark detection and Eye Aspect Ratio (EAR) monitoring to detect fatigue and alert the driver.

---

## 📌 Features
- Real-time **eye tracking** using dlib’s 68-point facial landmarks.
- **Eye Aspect Ratio (EAR)** calculation for detecting eye closure.
- Configurable thresholds and consecutive frame detection logic.
- Alerts: sound + on-screen warning.
- Works with **webcam** or **video input**.

## 📂 Project Structure

driver_drowsiness/
├─ models/
│  └─ shape_predictor_68_face_landmarks.dat   # dlib landmark model (not included)
├─ src/
│  ├─ drowsiness_detector.py                  # main script (webcam / video)
│  ├─ utils.py                                # helper functions (EAR, sound, etc.)
│  └─ train_model.py                          # optional (if using custom ML)
├─ requirements.txt
├─ README.md
└─ examples/
   └─ sample_video.mp4
