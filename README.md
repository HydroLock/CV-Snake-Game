# 🐍 CV Snake Game

A computer vision adaptation of the classic Nokia Snake game where the player controls the snake using **real-time hand gestures** captured through a webcam.

Instead of using keyboard controls, the game detects hand movement using **MediaPipe** and **OpenCV**, translating swipe gestures into movement commands while the game itself is rendered using **Pygame**.

---

## Inspiration

This project was inspired by a short Instagram reel demonstrating the concept of controlling a Snake game using hand gestures.

Rather than reproducing an existing project, I treated the idea as a learning opportunity and built my own implementation from scratch. While the overall concept is inspired by that demonstration, the code structure, gesture handling logic, threading model, and gameplay integration are my own implementation choices.

If you are the creator of the original demonstration and would like to be credited directly, please feel free to reach out or open an issue. I'd be happy to add proper attribution.

---

## Features

- 🎥 Real-time webcam-based control
- ✋ Hand tracking using MediaPipe
- ↔️ Swipe-based directional controls
- ⚡ By making a fist, a temporary speed boost is activated
- 🧵 Multi-threaded architecture for smoother gameplay
- 🎮 Classic Snake gameplay rendered using Pygame
- 📹 Live webcam preview with hand landmarks and gesture feedback

---

## How It Works

The application consists of two components running simultaneously:

### Gesture Detection

The webcam feed is processed continuously using **MediaPipe Hands**.

The system tracks the wrist position between frames to determine the direction of hand movement:

- Swipe Left → Snake moves left
- Swipe Right → Snake moves right
- Swipe Up → Snake moves up
- Swipe Down → Snake moves down

To improve stability, a short gesture cooldown is applied after every recognized swipe to prevent multiple unintended direction changes.

### Speed Boost

The fingers that are folded to form a fist is monitored, which should include all 5 fingers.

When a fist is formed and detected by the camera, the game temporarily increases the snake's movement speed.

### Game Loop

The project separates gameplay and computer vision into independent threads:

- **Main Thread**
  - Runs the Snake game
  - Updates score and game state
  - Handles rendering through Pygame

- **Gesture Thread**
  - Captures webcam frames
  - Detects hand landmarks
  - Processes gestures
  - Updates the current movement direction

This keeps the game responsive while computer vision processing occurs in the background.

---

## Technologies Used

- Python
- OpenCV
- MediaPipe
- NumPy
- Pygame
- Threading

---

## Project Structure

```
CV-Snake-Game/
│
├── main.py
├── snake_game.py
├── gesture_controller.py
├── requirements.txt
├── setup.py
├── .gitignore.txt
└── __pycache__/
```

### File Overview

**main.py**

Coordinates the overall application by initializing the webcam, starting gesture detection in a separate thread, updating the game state, and managing application cleanup.

**gesture_controller.py**

Responsible for:

- Hand landmark detection
- Swipe gesture recognition
- Folded fingers detection for speed boost
- Gesture cooldown handling
- Webcam visualization

**snake_game.py**

Contains the core Snake game logic including movement, collisions, food generation, scoring, rendering, and game state management.

---

## Installation

Clone the repository:

```bash
git clone https://github.com/HydroLock/CV-Snake-Game.git
```

Move into the project folder:

```bash
cd CV-Snake-Game
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

---

## Running the Project

```bash
python main.py
```

Ensure that your webcam is connected and accessible before launching the application.

---

## Controls

| Gesture | Action |
|----------|--------|
| Swipe Left | Move Left |
| Swipe Right | Move Right |
| Swipe Up | Move Up |
| Swipe Down | Move Down |
| Form a fist | Speed Boost |
| ESC | Exit Game |

---

## Learning Outcomes

Developing this project helped me gain practical experience with:

- Real-time computer vision
- MediaPipe hand landmark detection
- Gesture recognition using positional tracking
- Multi-threaded application design
- Integrating OpenCV with Pygame
- Event-driven game development

---

## Possible Improvements

Some ideas I may explore in the future include:

- Improved gesture smoothing
- Customizable gesture sensitivity
- Difficulty selection
- Sound effects and background music
- High-score tracking
- Pause menu
- Better restart gestures
- Additional gesture-controlled game mechanics

---

## Acknowledgements

This project was developed based on the concept demonstrated in an Instagram reel.
The implementation in this repository was created independently as a personal learning project.
