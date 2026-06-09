MPU6050-based 3D Cube Visualizer project that creates a real-time, motion-controlled rotating cube on an OLED display.
Project Overview
This embedded system project combines an MPU6050 (6-axis accelerometer/gyroscope) with a WeMos Mini Pro (ESP8266-based) and an SSD1306 OLED display to create a physically interactive 3D visualization. When you tilt or rotate the device, the cube on the screen responds in real-time, mimicking your movements.

How It Works
1. Motion Sensing (MPU6050)
The MPU6050 reads raw accelerometer data (ax, ay, az) to determine the device's orientation in space

It calculates pitch (forward/backward tilt) and roll (left/right tilt) angles using trigonometric functions:

atan2(ax, sqrt(ay² + az²)) - calculates pitch angle

atan2(ay, sqrt(ax² + az²)) - calculates roll angle

2. Angle Smoothing
Uses an exponential moving average (smoothing factor of 0.9) to reduce jitter and noise

Creates fluid, natural-looking rotations instead of abrupt movements

3. 3D to 2D Projection
Defines a cube with 8 vertices in 3D space (coordinates: ±halfCubeSize where halfCubeSize = 20)

Applies rotation matrices to transform the cube based on pitch and roll angles:

Pitch rotation (around X-axis): transforms Y and Z coordinates

Roll rotation (around Y-axis): transforms X and Z coordinates

Projects the 3D points onto 2D screen coordinates (128×64 pixels)

4. Visualization
Draws the cube's 12 edges (wireframe model)

Adds an "X" marking on the front face (diagonal lines) for visual orientation

Updates at approximately 20 FPS (50ms delay)

Key Features
 Real-time motion tracking - Cube follows physical device movement
 Smooth animation - Noise filtering for stable display
 3D wireframe rendering - Efficient edge-only drawing
 Low resource usage - Optimized for microcontroller constraints
 No external libraries needed beyond standard ones

Hardware Connection Guide
text
WeMos Mini Pro    →    MPU6050    →    OLED Display
3.3V             →    VCC        →    VCC
GND              →    GND        →    GND
D2 (GPIO4)       →    SDA        →    SDA
D1 (GPIO5)       →    SCL        →    SCL
Note: Both MPU6050 and OLED share the same I2C bus (SDA/SCL lines)

Mathematical Foundation
The code implements 3D rotation matrices:

Rotation around X-axis (pitch):

Y' = Y×cos(θ) - Z×sin(θ)

Z' = Y×sin(θ) + Z×cos(θ)

Rotation around Y-axis (roll):

X' = X×cos(φ) + Z'×sin(φ)

Z'' = -X×sin(φ) + Z'×cos(φ)

