# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A collection of self-contained browser games. Each game is a **single HTML file** with all CSS and JS inlined — no build step, no dependencies, no server required. Open any `.html` file directly in a browser to run it.

## Games

### `shooter.html` — NEON SIEGE
Top-down arena shooter using the HTML5 Canvas API.

**Architecture:**
- Single `<canvas id="c">` fills the viewport; redraws every frame via `requestAnimationFrame`
- Game loop: `update(dt)` mutates state → `draw()` renders — strictly separated
- State machine: `gameState` ∈ `{ menu, playing, levelClear, gameOver }`
- Entity arrays: `bullets`, `enemies`, `particles` — iterated in reverse when splicing
- Input captured into `keys` (keyboard) and `mouse` (position + buttons) objects; consumed by `update`
- Enemy types: `grunt` (slow, 1 HP), `charger` (fast dash, 1 HP), `tank` (slow, 3 HP) — configured via lookup tables in `spawnEnemy`
- Difficulty scales with `level`: `quotaForLevel` and `intervalForLevel` control enemy count and spawn rate

### `tictactoe.html` — Tic Tac Toe
DOM-based two-player game (no canvas).

**Architecture:**
- 9 `.cell` divs with `data-i` indices; state tracked in a flat `board` array
- Win detection iterates the 8 `WINS` constant patterns
- Score persists in a `scores` object across resets (not localStorage)

## Development Workflow

No build tools exist. Edit the HTML file directly and refresh the browser.

After changes, commit and push:
```bash
git add <file>
git commit -m "descriptive message"
git push
```

Remote: `https://github.com/oldmonk31/ClaudeCodeDemo`
