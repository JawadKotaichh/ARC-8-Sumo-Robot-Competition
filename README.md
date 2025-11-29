# ARC-8 Sumo Robot Competition

This repository contains Arduino code for a Sumo Robot designed to compete in the ARC-8 Sumo Robot Competition. The robot is equipped with multiple sensors for line detection and opponent detection, and uses the XMotion library for motor control.

## Project Overview

The Sumo Robot is an autonomous robot designed to compete in a sumo wrestling-style competition. The robot must:
- Stay within a circular ring (detected by line sensors)
- Detect and locate opponents using obstacle sensors
- Attack opponents while maintaining its position within the ring
- Avoid falling out of the ring boundaries

## Hardware Components

### Sensors

#### Line Detection Sensors
- **4 Line Sensors**: Front Right (FR), Front Left (FL), Back Right (BR), Back Left (BL)
  - Used to detect the white ring boundary
  - Black surface = inside ring (safe)
  - White surface = outside ring (danger)

#### Opponent Detection Sensors
- **5 Obstacle Sensors**: Left, Left Diagonal, Middle, Right Diagonal, Right
  - Used to detect the presence and position of opponents
  - Triggers attack behaviors when opponent is detected

### Additional Components
- **XMotion Motor Controller**: Controls robot movement and navigation
- **DIP Switches**: Configuration switches (3 switches)
- **Start Button**: Microstart input (D10)
- **LED Indicators**: User feedback LEDs

## Code Files

### 1. `Prototype_Sumo_Robot.ino`
Main implementation with comprehensive sumo robot logic.

**Features:**
- Ring boundary detection using 4 line sensors
- Opponent detection using 3 obstacle sensors
- Attack strategies based on opponent position
- Star search pattern for finding opponents when lost
- Ring-keeping behavior to prevent falling out

**Key Functions:**
- `is_in_ring()`: Checks if robot is within ring boundaries
- `is_not_detected()`: Checks if opponent is detected
- `Attack()`: Implements attack strategies based on sensor readings
- `star_search()`: Performs a star pattern search to locate opponents

### 2. `Xmotion_code.ino`
Advanced implementation with enhanced sensor configuration and movement patterns.

**Features:**
- 5 opponent detection sensors for better coverage
- 2 line sensors for boundary detection
- Arc turning capabilities for smoother movement
- Memory system to remember last detected opponent position
- DIP switch configuration support
- Start button integration

**Key Behaviors:**
- Diagonal sensor detection with arc turns
- Line sensor edge detection and recovery
- Memory-based movement when opponent is lost
- Configurable via DIP switches

### 3. `prototypecode.ino`
Simple prototype code for basic testing.

**Features:**
- Basic sensor reading
- Simple forward/stop movement based on sensor input
- Minimal implementation for initial testing

## Installation & Setup

### Prerequisites
- Arduino IDE
- XMotion library installed in Arduino IDE
- Compatible Arduino board (compatible with XMotion shield)

### Setup Instructions

1. **Install XMotion Library**
   - Download and install the XMotion library for Arduino
   - Ensure the library is properly installed in your Arduino libraries folder

2. **Configure Pin Assignments**
   - Open the desired `.ino` file
   - Update pin numbers according to your hardware configuration
   - Note: `Prototype_Sumo_Robot.ino` has placeholder pin numbers that need to be filled in

3. **Upload Code**
   - Connect your Arduino board
   - Select the correct board and port in Arduino IDE
   - Upload the code to your board

4. **Calibration**
   - Test line sensors on black and white surfaces
   - Adjust sensor thresholds if needed
   - Test obstacle detection range
   - Fine-tune movement speeds and delays

## Usage

### Starting the Robot
1. Power on the robot
2. Wait for initialization (5-second delay in prototype code)
3. Press the start button (if using `Xmotion_code.ino`)
4. Robot will begin autonomous operation

### Robot Behaviors

#### Ring Keeping
- When a line sensor detects white (ring boundary):
  - Front sensors: Robot backs up and rotates
  - Back sensors: Robot moves forward and rotates
- Ensures robot stays within competition ring

#### Opponent Detection & Attack
- When opponent is detected:
  - Single sensor: Robot turns toward opponent
  - Multiple sensors: Robot moves forward to attack
  - No detection: Robot performs search pattern

#### Search Pattern
- Star search algorithm: Robot moves in a 5-point star pattern
- Each point involves forward movement and 144-degree rotation
- Continues until opponent is detected

## Configuration

### Adjustable Parameters

**In `Prototype_Sumo_Robot.ino`:**
- `speed`: Movement speed (default: 70)
- `search_distance`: Distance for search pattern (default: 100)
- `Timer`: Movement time duration (default: 1500ms)

**In `Xmotion_code.ino`:**
- Sensor pin assignments can be modified
- Movement speeds and delays can be adjusted
- DIP switch configurations can be customized

## Troubleshooting

### Common Issues

1. **Robot not moving**
   - Check motor connections
   - Verify XMotion library is installed
   - Ensure power supply is adequate

2. **Sensors not detecting**
   - Verify sensor pin connections
   - Check sensor power supply
   - Test sensors individually with serial output

3. **Robot falls out of ring**
   - Calibrate line sensors
   - Adjust sensor thresholds
   - Increase backup/rotation delays

4. **Not detecting opponents**
   - Check obstacle sensor connections
   - Verify sensor range
   - Adjust detection sensitivity

## Competition Strategy

The robot implements several strategic behaviors:
- **Aggressive Forward Movement**: Moves forward when opponent is centered
- **Positioning**: Uses diagonal sensors for better angle of attack
- **Ring Awareness**: Prioritizes staying in ring over attacking
- **Search Pattern**: Systematic search when opponent is lost

## Development Notes

- `Prototype_Sumo_Robot.ino` contains incomplete pin assignments (marked with `;`)
- Some code includes commented-out sensor reading sections
- The star search function uses a 5-point pattern (144-degree turns)
- Memory system in `Xmotion_code.ino` helps maintain direction when opponent is temporarily lost

## Future Improvements

- Complete pin assignments in prototype code
- Add serial debugging output
- Implement PID control for smoother movements
- Add calibration mode for sensor tuning
- Implement more sophisticated attack strategies
- Add configuration via serial commands

## License

This project is developed for the ARC-8 Sumo Robot Competition.

## Contributors

Developed for ARC-8 Sumo Robot Competition participation.

---

**Note**: Make sure to test the robot thoroughly before competition. Adjust parameters based on your specific hardware configuration and competition ring characteristics.

