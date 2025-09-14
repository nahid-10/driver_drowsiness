# Driver Drowsiness Detection System 🚗💤


This project demonstrates how to build a **real-time driver drowsiness detection system** using Python, OpenCV, and Dlib. The system monitors eye movements using facial landmarks and triggers an alert when signs of fatigue or sleepiness are detected.

---

## 📌 Project Overview

The goal of this project is to:  

- Detect driver’s face and eye regions using **dlib facial landmark detection**  
- Calculate **Eye Aspect Ratio (EAR)** to measure eye openness  
- Trigger an **alarm alert** when eyes remain closed beyond a threshold  
- Provide **real-time monitoring** using a webcam or pre-recorded video  

---

## 🧰 Tools & Technologies

| Tool / Library       | Purpose                                       |
|----------------------|-----------------------------------------------|
| `OpenCV`             | Video capture, image processing, visualization |
| `dlib`               | Facial landmark detection (68 points)         |
| `imutils`            | Utility functions for image resizing and display |
| `numpy`              | Numerical computations for EAR formula        |
| `playsound` / `simpleaudio` | Play alarm sound when drowsiness detected |
| `scipy`              | Distance calculations for EAR                 |
| `Python`             | Core programming language                     |

---

## 📂 Files Included

- `src/drowsiness_detector.py` – Main script (webcam/video detection)  
- `src/utils.py` – Helper functions (EAR calculation, sound handling)  
- `src/train_model.py` – Optional file for training/testing ML-based models  
- `models/shape_predictor_68_face_landmarks.dat` – Pre-trained dlib landmark model (not included)  
- `examples/sample_video.mp4` – Example input video  
- `requirements.txt` – Python dependencies  
- `README.md` – Project documentation  

---

## 📊 Sample Usage

Some example use cases:

- Monitor driver **via webcam** in real time  
- Detect **eye closure and drowsiness** from recorded video  
- Trigger **sound alarms** when driver appears sleepy  
- Display **on-screen warnings** to alert the driver  

---

## ⚙️ Technical Details

- **Face Detection:** dlib frontal face detector  
- **Facial Landmarks:** 68-point predictor (`shape_predictor_68_face_landmarks.dat`)  
- **Eye Aspect Ratio (EAR):**  
- **Threshold:** EAR < 0.25 indicates eyes closed  
- **Consecutive Frames Rule:** Alarm triggers if eyes stay closed for 20+ frames  
- **Alerts:** Plays sound + displays warning  

---

## 🔧 Optimization Features

- **Configurable EAR threshold** for different drivers  
- **Adjustable consecutive frame count** to reduce false alarms  
- **Webcam or video input** options  
- **Lightweight computation** for real-time performance  

---

## 💡 Future Improvements

- Add **yawn detection** using mouth aspect ratio (MAR)  
- Monitor **head pose** to detect nodding off  
- Train a **deep learning model (CNN/LSTM)** for better accuracy  
- Support **infrared cameras** for night-time driving  

---

## 📄 License

This project is **open-source** and free to use for educational purposes.
