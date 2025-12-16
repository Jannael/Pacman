# Pacman Clone

A classic Pacman game clone built with **TypeScript** and **HTML5 Canvas**. This project recreates the core mechanics of the original arcade game, including the distinct pathfinding behaviors of the four ghosts.

## Description

This project implements the famous arcade game logic in a web environment. It features a custom grid-based collision system, asset management for animations, and a pathfinding algorithm that drives the autonomous ghosts. The game is rendered on an HTML Canvas, providing smooth performance and control.

## Features

- **Classic Gameplay**: Collect all pellets to win while avoiding ghosts.
- **Unique Ghost AI**: Each ghost has its own specific personality and chasing algorithm, mimicking the original arcade behaviors.
- **Pathfinding**: Custom implementation of target-based navigation for enemies.
- **Responsive Design**: The game board adapts to the screen size.
- **Asset Handling**: Support for sprites and animations (GIFs/PNGs).

## How it Works

The game is built around a central loop that renders the state of the `gameboard` matrix to the canvas.

### The Grid System
The game map is represented as a 2D array (`gameboard` in `script.ts`). Each cell contains a number or character representing its state:
- `1`: Wall
- `2`: Pellet (Coin)
- `0`: Empty space
- `P`: Pacman
- `b`, `p`, `i`, `c`: Ghost positions (Blinky, Pinky, Inky, Clyde)

### Pathfinding (`routeAlgorithm.ts`)
The ghosts use a pathfinding function `followThetarget` to decide their next move. This function:
1.  Calculates possible moves (Up, Down, Left, Right) excluding walls and reverse direction.
2.  Calculates the Euclidean distance from each possible immediate neighbor to the **Target Tile**.
3.  Selects the move that minimizes the distance to the target.

## Ghost Personalities

One of the most interesting aspects of this project is the faithful implementation of the ghost artificial intelligence. Each ghost calculates its **Target Tile** differently:

### 🔴 Blinky (Red) - The Chaser
- **Behavior**: Aggressive.
- **Target**: Pacman's current tile.
- **Logic**: Constantly tries to shorten the distance to Pacman effectively.

### 🌸 Pinky (Pink) - The Ambusher
- **Behavior**: Tries to get ahead of you.
- **Target**: 4 tiles *in front* of Pacman's current direction.
- **Logic**: Predicts where Pacman is going to cut him off.

### 💧 Inky (Cyan) - The Strategist
- **Behavior**: Unpredictable support.
- **Target**: Calculated based on a vector between Blinky's position and a point 2 tiles in front of Pacman.
- **Logic**: Uses Blinky's position to flank Pacman, often trapping him between the two ghosts.

### 🍊 Clyde (Orange) - The Coward
- **Behavior**: Chases then retreats.
- **Target**: Pacman's tile *unless* he gets too close (within 8 tiles). If closer than 8 tiles, he switches target to his home corner (bottom-left).
- **Logic**: Appears to chase but will suddenly turn away when expecting a collision.

## Installation & Usage

### Prerequisites
- Node.js (v24.0.3 or higher recommended)
- pnpm

### Setup
1.  Clone the repository:
    ```bash
    git clone <repository-url>
    ```
2.  Install dependencies:
    ```bash
    pnpm install
    ```
3.  Compile the TypeScript code (if not using a bundler with on-the-fly compilation):
    ```bash
    tsc -w
    ```
    *Note: The project uses `script.js` directly in the HTML, so ensure the TypeScript is compiled to JavaScript.*

### Running the Game
Simply open `index.html` in your browser.
or use a local server like `live-server` or `http-server` for a better experience with module loading.

## Controls

- **Arrow Up**: Move Up
- **Arrow Down**: Move Down
- **Arrow Left**: Move Left
- **Arrow Right**: Move Right

---

*Enjoy the retro experience!*