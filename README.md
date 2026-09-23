# Pac-Man

A Java-based recreation of the classic **Pac-Man** arcade game built using **JavaFX** and **Gradle**.

The project implements player movement, maze navigation, pellet collection, scoring, lives, multiple levels, collision detection, and ghost behaviour using chase and scatter modes.

## Features

- Classic Pac-Man maze gameplay
- Keyboard-controlled Pac-Man movement
- Four directional controls using the arrow keys
- Pellet collection and score tracking
- Multiple player lives
- Multiple configurable levels
- Ghost movement and targeting behaviour
- Ghost **CHASE** and **SCATTER** modes
- Collision detection between:
  - Pac-Man and walls
  - Pac-Man and pellets
  - Pac-Man and ghosts
- Automatic level progression
- Game-over and player-win states
- Configurable movement speeds and level behaviour
- JavaFX graphical interface
- Sprite-based rendering

## Tech Stack

- **Java**
- **JavaFX 17**
- **Gradle**
- **JSON Simple**
- **JUnit 5**

## Project Structure

```text
pacman/
├── build.gradle
└── src/
    └── main/
        ├── java/
        │   └── pacman/
        │       ├── App.java
        │       ├── ConfigurationParseException.java
        │       │
        │       ├── model/
        │       │   ├── engine/
        │       │   ├── entity/
        │       │   ├── factories/
        │       │   ├── level/
        │       │   └── maze/
        │       │
        │       └── view/
        │           ├── background/
        │           ├── display/
        │           ├── entity/
        │           └── keyboard/
        │
        └── resources/
            ├── config.json
            ├── map.txt
            ├── new-map.txt
            └── maze/
                ├── ghosts/
                ├── pacman/
                ├── walls/
                ├── pellet.png
                └── PressStart2P-Regular.ttf
Architecture

The project separates the game logic from the user interface.

Model

The model package contains the main gameplay logic, including:

Game engine
Maze representation
Levels
Player
Ghosts
Pellets
Physics and collision handling
Entity factories
View

The view package handles:

JavaFX rendering
Game window
Score display
Lives display
Game-state messages
Keyboard input
Design Patterns

The implementation uses several object-oriented design patterns.

Factory Pattern

Factories are used to create different game objects including:

Pac-Man
Ghosts
Pellets
Walls

The RenderableFactoryRegistry manages the available renderable factories.

Observer Pattern

Observers are used to communicate changes between parts of the game.

Examples include:

Game-state changes
Score changes
Lives changes
Pac-Man position updates for ghost behaviour
Command Pattern

Player movement is implemented using command objects such as:

MoveUpCommand
MoveDownCommand
MoveLeftCommand
MoveRightCommand

Keyboard input creates movement commands which are processed by the movement system.

Ghost Behaviour

Ghosts alternate between two behaviour modes.

Scatter Mode

Ghosts move toward their assigned corner of the maze.

Chase Mode

Ghosts target Pac-Man's current position.

When ghosts reach intersections, they evaluate possible directions and select a path based on the distance to their current target.

Ghosts also avoid immediately reversing direction unless no alternative path is available.

Game Configuration

Game settings are stored in:

src/main/resources/config.json

Example configuration:

{
  "map": "src/main/resources/map.txt",
  "numLives": 3,
  "levels": [
    {
      "levelNo": 1,
      "pacmanSpeed": 3.0,
      "ghostSpeed": {
        "chase": 1.5,
        "scatter": 1.5,
        "frightened": 1.0
      },
      "modeLengths": {
        "chase": 7,
        "scatter": 20,
        "frightened": 10
      }
    }
  ]
}

This makes it possible to configure:

Number of lives
Pac-Man speed
Ghost speed
Ghost-mode durations
Maze file
Level-specific difficulty
Scoring

Each pellet is worth:

100 points

The player's score increases whenever a pellet is collected.

A level is completed when all pellets in the maze have been collected.

Controls
Key	Action
↑	Move Up
↓	Move Down
←	Move Left
→	Move Right
Running the Project
Requirements

Make sure you have:

Java 17 or later
Gradle

installed on your system.

Clone the Repository
git clone https://github.com/Anandkripal/pacman.git
cd pacman
Run with Gradle
gradle run

If you are using the Gradle wrapper, you can instead run:

./gradlew run

On Windows:

gradlew.bat run
Main Entry Point

The application starts from:

src/main/java/pacman/App.java

The configured Gradle main class is:

pacman.App
Game Flow

The basic gameplay loop is:

Start Game
    ↓
Load Maze and Level Configuration
    ↓
READY State
    ↓
Gameplay Begins
    ↓
Move Pac-Man and Ghosts
    ↓
Detect Collisions
    ↓
Collect Pellets / Lose Lives
    ↓
Check Level Completion
    ↓
Next Level or Player Wins

If the player loses all lives, the game transitions to the GAME OVER state.

What This Project Demonstrates

This project demonstrates practical application of:

Object-oriented programming
Java interfaces and inheritance
Event-driven programming
JavaFX application development
Collision detection
Basic game physics
Game-loop architecture
JSON-based configuration
Observer pattern
Factory pattern
Command pattern
Modular software architecture
Future Improvements

Possible improvements include:

Power pellets
Frightened ghost behaviour
Ghost-eating mechanics
Sound effects and background music
High-score persistence
Start and pause menus
Additional maps
More advanced ghost personalities
Improved animations
Difficulty selection
Unit and integration test coverage
