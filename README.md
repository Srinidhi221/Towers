# Towers Puzzle Game

A competitive implementation of the classic Towers (Skyscrapers) logic puzzle with CPU opponents using different strategic approaches.

## About

Towers is a 4×4 logic puzzle where players must place numbers 1-4 in each cell following specific rules. This version adds turn-based competitive gameplay where you face off against a CPU opponent that can switch between four different decision-making strategies.

## Rules

The puzzle follows standard Towers constraints:
- Each row contains numbers 1-4 exactly once
- Each column contains numbers 1-4 exactly once
- Edge clues show how many towers are visible from that direction (taller towers block shorter ones)

### Scoring System
- Correct placement: +10 points
- Complete a row/column: +20 bonus
- Invalid move: -5 lives
- Each player starts with 100 lives

### Victory Conditions
The game ends when the board is complete or a player runs out of lives. The winner is determined by:
1. Lives remaining (player alive wins)
2. Higher score
3. If tied, it's a draw

## CPU Strategies

The CPU can use four different approaches:

**Lives-Greedy (Survival)** - Focuses on safe moves to preserve lives. Prefers cells with fewer possible values to minimize risk.

**Completion-Greedy (Rusher)** - Prioritizes finishing nearly-complete rows and columns quickly.

**Score-Greedy (Gambler)** - Goes for high-scoring opportunities even if riskier.

**Constraint-Greedy (MRV)** - Uses the Minimum Remaining Values heuristic to tackle the most constrained cells first.

Each strategy shows a different colored heat map indicating which cells it considers high-priority.

## Features

- Real-time heat map showing CPU decision process
- Switch strategies mid-game to change AI behavior
- Clean dark-themed interface
- Move validation with visual feedback
- Reasoning panel explaining CPU moves

## Running the Game

### Requirements
- Java JDK 8 or higher

### Compilation
```bash
javac game/*.java
```

### Execution
```bash
java game.TowersssGameGUI
```

## Project Structure
```
game/
├── TowersssGameGUI.java      # Main game window and controls
├── GameState.java             # Game logic and validation
├── PuzzleGenerator.java       # Creates valid puzzle configurations
├── StrategyLives.java         # Survival strategy
├── StrategyCompletion.java    # Completion strategy
├── StrategyScore.java         # Score-maximizing strategy
└── StrategyMRV.java          # Constraint-based strategy
```

## How to Play

1. Click any empty cell on your turn
2. Select a value from the popup (grayed out values are invalid)
3. Watch the CPU analyze the board with the heat map
4. Try to outscore and outlast the CPU

You can change the CPU strategy anytime using the dropdown menu. The heat map can be toggled on/off.

## Understanding Greedy Algorithms and Their Limitations

Greedy algorithms select the locally optimal choice at each step without considering future consequences. In the Towers puzzle, each strategy evaluates available moves and immediately commits to the highest-scoring option. While computationally efficient, this approach does not guarantee optimal solutions. For example, Completion-Greedy may rush to finish a row that violates visibility rules, incurring penalties, while Lives-Greedy may play too conservatively and score minimal points. These limitations arise because greedy algorithms cannot reconsider decisions or anticipate downstream effects of current choices.

## Greedy Algorithms as Practical Heuristics

In this project, greedy algorithms function as heuristics that provide reasonable solutions quickly rather than guaranteed optimal outcomes. The four strategies demonstrate varied problem-solving approaches suitable for real-time gameplay. Achieving truly optimal solutions would require exhaustive methods like backtracking that explore all possible sequences. Greedy heuristics offer a practical trade-off between solution quality and speed, making them valuable for interactive applications. This implementation effectively demonstrates how greedy approaches address constraint satisfaction problems while maintaining the distinction between heuristic adequacy and mathematical optimality.

## Limitations

- Fixed 4×4 board size
- No undo functionality
- Heat map animation speed cannot be adjusted

## Possible Improvements

- Larger grid options (5×5, 6×6)
- Hint system for difficult moves
- Move history tracking
- Minimax or alpha-beta pruning strategies
- Multiplayer network mode
