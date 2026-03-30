# Puzzle

An Android sliding-puzzle game built around two ideas:

1. **A playable image-based puzzle system**
2. **A simple artificial neural network experiment** used to influence scoring / level progression

This project was originally developed as a graduation project, so some class names, comments, and variable names are in Turkish.

## What the project does

The app turns a source image into a grid of puzzle tiles, removes one tile to create the empty space, shuffles the board, and lets the player solve the puzzle by moving adjacent pieces into the empty slot.

At the same time, the project experiments with a lightweight neural-network-based scoring idea:
- player performance is evaluated using **time spent** and **success / failure**
- those values are passed through a **small hand-built MLP**
- the result affects the player's score and the next level state

## Main features

- **Android puzzle game**
- **Image splitting into puzzle tiles**
- **Dynamic board generation**
- **Sliding-piece movement**
- **Solved-state detection**
- **Custom shuffle logic**
- **Difficulty / level progression based on Fibonacci-inspired steps**
- **A small custom XOR neural network implementation**

## Project structure

### Game side
The game package contains the core puzzle logic:

- `MainActivity`  
  Launches the puzzle board and binds the UI to the game logic.

- `Logic`  
  Creates the game object, places the puzzle pieces on the screen, and initializes the board.

- `GameOb`  
  Handles move updates, validates whether a clicked tile is adjacent to the empty slot, swaps tiles when valid, and checks whether the puzzle is solved.

- `Level`  
  Stores the original solution image grid, the shuffled grid, score, level state, timing information, and puzzle completion logic.

- `FKaristir`  
  Shuffles the puzzle by moving the empty tile through valid directions. Also contains Fibonacci-based level-step logic.

- `SplitImage`  
  Splits a drawable resource into sub-images and converts them into puzzle tiles.

- `MyImage`  
  Wrapper around each puzzle piece, storing its bitmap, ID, empty-tile status, and `ImageView`.

### Neural network side
The `ysa/` package contains a small custom neural-network implementation:

- `JAnn`  
  Trains and tests a tiny MLP on the XOR problem, then outputs a rounded result based on the current game-related inputs.

- `Net`  
  Implements forward propagation, backpropagation, weight updates, and error calculation.

- `NetworkIslemleri`  
  Handles network parameters such as random weight initialization, momentum storage, sigmoid activation, and loss calculation.

- `NoronIslemleri`  
  Stores the layer structure, neuron outputs, deltas, weights, and previous weight values.

## Technical notes

- The puzzle board is built from an image resource (`R.drawable.tiger` in the current version).
- The board size is determined by `howMany`, where the square root defines the row/column count.
- One randomly selected tile is turned into the empty tile.
- The current implementation checks valid moves by testing whether the clicked tile is directly adjacent to the empty tile.
- Puzzle completion is checked by comparing the current tile arrangement with the original solution arrangement.
- Level progression is based on a Fibonacci-style progression model.
- The neural network is a small educational implementation, not a production ML system.

## What is interesting here

This repo is interesting less because of visual polish and more because it combines:

- classic mobile puzzle mechanics
- custom image-processing/game-state code
- hand-written neural-network experimentation
- adaptive progression ideas

It is an early project, but it shows an attempt to combine gameplay logic with simple AI-driven progression rather than building only a static puzzle.

## Limitations

- The codebase is older and not organized in a modern Android architecture style.
- Naming is mixed Turkish/English.
- The ANN usage is intentionally simple and should be seen as an experiment, not a robust gameplay AI.
- Some comments and unfinished ideas from the graduation-project phase are still present.

## Future directions

- Refactor the project into cleaner modules
- Modernize the Android structure
- Make the progression logic easier to inspect and tune
- Expand the adaptive system beyond XOR-based experimentation
- Support multiple images, puzzle sizes, and cleaner UI/UX

## Summary

**Puzzle** is an Android sliding-puzzle project with a hand-built gameplay core and a small custom ANN experiment layered on top of its scoring / progression system.

It is best understood as a meaningful student-engineering project that combines:
- puzzle mechanics
- image splitting
- board-state management
- basic ML experimentation
