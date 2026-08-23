# Sudoku — Terminal-Based C Game

A terminal-based Sudoku game written in C using the ncurses library. The program generates a randomized Sudoku board, can solve the generated puzzle automatically, and also provides an interactive mode where the user can solve it manually.

## Features

- Random Sudoku generation
- Automatic Sudoku solving using recursive backtracking
- Interactive manual-solving mode
- Arrow-key navigation in the terminal
- Four difficulty levels: Easy, Medium, Hard, and Very Hard
- Elapsed-time display while solving
- Input validation using row, column, and 3×3 box constraints
- Option to reveal the solution after the 10-minute challenge period
- Color-based terminal interface using ncurses

## How It Works

### Sudoku Generation

The program first creates a completed 9×9 Sudoku grid. It initializes selected 3×3 regions with random values and then uses the Sudoku solver to complete the remaining cells.

After a complete board is generated, cells are removed according to the selected difficulty level to create the puzzle shown to the user.

### Automatic Solver

The computer solves the puzzle using recursive backtracking:

```text
Find an empty cell
        ↓
Try numbers from 1 to 9
        ↓
Check row, column and 3×3 box
        ↓
Place a valid number
        ↓
Recursively solve the remaining cells
        ↓
If no solution is possible, undo and try another number
```

### Manual Mode

In manual mode, the user moves around the Sudoku grid using the arrow keys. A value can be entered only if it satisfies the current row, column, and 3×3 box constraints.

## Difficulty Levels

| Level | Clues | Cells Removed |
|---|---:|---:|
| Easy | 35 | 46 |
| Medium | 28 | 53 |
| Hard | 22 | 59 |
| Very Hard | 17 | 64 |

The current implementation determines difficulty from the number of clues remaining. It does not explicitly check whether every generated puzzle has a unique solution.

## Controls

| Key | Action |
|---|---|
| Up Arrow | Move up |
| Down Arrow | Move down |
| Left Arrow | Move left |
| Right Arrow | Move right |
| Enter | Enter a value in the selected empty cell |
| `q` | Quit manual-solving mode |

## Algorithm

The solver uses a standard recursive backtracking algorithm.

For every empty cell, it tries the numbers 1–9 and checks whether the number can safely be placed by verifying:

1. The current row
2. The current column
3. The current 3×3 sub-grid

If a valid number is placed, the solver recursively continues with the next empty cell. If it reaches a state where no valid number can be placed, it backtracks and tries another possibility.

The implementation uses a straightforward first-empty-cell strategy and does not currently use advanced techniques such as Minimum Remaining Values (MRV).

## Complexity

Backtracking has exponential worst-case complexity for general Sudoku solving. Actual execution time depends on the puzzle and the order in which candidate values are explored.

## Tech Stack

- C
- ncurses
- GCC
- Recursive backtracking
- Standard C library random-number functions

## Project Structure

```text
Sud-O-Ku/
├── main.c
├── README.md
├── Makefile
└── .gitignore
```

`main.c` contains the Sudoku generation, solving algorithm, game logic, input handling, timer, and terminal interface.

## Setup

### Ubuntu / Debian / WSL

Install the required tools:

```bash
sudo apt update
sudo apt install build-essential libncurses-dev
```

Clone the repository:

```bash
git clone https://github.com/shivamparth123/Sud-O-Ku.git
cd Sud-O-Ku
```

Build the project:

```bash
make
```

Run it:

```bash
./sudoku
```

You can also compile directly:

```bash
gcc -Wall -Wextra -O2 main.c -lncurses -o sudoku
./sudoku
```

To remove the compiled executable:

```bash
make clean
```

## Windows

The program uses the curses API, so native Windows execution requires a compatible curses implementation such as PDCurses. Using WSL with Ubuntu is another straightforward option.

## Limitations

The current implementation is intentionally simple and can be improved in several ways:

- Puzzle generation does not verify that a puzzle has exactly one solution.
- The solver uses the first empty cell rather than more advanced cell-selection heuristics.
- The game state is not saved between sessions.
- The source code is primarily contained in one C file.
- The terminal interface depends on a curses-compatible environment.

## Possible Improvements

- Add unique-solution verification during puzzle generation
- Improve the solver with MRV and constraint-propagation techniques
- Add save/load functionality
- Add score and completion-time tracking
- Separate the solver, generator, and UI into different source files
- Add automated tests for Sudoku generation and solving
- Improve cross-platform terminal support

## What This Project Demonstrates

This project provides practice with:

- C programming
- Recursion and backtracking
- 2D arrays
- Constraint checking
- Randomized puzzle generation
- Terminal-based user interfaces
- Keyboard input handling
- Basic algorithmic complexity

## Attribution

This repository is a fork of the original `Levi477/Sud-O-Ku` project. The fork relationship is preserved on GitHub. Resume and portfolio descriptions should accurately represent the changes and contributions made to this repository.

Original repository:
https://github.com/Levi477/Sud-O-Ku
