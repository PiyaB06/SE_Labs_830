# Lab 4: Pac-Man

## Project overview

This repository contains a single-file Pac-Man-style game built with Pygame. The Lab 4 work fixes power-pellet behavior and adds visual and audio feedback to pellet collection.

## Changes made

- **Fixed power pellets:** Power pellets are marked with `o` in the maze. When one is collected, the game recognizes that marker, awards the pellet points plus the power-pellet bonus, starts the timed frightened mode, and reverses every ghost that has not already been eaten. While frightened mode is active, ghosts can be eaten on collision for bonus points.
- **Added individual frightened colors:** Each ghost has its own color override while frightened, rather than all frightened ghosts sharing the same color. Other modes keep their existing default colors.
- **Added pellet sounds:** Collecting pellets plays a short alternating sound. Collecting the final pellet plays a higher, longer sound to distinguish the win-triggering pickup.

## Incomplete bonus-life feature

The game update logic can award an extra life when the score reaches a configured threshold, and the file defines a 1,000-point threshold. However, a second definition of `bonus_life_threshold()` later in the file contains only `pass`, which replaces the earlier definition in Python. As a result, the threshold is currently `None` and the game does **not** award bonus lives. This feature needs that duplicate empty definition removed or implemented to work.

## Submission materials

The repository also includes before-and-after gameplay videos and the chat history associated with the work.

**Project repository:** [PiyaB06/34_pacman](https://github.com/PiyaB06/34_pacman)