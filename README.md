# Towers Puzzle Game - 4 Greedy Strategies

A competitive implementation of the classic Towers puzzle (also known as Skyscrapers) where you play against CPU using different strategic approaches.

##  Game Overview

Towers is a logic puzzle where you fill a 4×4 grid with numbers 1-4, ensuring:
- Each number appears exactly once per row
- Each number appears exactly once per column
- The clues around the edges indicate how many "towers" are visible from that direction (taller towers hide shorter ones behind them)

## Game Mechanics

### Scoring System
- **Valid Move**: +1 point, +5 lives
- **Completing a Row/Column**: +2 bonus points per completion
- **Invalid Move**: -5 points, -10 lives

### Win Conditions
The game ends when:
1. The board is full
2. Either player runs out of lives (≤0)
3. No valid moves remain

**Winner is determined by:**
1. If one player has 0 lives → other player wins
2. Highest score
3. If tied on score → most lives remaining
4. If still tied → declared a TIE

## 🤖 AI Strategies

The CPU opponent can use four different greedy strategies, each with its own color-coded heat map:

### 1. **SCORE-GREEDY** (Blue Heat Map) 🔵
**Goal**: Maximize immediate points
- **Formula**: `Utility = 2.0 × deltaPoints + 0.5 × deltaLives`
- **Strategy**: Prioritizes moves that complete rows/columns for bonus points
- **When to use**: When ahead in lives and want to build a point lead
- **Weakness**: May sacrifice survival for points

### 2. **LIVES-GREEDY** (Green Heat Map) 🟢
**Goal**: Maximize survival/longevity
- **Formula**: `Utility = 0.5 × deltaPoints + 2.0 × deltaLives`
- **Strategy**: Prioritizes staying alive over scoring
- **When to use**: When low on lives and need to last longer
- **Weakness**: May fall behind in score

### 3. **CONSTRAINT-GREEDY** (Purple Heat Map) 🟣
**Goal**: Solve most constrained cells first (MCV Heuristic)
- **Formula**: `Score = (10.0 / validOptions) × 15.0 + basePoints × 5.0`
- **Strategy**: Tackles cells with fewer valid options before they become impossible
- **When to use**: Complex board states requiring systematic solving
- **Weakness**: May not optimize for score or lives
- **Logic**: "If a cell has only 1 valid option, solve it NOW before it becomes impossible"

### 4. **COMPLETION-GREEDY** (Red Heat Map) 🔴
**Goal**: Complete rows/columns fastest (Aggressive)
- **Formula**: `Score = (10.0/emptyInRow + 10.0/emptyInCol) × 12.0 + basePoints × 8.0`
- **Strategy**: Prioritizes nearly-complete lines to finish them quickly
- **When to use**: For fast visible progress and reducing search space
- **Weakness**: May create difficult constraints elsewhere
- **Logic**: "If a row has 1 empty cell left, filling it completes the row"

##  Heat Map Visualization

Each strategy displays a **color-coded heat map** showing which cells the AI values most:
- **Darker/More Saturated** = Higher priority for AI
- **Lighter/Less Saturated** = Lower priority for AI
- **White** = No valid moves or filled cells

The heat map updates dynamically and animates when the CPU is thinking, giving you insight into the AI's decision-making process.

## HOW TO PLAY

1. **Your Turn**:
   - Click any empty cell
   - Select a value (1-4) from the popup
   - Only valid moves are enabled

2. **CPU Turn**:
   - Watch the heat map animate (if enabled)
   - CPU selects its move based on chosen strategy
   - Status updates show the move result

3. **Strategy Selection**:
   - Change CPU strategy anytime using the dropdown
   - Heat map colors update to match strategy
   - Toggle heat map visibility with checkbox

##  Running the Game

### Prerequisites
- Java JDK 8 or higher
- Java Swing (included in standard JDK)

### Compilation
```bash
javac TowersGameGUI.java
```

### Execution
```bash
java TowersGameGUI
```

## 🏗️ Project Structure

```
TowersGameGUI.java
├── Game State Management
│   ├── grid[][]          # 4×4 board
│   ├── rowUsed[][]       # Track used values per row
│   └── colUsed[][]       # Track used values per column
│
├── UI Components
│   ├── cellButtons[][]   # Grid cells
│   ├── valueButtons[]    # Value selection (1-4)
│   ├── strategyCombo     # Strategy dropdown
│   └── heatMapToggle     # Heat map visibility
│
├── Core Game Logic
│   ├── canPlace()        # Validate moves
│   ├── checkRow()        # Verify row constraints
│   ├── checkCol()        # Verify column constraints
│   └── placeValue()      # Execute moves
│
├── AI System
│   ├── getBest()         # Find optimal move
│   ├── eval()            # Strategy dispatcher
│   ├── evalScore()       # Score-Greedy
│   ├── evalLives()       # Lives-Greedy
│   ├── evalConstraint()  # Constraint-Greedy
│   └── evalCompletion()  # Completion-Greedy
│
└── Visualization
    ├── updateHeatMap()   # Calculate heat values
    ├── animateHeatMap()  # Animate visualization
    └── getHeatColor()    # Strategy-specific colors
```

## Learning Outcomes

This project demonstrates:
- **Graph Representation**: The puzzle as a constraint satisfaction problem
- **Greedy Algorithms**: Four different heuristic approaches
- **Game Theory**: Competitive two-player dynamics
- **UI/UX Design**: Real-time visualization of AI decision-making
- **Java Swing**: Event-driven GUI programming

## 🔧 Technical Features

- **Constraint Validation**: Real-time checking of Towers puzzle rules
- **Dynamic Heat Maps**: Visual feedback on AI priorities
- **Animated Transitions**: Smooth cell-by-cell heat map animation
- **Strategy Comparison**: Switch strategies mid-game to compare
- **Score/Lives System**: Adds competitive pressure beyond puzzle-solving

##  Strategy Comparison

| Strategy | Best For | Weakness | Complexity |
|----------|----------|----------|------------|
| Score-Greedy | Aggressive scoring | Risky with lives | Low |
| Lives-Greedy | Defensive play | Falls behind in points | Low |
| Constraint-Greedy | Complex boards | Not score-optimized | Medium |
| Completion-Greedy | Fast progress | May create dead ends | Medium |

##  Known Issues

- Value buttons may not always properly disable for invalid moves (validation still works)
- Heat map animation delay is fixed at 120ms per cell
- No undo functionality

##  Future Enhancements

- [ ] Minimax or Monte Carlo Tree Search AI
- [ ] Multiple difficulty levels (3×3, 5×5, 6×6 grids)
- [ ] Hint system for players
- [ ] Move history and replay
- [ ] Tournament mode (best of N games)
- [ ] Custom puzzle input
- [ ] Save/Load game state


## 👨‍💻 Author

Created as a demonstration of greedy algorithms and competitive AI strategies in puzzle-solving.

---

**Enjoy the game and may the best strategy win! 🏆**
