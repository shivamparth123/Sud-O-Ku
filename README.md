# Sudoku — Terminal-Based C Game

A terminal-based Sudoku game written in **C** with an interactive **ncurses** interface. The program can generate a randomized Sudoku board, solve it automatically, or let the player solve it manually using keyboard navigation.

> **Repository note:** This repository is a fork of the original `Levi477/Sud-O-Ku` project. The fork relationship is intentionally preserved on GitHub. Any resume or portfolio description should accurately reflect your own contribution to the project.

## ✨ Features

- 🎲 **Random Sudoku generation**
- 🤖 **Automatic Sudoku solving** using recursive backtracking
- 🧩 **Interactive manual solving** in the terminal
- 🎮 Arrow-key navigation with `UP`, `DOWN`, `LEFT`, and `RIGHT`
- 🎯 Four difficulty levels:
  - **Easy** — 35 clues
  - **Medium** — 28 clues
  - **Hard** — 22 clues
  - **Give Up / Very Hard** — 17 clues
- ⏱️ **Live elapsed-time display** while solving
- ✅ Input validation using Sudoku row, column, and 3×3-box constraints
- 💡 Optional solution reveal after the 10-minute challenge period
- 🎨 Color-based terminal interface using ncurses
- 🖥️ Cross-platform screen-clearing logic for Windows/Unix-like systems (terminal/curses dependencies still apply)

## 🧠 How It Works

### 1. Generate a complete Sudoku

The program starts with an empty 9×9 grid, seeds selected 3×3 regions with random values, and completes the board using the recursive Sudoku solver.

### 2. Create the puzzle

A configurable number of cells are removed from the solved board according to the selected difficulty level.

```text
Easy        → 35 clues
Medium      → 28 clues
Hard        → 22 clues
Very Hard   → 17 clues
```

### 3. Solve automatically

The computer uses **recursive backtracking**:

```text
Find an empty cell
      ↓
Try numbers 1–9
      ↓
Check row / column / 3×3 box
      ↓
Place valid number
      ↓
Recursively solve remaining cells
      ↓
If stuck → undo and try next number
```

### 4. Solve manually

The player navigates through the board with the arrow keys. Empty cells accept values only when the value satisfies the Sudoku constraints.

## 🧮 Core Algorithm

The main solver is a classic **backtracking search**.

The safety check verifies three constraints:

1. The number does not already occur in the current row.
2. The number does not already occur in the current column.
3. The number does not already occur in the current 3×3 sub-grid.

The solver recursively fills cells and backtracks whenever a partial assignment cannot lead to a solution.

### Complexity

For a general Sudoku solver, backtracking has exponential worst-case behavior. For a standard 9×9 Sudoku, practical runtime depends heavily on the puzzle structure and the ordering of candidate choices.

The current implementation uses a straightforward **first-empty-cell** strategy rather than advanced heuristics such as Minimum Remaining Values (MRV).

## 🎮 Controls

| Key | Action |
|---|---|
| `↑` | Move cursor up |
| `↓` | Move cursor down |
| `←` | Move cursor left |
| `→` | Move cursor right |
| `Enter` | Enter a value in the selected empty cell |
| `q` | Quit the manual-solving mode |

## 📊 Difficulty Levels

The game uses the number of remaining clues to control difficulty:

| Level | Clues | Cells Removed |
|---|---:|---:|
| Easy | 35 | 46 |
| Medium | 28 | 53 |
| Hard | 22 | 59 |
| Very Hard | 17 | 64 |

> The current implementation controls difficulty by clue count. It does **not** explicitly verify that every generated puzzle has a unique solution.

## 🛠️ Tech Stack

- **Language:** C
- **Interface:** ncurses / terminal UI
- **Core algorithm:** Recursive backtracking
- **Randomization:** C standard library `rand()` / `srand()`
- **Input:** Keyboard navigation through ncurses
- **Build:** GCC + ncurses development libraries

## 📁 Project Structure

```text
Sud-O-Ku/
├── main.c          # Sudoku generation, solving, game loop and UI
├── README.md       # Project documentation
├── Makefile        # Build and run helpers
└── .gitignore      # Generated/build artifacts
```

## 🚀 Installation & Setup

### Ubuntu / Debian / WSL

Install GCC and ncurses:

```bash
sudo apt update
sudo apt install build-essential libncurses-dev
```

Clone the repository:

```bash
git clone https://github.com/shivamparth123/Sud-O-Ku.git
cd Sud-O-Ku
```

Build:

```bash
make
```

Run:

```bash
./sudoku
```

Or directly:

```bash
gcc -Wall -Wextra -O2 main.c -lncurses -o sudoku
./sudoku
```

Clean the executable:

```bash
make clean
```

## 🖥️ Windows

The program uses the curses API, so a compatible curses implementation such as **PDCurses** is required for native Windows builds. The code also contains Windows-specific screen-clearing logic, but the curses dependency still needs to be configured separately.

For the simplest setup, running the project through **WSL/Ubuntu** is recommended.

## 🔍 Current Limitations

This is a compact educational implementation. Some areas can be improved further:

- Puzzle generation does not explicitly test for **unique solutions** after removing clues.
- The solver uses the first available empty cell instead of MRV/constraint propagation heuristics.
- The terminal UI depends on a curses-compatible environment.
- The current implementation keeps the game state in memory rather than saving/resuming sessions.
- The code is contained primarily in a single `main.c` file and could be modularized into generation, solving, UI, and game-state components.

## 🚧 Possible Improvements

Future versions could add:

- Unique-solution verification during puzzle generation
- MRV / most-constrained-cell heuristic
- Forward checking and constraint propagation
- Difficulty estimation based on solving complexity rather than clue count alone
- Persistent game save/load
- High-score and completion-time tracking
- Better cross-platform terminal support
- Modular source files (`solver.c`, `generator.c`, `ui.c`, etc.)
- Automated unit tests for Sudoku validity and solver correctness

## 🎯 Learning Outcomes

This project demonstrates practical use of:

- C programming
- Recursion
- Backtracking algorithms
- 2D arrays
- Constraint checking
- Randomized puzzle generation
- Terminal UI programming
- Keyboard event handling
- Basic algorithmic complexity reasoning

## 📌 Academic / Portfolio Note

This repository is best presented as a **C-based algorithms and terminal-UI project**. For a resume, emphasize the parts you personally implemented or substantially modified rather than claiming the entire fork as original work.

## 📄 License / Attribution

This repository is a fork of `Levi477/Sud-O-Ku`. Please refer to the original repository and its licensing/attribution terms before redistributing or relicensing the code.

Original project:
https://github.com/Levi477/Sud-O-Ku
