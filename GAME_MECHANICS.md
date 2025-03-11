# CTRL+B Game Mechanics

## Game Board

CTRL+B is played on a 4x4 grid, where each cell can contain stacks of red or blue pieces.

```
┌─────┬─────┬─────┬─────┐
│     │     │     │     │
│  0  │  1  │  2  │  3  │
│     │     │     │     │
├─────┼─────┼─────┼─────┤
│     │     │     │     │
│  4  │  5  │  6  │  7  │
│     │     │     │     │
├─────┼─────┼─────┼─────┤
│     │     │     │     │
│  8  │  9  │ 10  │ 11  │
│     │     │     │     │
├─────┼─────┼─────┼─────┤
│     │     │     │     │
│ 12  │ 13  │ 14  │ 15  │
│     │     │     │     │
└─────┴─────┴─────┴─────┘
```

## Cell Structure

Each cell in the grid contains a 3x3 inner grid that can be filled with pieces:

```
┌───────────────┐
│ ┌───┬───┬───┐ │
│ │ 0 │ 1 │ 2 │ │
│ ├───┼───┼───┤ │
│ │ 3 │ 4 │ 5 │ │
│ ├───┼───┼───┤ │
│ │ 6 │ 7 │ 8 │ │
│ └───┴───┴───┘ │
└───────────────┘
```

## Stacking Mechanics

1. **Basic Placement**: Players take turns placing their pieces (red or blue) in empty cells.

2. **Stacking Levels**:
   - Level 1: Single piece in a cell
   - Level 2: Two pieces stacked in the same position
   - Level 3: Three pieces stacked in the same position (maximum)

3. **Visual Representation**:

```
Level 1 (Single Piece):    Level 2 (Stacked):    Level 3 (Max Stack):
┌───────────────┐         ┌───────────────┐     ┌───────────────┐
│ ┌───┬───┬───┐ │         │ ┌───┬───┬───┐ │     │ ┌───┬───┬───┐ │
│ │   │ R │   │ │         │ │   │RR │   │ │     │ │   │RRR│   │ │
│ ├───┼───┼───┤ │         │ ├───┼───┼───┤ │     │ ├───┼───┼───┤ │
│ │ B │   │   │ │         │ │ B │   │BB │ │     │ │ B │   │BBB│ │
│ ├───┼───┼───┤ │         │ ├───┼───┼───┤ │     │ ├───┼───┼───┤ │
│ │   │   │   │ │         │ │   │ R │   │ │     │ │   │RRR│   │ │
│ └───┴───┴───┘ │         │ └───┴───┴───┘ │     │ └───┴───┴───┘ │
└───────────────┘         └───────────────┘     └───────────────┘
```

## Push Mechanics

When a cell is completely filled (all 9 positions), it triggers a "push" to adjacent cells:

```
Before Push:                     After Push:
┌─────┬─────┬─────┐             ┌─────┬─────┬─────┐
│     │     │     │             │     │  B  │     │
│     │  B  │     │             │     │     │     │
│     │     │     │             │     │  R  │     │
├─────┼─────┼─────┤             ├─────┼─────┼─────┤
│     │ BBB │     │             │  B  │     │  B  │
│  R  │ RRR │     │  ──────►    │     │     │     │
│     │ BBB │     │             │     │     │  R  │
├─────┼─────┼─────┤             ├─────┼─────┼─────┤
│     │     │     │             │     │  B  │     │
│     │  R  │     │             │     │     │     │
│     │     │     │             │     │  R  │     │
└─────┴─────┴─────┘             └─────┴─────┴─────┘
```

1. When a cell is filled, the pieces are pushed to the four adjacent cells (up, right, down, left).
2. The color with the majority in the filled cell determines which color gets pushed.
3. If there's a tie, both colors are pushed.

## Scoring

Scoring is based on the number and level of stacks:

1. **Level 1 Stack**: 1 point per piece
2. **Level 2 Stack**: 3 points per stack
3. **Level 3 Stack**: 9 points per stack

Example scoring calculation:
```
┌─────┬─────┬─────┬─────┐
│ R   │ RR  │ B   │ RRR │
│     │     │     │     │
│     │     │     │     │
├─────┼─────┼─────┼─────┤
│     │ B   │ BBB │     │
│     │     │     │     │
│     │     │     │     │
├─────┼─────┼─────┼─────┤
│ RR  │     │ BB  │     │
│     │     │     │     │
│     │     │     │     │
├─────┼─────┼─────┼─────┤
│     │ R   │     │ B   │
│     │     │     │     │
│     │     │     │     │
└─────┴─────┴─────┴─────┘

Red Score: 1 + 3 + 9 + 3 + 1 = 17 points
Blue Score: 1 + 9 + 3 + 1 = 14 points
```

## Winning the Game

The game ends when:

1. The entire board is filled, or
2. A predetermined number of moves has been played

The player with the highest score wins. In case of a tie, the game is declared a draw.

## Character System

CTRL+B features six unique AI characters, each with their own personality and dialogue:

1. **Sharon**: Chaotic and passionate
2. **Gary**: Critical and condescending
3. **Dev**: Technical and robotic
4. **Satoshi**: Cryptic and philosophical
5. **Alexa**: Rhythmic and musical
6. **Marj**: Bold and fashion-forward

Each character has three sets of dialogues:
- Before-game dialogues
- During-game dialogues
- Game outcome dialogues (victory and defeat)

## Blockchain Integration

When playing with a connected Universal Profile:

1. Wins are registered to the UP Wallet address
2. Achievements can be minted as NFTs
3. Player statistics are tracked and stored

This creates a permanent record of gameplay achievements and allows for potential future rewards and recognition within the LUKSO ecosystem. 
