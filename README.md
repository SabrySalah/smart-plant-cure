# Smart Plant Cure — AI-powered Plant Disease Detection & Curing System

**Smart Plant Cure** is an end-to-end system that uses a Convolutional Neural Network (CNN) to detect plant diseases from images and automatically release the correct treatment via an IoT hardware setup connected to a water/source. The project also includes a web interface for monitoring and manual control.

## Features
- ✅ CNN model to classify plant diseases from leaf images  
- ✅ Automatic hardware control (Arduino) to dispense targeted treatment into irrigation/water lines  
- ✅ Web dashboard to monitor plant health, view recent detections, and manually trigger treatments  
- ✅ Logging of detections and treatments for audit and review

## Repo structure
See the top-level folders:
- `model/` — training scripts, notebooks, preprocessing
- `web/` — frontend and backend (API + dashboard)
- `hardware/` — Arduino sketches, wiring diagrams, BOM (bill of materials)
- `data/` — dataset info and small sample images
- `docs/` — deployment & usage guides

## Quick demo
1. Train or load the pretrained CNN model from `model/checkpoints/`.
2. Start backend API: `cd web/backend && uvicorn main:app --reload`
3. Start frontend: `cd web/frontend && npm start` (or open `index.html`)
4. Connect Arduino to server (serial or MQTT). The backend will send commands to trigger treatment.

## Model (high level)
- Architecture: Convolutional Neural Network (CNN) — e.g., transfer learning with ResNet or MobileNet for faster training and inference.
- Input: RGB leaf images (recommended size 224x224)
- Output: disease class and confidence score
- Training: augment images (flip, rotate, color jitter), use cross-entropy loss, early stopping, and learning rate scheduling.

## Hardware
- Microcontroller: Arduino Uno / ESP32 (ESP32 recommended for WiFi)
- Actuators: peristaltic pumps or solenoid valves for releasing treatments
- Power: separate power supply for pumps (match voltage/current)
- Communication: Serial over USB, or MQTT over WiFi if using ESP32
- Add wiring diagram in `hardware/wiring_diagram.png` and the Arduino sketch `hardware/arduino/plant_controller.ino`

## Installation (backend)
```bash
# create virtualenv
python -m venv venv
source venv/bin/activate   # or venv\Scripts\activate on Windows
pip install -r requirements.txt
# run backend
uvicorn main:app --reload
