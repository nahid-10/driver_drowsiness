Overview

This project monitors a driver's eyes using a webcam (or video) and computes the Eye Aspect Ratio (EAR) from facial landmarks. If eyes stay closed or EAR is below a threshold for a configurable number of consecutive frames, the system triggers an alert (sound, visual, or both).

Features

Real-time face and facial-landmark detection using dlib.

Eye Aspect Ratio (EAR) calculation for blink/eye-closure detection.

Configurable thresholds and consecutive-frame detection logic.

Alerts: beep sound and on-screen warning.

Works with webcam or prerecorded video.

Project Structure
driver_drowsiness/

├─ models/

│  └─ shape_predictor_68_face_landmarks.dat   # dlib landmark model 

├─ src/

│  ├─ drowsiness_detector.py                  # main script (webcam / video)

│  ├─ utils.py                                # helper functions (EAR, sound, etc.)

│  └─ train_model.py                          # optional (if using custom ML)

├─ requirements.txt
├─ README.md
└─ examples/
   └─ sample_video.mp4

Requirements

Minimum tested environment:

Python 3.8+

OpenCV (opencv-python)

dlib (compiled or prebuilt wheel)

imutils

numpy

playsound (or simpleaudio) for alert sound

scipy (optional)

tqdm (optional)




Note: Installing dlib can require CMake and build tools. On Windows use prebuilt wheels or conda; on Linux/Mac install CMake + boost first.

Installation

Clone the repo:

git clone https://github.com/nahid-10/driver_drowsiness.git
cd driver_drowsiness


(Optional) Create a virtual environment:

python -m venv venv
# Windows
venv\Scripts\activate
# macOS / Linux
source venv/bin/activate


Install dependencies:

pip install -r requirements.txt


Download dlib’s 68-landmark model and place it in models/:

shape_predictor_68_face_landmarks.dat — you can download from dlib model zoo.

Usage
Run with webcam (default)
python src/drowsiness_detector.py

Run with a video file
python src/drowsiness_detector.py --video examples/sample_video.mp4

Command-line options (example)
--shape-predictor   models/shape_predictor_68_face_landmarks.dat
--video             path/to/video.mp4      # if omitted, use webcam
--ear-threshold     0.25                   # eye aspect ratio threshold
--consec-frames     20                     # frames to trigger alert
--sound             alert.wav              # optional custom alert sound

Example: drowsiness_detector.py (usage snippet)
from src.drowsiness_detector import DrowsinessDetector

detector = DrowsinessDetector(
    shape_predictor_path="models/shape_predictor_68_face_landmarks.dat",
    ear_threshold=0.25,
    consec_frames=20,
    sound_path="assets/alarm.wav",
)

# Run webcam
detector.run(webcam_index=0)

# Or run on a video file
detector.run(video_path="examples/sample_video.mp4")

How it works (brief)

Detect face using dlib’s frontal face detector or OpenCV Haar cascade.

Use dlib’s shape predictor to find 68 facial landmarks.

Extract eye coordinates and compute the Eye Aspect Ratio (EAR).

If EAR < threshold for consec_frames consecutive frames → increment counter.

When counter exceeds consec_frames, trigger alert and display on-screen warning.

Reset counter when EAR goes back above threshold (eyes open).

EAR formula (for one eye):

EAR = (||p2 - p6|| + ||p3 - p5||) / (2 * ||p1 - p4||)


where p1..p6 are eye landmark points.

Training / Model (optional)

This project uses the pre-trained dlib facial landmark model for landmarks detection, so no custom training is required for EAR-based detection.

If you want to build a classifier (CNN/RNN) to detect drowsiness from frames or sequences:

Prepare labeled dataset (open/closed eyes or drowsy/not drowsy sequences).

Train a lightweight CNN or 3D-CNN / LSTM on sequences.

Save a model.pth / model.h5 and load it in src/train_model.py or src/drowsiness_detector.py.

Basic tips for training:

Augment data (brightness, rotation).

Use sequences of frames (temporal context improves accuracy).

Evaluate on held-out drivers to avoid overfitting.

Tips to improve

Use a multi-modal approach: combine head pose, yawning detection, and steering wheel behavior.

Add face tracking and smoothing of EAR values (rolling average) to reduce false positives.

Use infrared camera or NIR for night-time robustness.

Use a lightweight temporal model (1D-CNN or LSTM) to detect micro-sleeps.

Implement a user calibration step to adapt EAR threshold per-driver.

Troubleshooting

dlib installation issues: Install CMake and Visual Studio build tools (Windows) or use conda: conda install -c conda-forge dlib.

Low FPS: Resize frames before processing, or run detection every N frames and track in between.

False alarms: Increase ear_threshold slightly or use longer consec_frames.

No sound on Windows: Try playsound alternatives (e.g., simpleaudio) or use system-specific calls.

Contributing

Contributions are welcome!

Fork the repo

Create a feature branch (git checkout -b feature-name)

Commit your changes (git commit -m "Add feature")

Push and open a PR

Please add tests for new features and keep code style consistent.

License & Acknowledgements

MIT License (or choose your preferred license).

Uses: dlib (landmark predictor), OpenCV, and many open-source resources for EAR definition and examples.

Contact

Md Nahid Hossain

GitHub: https://github.com/nahid-10
