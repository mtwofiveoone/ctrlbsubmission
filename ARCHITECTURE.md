# CTRL+B Technical Architecture

## Overview

CTRL+B is a strategic 4x4 grid game built as a LUKSO Universal Profile Mini-App. The game combines traditional grid-based gameplay with blockchain integration, allowing players to earn achievements and register wins on the LUKSO blockchain.

## System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        CTRL+B Application                        │
├─────────────┬─────────────────────────────┬─────────────────────┤
│             │                             │                     │
│  Frontend   │         Game Engine         │  Blockchain Layer   │
│             │                             │                     │
├─────────────┼─────────────────────────────┼─────────────────────┤
│ - Astro.js  │ - GridGame.ts               │ - LuksoService.ts   │
│ - HTML/CSS  │ - GameAI.ts                 │ - UP Integration    │
│ - UI/UX     │ - GameScene.ts              │ - NFT Contract      │
│             │ - Character Dialogues       │                     │
├─────────────┼─────────────────────────────┼─────────────────────┤
│             │                             │                     │
│ Data Layer: │        FirebaseService      │    Browser Storage  │
│             │                             │                     │
└─────────────┴─────────────────────────────┴─────────────────────┘
```

## Component Breakdown

### 1. Frontend Layer

The frontend is built using Astro.js, a modern static site builder, with a focus on performance and developer experience.

**Key Components:**
- **Layout.astro**: Defines the base HTML structure and metadata
- **Pages**:
  - **index.astro**: Main game interface
  - **achievements.astro**: Displays player achievements
  - **tutorial.astro**: Interactive game tutorial

The UI is designed to be responsive and supports both standalone web application mode and mini-app mode within the LUKSO ecosystem.

### 2. Game Engine

The core game logic is implemented in TypeScript, providing a robust and type-safe foundation.

**Key Components:**
- **GridGame.ts**: Core game mechanics, board state management, move validation
- **GameAI.ts**: AI opponent
- **GameUI.ts**: Manages game UI elements and animations
- **Character Dialogues**: Provides personality to AI opponents through:
  - BeforeGameDialogues.ts
  - DialogueOptions.ts
  - GameOutcomeDialogues.ts

### 3. Blockchain Integration

CTRL+B integrates with the LUKSO blockchain, allowing for Universal Profile authentication and NFT achievements.

**Key Components:**
- **LuksoService.ts**: Core service for LUKSO blockchain interactions
  - Universal Profile authentication
  - Transaction handling
  - Win registration
- **LuksoUI.ts**: UI components for blockchain interactions
- **NFT Contract Integration**: Allows minting of achievement NFTs

### 4. Data Persistence

**Key Components:**
- **FirebaseService.ts**: Cloud-based data storage for:
  - Player statistics
  - Achievement tracking
  - Leaderboards
- **Browser Storage**: Local storage for game state and session management

## Data Flow

```
┌──────────┐    ┌───────────┐    ┌────────────┐    ┌──────────────┐
│  Player  │───►│  GameUI   │───►│  GridGame  │───►│  LuksoService │
└──────────┘    └───────────┘    └────────────┘    └──────────────┘
      │               │                │                   │
      │               │                │                   │
      │               │                │                   ▼
      │               │                │           ┌──────────────┐
      │               │                │           │  LUKSO       │
      │               │                │           │  Blockchain  │
      │               │                │           └──────────────┘
      │               │                │                   ▲
      │               │                │                   │
      │               │                ▼                   │
      │               │         ┌────────────┐            │
      │               └────────►│  GameAI    │            │
      │                         └────────────┘            │
      │                                                   │
      ▼                                                   │
┌──────────────┐                                  ┌──────────────┐
│  Firebase    │◄─────────────────────────────────┤ Achievement  │
│  Database    │                                  │ System       │
└──────────────┘                                  └──────────────┘
```

## Key Interactions

1. **Game Initialization**:
   - Player loads the application
   - GameUI initializes the game board
   - LuksoService checks for Universal Profile connection
   - Character selection and dialogue initialization

2. **Gameplay Loop**:
   - Player makes a move on the grid
   - GridGame validates and processes the move
   - GameAI calculates and executes response (if playing against AI)
   - UI updates with new game state and character dialogues
   - Scores are calculated and displayed

3. **Win Registration**:
   - When a game concludes, the winner is determined
   - If connected to LUKSO, win is registered on the blockchain
   - FirebaseService updates player statistics
   - Achievement system checks for unlocked achievements

4. **Achievement System**:
   - Player actions trigger achievement checks
   - Unlocked achievements are displayed to the player
   - NFT achievements can be minted on the LUKSO blockchain
   - Achievement progress is stored in Firebase

## Technical Specifications

### Frontend
- **Framework**: Astro.js
- **Styling**: CSS with animations
- **Responsiveness**: Supports both desktop and mobile views

### Game Engine
- **Language**: TypeScript
- **State Management**: Custom state management in GridGame.ts
- **AI Difficulty Levels**: Easy, Medium, Hard

### Blockchain Integration
- **Network**: LUKSO Mainnet
- **Standards**: LSP0 (Universal Profile), LSP7/LSP8 (Digital Assets)
- **Authentication**: Universal Profile Browser Extension

### Data Storage
- **Cloud Database**: Firebase Firestore
- **Local Storage**: Browser localStorage for session persistence
- **Blockchain Storage**: On-chain storage for wins and achievements

## Security Considerations

- Firebase Security Rules protect user data
- Client-side validation with server-side verification for achievements
- Environment variables for sensitive configuration
- Proper error handling for blockchain transactions

## Deployment Architecture

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│                 │     │                 │     │                 │
│  Static Assets  │────►│  CDN/Hosting    │◄────│  User Browser   │
│                 │     │                 │     │                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘
                                │                        │
                                ▼                        │
                        ┌─────────────────┐             │
                        │                 │             │
                        │  Firebase       │◄────────────┘
                        │                 │
                        └─────────────────┘
                                │
                                ▼
                        ┌─────────────────┐
                        │                 │
                        │  LUKSO Network  │
                        │                 │
                        └─────────────────┘
```

## Mini-App Integration

CTRL+B is designed to function as a LUKSO Universal Profile Mini-App, which allows it to:

1. Be embedded within Universal Profile interfaces
2. Access the hosting Universal Profile's context
3. Interact with the blockchain on behalf of the user (with permission)
4. Register wins and achievements directly to the user's Universal Profile

The Mini-App integration is handled through the LuksoService, which detects whether the application is running in a Mini-App context and adjusts its behavior accordingly.

## Conclusion

CTRL+B represents a modern approach to blockchain gaming, combining traditional game mechanics with blockchain integration. The architecture is designed to be modular, allowing for easy maintenance and future expansion. The integration with LUKSO's Universal Profiles provides a seamless user experience while leveraging blockchain technology for achievements and win registration. 
