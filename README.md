# Synaptic Wars - Neuro Engine

## Table of Contents
- [Overview](#overview)
- [Architecture](#architecture)
- [Core Components](#core-components)
- [Neuro-Engine](#neuro-engine)
- [Gameplay](#gameplay)
- [API Documentation](#api-documentation)
- [Setup and Installation](#setup-and-installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [Troubleshooting](#troubleshooting)
- [Development Guidelines](#development-guidelines)

## Overview

Synaptic Wars is an innovative neuro-adaptive game that uses simulated EEG data to dynamically adjust gameplay mechanics based on the player's emotional state. The system creates a personalized gaming experience by analyzing brainwave patterns and modifying difficulty, pacing, rewards, and enemy behavior in real-time.

### Key Features
- **Neuro-Adaptive AI**: Adjusts difficulty and pacing based on emotional state
- **Real-time Emotional Analysis**: Processes EEG data for emotional state detection
- **Adaptive Gameplay**: Modifies enemy behavior, ability cooldowns, and spawn rates
- **Neuro-Enhanced Enemies**: Tau Tanglers adapt their behavior based on player emotional state
- **Adaptive Abilities**: Player abilities change effectiveness based on emotional state
- **Live Dashboard**: Visualizes emotional states, adaptations, and performance metrics
- **EEG Simulation**: Mode-switchable brainwave data for testing without hardware

## Architecture

The application follows a clean, modular architecture with distinct layers:

```
synaptic-wars-mvp/
├── config.js                 # Game configuration
├── main.js                   # Application entry point
├── index.html                # Main HTML structure
├── core/                     # Core engine components
│   ├── game.js              # Main game loop and state management
│   ├── renderer.js          # Canvas rendering system
│   ├── event-bus.js         # Central event system
│   └── input-handler.js     # Keyboard input handling
├── neuro-engine/            # Neuro-adaptive AI system
│   ├── eeg-simulator.js     # EEG data simulation
│   ├── emotional-director.js # Emotional state analysis
│   ├── neuro-adaptive-engine.js # Game adaptation engine
│   └── neuro-bridge.js      # DeepSeek API interface
├── gameplay/                # Game-specific mechanics
│   ├── neuro-enhanced-tanglers.js # Adaptive enemy system
│   └── adaptive-abilities.js # Dynamic ability system
└── ui/                      # User interface components
    └── neuro-dashboard-enhanced.js # Neuro dashboard component
```

### Architecture Diagram

```
┌─────────────────────────────────────────────────────────┐
│                   Main Application                      │
├─────────────────────────────────────────────────────────┤
│ main.js → Game (core/game.js) → Renderer (renderer.js) │
│         ↓                                              │
│  ┌─────────────────┐                                   │
│  │   Input Handler │                                   │
│  └─────────────────┘                                   │
├─────────────────────────────────────────────────────────┤
│                    Neuro Engine                        │
├─────────────────────────────────────────────────────────┤
│  EEG Simulator  ←→  Emotional Director  ←→  Neuro Bridge │
│                       ↓                                  │
│            Neuro Adaptive Engine                        │
├─────────────────────────────────────────────────────────┤
│                    Gameplay Layer                       │
├─────────────────────────────────────────────────────────┤
│  Neuro-Enhanced Tanglers  ↔  Adaptive Abilities        │
├─────────────────────────────────────────────────────────┤
│                     UI Layer                            │
├─────────────────────────────────────────────────────────┤
│             Neuro Dashboard Enhanced                    │
└─────────────────────────────────────────────────────────┘
```

## Core Components

### Game (core/game.js)
The central game class manages the main game loop, state, and coordinates with the neuro-engine.

**Key Responsibilities:**
- Manages main game loop (update/render cycle)
- Coordinates with input handler and neuro-engine
- Handles player movement and ability usage
- Manages tangler spawning and state
- Updates game state based on neuro-adaptations

**Methods:**
- `initializeNeuroEngine()` - Sets up neuro-engine components
- `start()` - Starts the game
- `update(deltaTime)` - Updates game state each frame
- `handleEEGUpdate(eegData)` - Processes emotional data and applies adaptations
- `useAbility(abilityName)` - Activates player abilities
- `getTanglerData()` - Returns tangler data for rendering
- `setEEGMode(mode)` - Changes EEG simulation mode

### Renderer (core/renderer.js)
Handles the visual rendering of the game state to the canvas.

**Key Responsibilities:**
- Draws player and tanglers on the canvas
- Converts 3D world coordinates to screen coordinates
- Renders health bars for tanglers
- Adjusts rendering based on tangler behavior

### Event Bus (core/event-bus.js)
A central event system that allows different components to communicate without direct dependencies.

**Key Responsibilities:**
- Subscribing components to events
- Publishing events to subscribed components
- Decoupling system components

**Methods:**
- `subscribe(event, callback)` - Subscribe to an event
- `publish(event, data)` - Publish an event with data

### Input Handler (core/input-handler.js)
Manages keyboard input for player movement and ability activation.

**Key Responsibilities:**
- Captures keyboard events
- Tracks pressed keys
- Provides interface for checking key states

**Methods:**
- `isKeyPressed(keyCode)` - Check if a specific key is currently pressed

## Neuro-Engine

The neuro-engine is the core AI system that adapts gameplay based on emotional states. It consists of four interconnected components:

### EEG Simulator (neuro-engine/eeg-simulator.js)
Simulates realistic EEG data streams with different emotional states.

**Key Features:**
- Mode-based simulation (focused, relaxed, stressed, dynamic)
- Realistic brainwave data (alpha, beta, theta, delta, gamma)
- Dynamic data variations

**Methods:**
- `connect()` - Connects the simulator
- `disconnect()` - Disconnects the simulator
- `setSimulationMode(mode)` - Changes the simulation mode
- `getCurrentData()` - Gets current EEG data
- `setDataUpdateHandler(callback)` - Sets callback for data updates

### Emotional Director (neuro-engine/emotional-director.js)
Analyzes EEG data to determine emotional states and generates adaptation strategies.

**Key Responsibilities:**
- Processes EEG data to determine emotional state
- Maintains emotional state history
- Generates adaptation strategies based on emotional state
- Creates recommendations for the player

**Methods:**
- `processPlayerState(eegData, gameState)` - Processes emotional state
- `generateAdaptations(emotionalState)` - Creates gameplay adaptations
- `getEmotionalTrend()` - Returns emotional state trend
- `generateRecommendations(emotionalState)` - Creates player recommendations

### Neuro Adaptive Engine (neuro-engine/neuro-adaptive-engine.js)
Applies neuro-adaptations to the game state based on emotional analysis.

**Key Responsibilities:**
- Applies gameplay modifications based on emotional state
- Tracks adaptation performance metrics
- Manages adaptation history
- Provides fallback mechanisms

**Methods:**
- `applyAdaptations(gameState, eegData)` - Applies adaptations to game state
- `getPerformanceReport()` - Returns performance metrics
- `reset()` - Resets adaptation history
- `adaptGameState(gameState, adaptations)` - Adapts the game state

### Neuro Bridge (neuro-engine/neuro-bridge.js)
Interface to DeepSeek API for emotional analysis (simulated in MVP).

**Key Responsibilities:**
- Communicates with DeepSeek API
- Processes emotional analysis requests
- Handles API responses and error states

**Methods:**
- `initialize()` - Initializes the bridge
- `processEmotionalState(eegData, gameState)` - Processes emotional state analysis

## Gameplay

### Neuro-Enhanced Tanglers (gameplay/neuro-enhanced-tanglers.js)
Enemies that adapt their behavior based on the player's emotional state.

**Key Features:**
- Behavior adaptation based on emotional state (aggressive, defensive, strategic, erratic)
- Dynamic spawning and health adjustments
- Entanglement mechanics for ability interactions
- Calm effects that reduce aggression

**Methods:**
- `spawnTangler(position)` - Spawns a new tangler
- `updateTanglers(deltaTime, playerPosition)` - Updates all tanglers
- `applyDamage(tanglerId, damage)` - Applies damage to a tangler
- `updateAdaptationSettings(adaptations)` - Updates adaptation settings
- `activateEntanglement(duration)` - Activates quantum entanglement effect
- `applyCalm(seconds)` - Applies calming effect to tanglers

### Adaptive Abilities (gameplay/adaptive-abilities.js)
Player abilities that adjust their effectiveness based on emotional state.

**Key Features:**
- Cooldown adjustments based on emotional state
- Effectiveness scaling based on emotional intensity
- Dynamic energy costs based on emotional state
- Multiple ability types with unique effects

**Methods:**
- `updateAbilities(deltaTime)` - Updates ability states
- `activateAbility(abilityName, playerEnergy)` - Activates an ability
- `getAbilityInfo(abilityName)` - Gets ability information
- `getAllAbilitiesInfo()` - Gets information for all abilities
- `resetCooldowns()` - Resets all ability cooldowns

## API Documentation

### Game API

#### Game States
- `score`: Current player score
- `level`: Current game level
- `playerEnergy`: Current player energy
- `maxEnergy`: Maximum player energy
- `playerPosition`: Current player position (x, y, z)
- `difficultyMultiplier`: Current difficulty multiplier
- `spawnRateMultiplier`: Current spawn rate multiplier
- `rewardMultiplier`: Current reward multiplier
- `gameActive`: Whether the game is currently active

#### Events
- `startGame`: Starts the game
- `useAbility`: Activates an ability (data: ability name)
- `setEEGMode`: Sets EEG simulation mode (data: mode)
- `gameStarted`: Triggered when game starts
- `gameStateUpdate`: Published with game state updates

#### Abilities
- `dendritic_lightning`: Damage ability
  - Base cooldown: 3.0s
  - Base cost: 20 energy
  - Base damage: 50
- `serotonin_tsunami`: Healing/defensive ability
  - Base cooldown: 5.0s
  - Base cost: 30 energy
  - Base healing: 25
- `quantum_entanglement`: Utility ability
  - Base cooldown: 8.0s
  - Base cost: 40 energy
  - Base duration: 4.0s

## Setup and Installation

### Prerequisites
- Modern web browser (Chrome, Firefox, Safari, Edge)
- Python 3.x (for local server option) - optional but recommended

### Installation Steps
1. Clone or download the repository to your local machine
2. Ensure all files are present in the synaptic-wars-mvp directory
3. The application can be run directly in a browser or via a local server

## Configuration

All game configuration is managed through the `config.js` file:

```javascript
export const config = {
    player: {
        moveSpeed: 2.5,
        initialEnergy: 100,
        maxEnergy: 100,
        energyRecoveryRate: 10, // per second
    },
    game: {
        baseSpawnInterval: 5, // seconds
        minTanglerCount: 2,
    },
    abilities: {
        dendritic_lightning: {
            name: 'Dendritic Lightning',
            baseCooldown: 3.0,
            baseCost: 20,
            baseDamage: 50,
            description: 'Electrifies Tau Tanglers with neural impulses',
        },
        serotonin_tsunami: {
            name: 'Serotonin Tsunami',
            baseCooldown: 5.0,
            baseCost: 30,
            baseHealing: 25,
            description: 'Releases healing energy that calms neural environment',
        },
        quantum_entanglement: {
            name: 'Quantum Entanglement',
            baseCooldown: 8.0,
            baseCost: 40,
            baseDuration: 4.0,
            description: 'Creates quantum links between Tau Tanglers',
        },
    },
    tangler: {
        baseHealth: 100,
        scoreValue: 10,
        baseMoveSpeed: 0.01,
        erraticThreshold: 0.3, // Health percentage below which behavior becomes erratic
        erraticSpeedMultiplier: 1.5,
        entanglement: {
            splashDamageMultiplier: 0.5,
            splashSpeedMultiplier: 1.2,
        }
    }
};
```

## Running the Application

### Direct Browser Method
1. Open `index.html` directly in your web browser
2. The application will load with a loading screen
3. The game will auto-start after 2 seconds or you can click "Begin Neural Journey"

### Local Server Method (Recommended)
1. Navigate to the synaptic-wars-mvp directory in your terminal
2. Start a local server:
   - For Python 3: `python -m http.server 8000`
   - For Python 2: `python -m SimpleHTTPServer 8000`
3. Open `http://localhost:8000` in your browser
4. Navigate to the index.html page

### Controls
- **Movement**: W, A, S, D keys
- **Abilities**:
  - Q: Dendritic Lightning (damage)
  - W: Serotonin Tsunami (healing/support)
  - E: Quantum Entanglement (utility)
- **EEG Modes**: Click on the Focused/Relaxed/Stressed/Dynamic buttons

## Troubleshooting

### Common Issues
- **Blank page or module errors**: Use the local server method instead of opening directly in browser
- **Slow updates**: The dashboard refreshes once per second by design; check console logs for activity
- **Controls not responding**: Ensure the game window is focused and keys are properly recognized
- **No visual changes**: Check that WebGL is enabled in your browser

### Debugging Process
1. Open browser developer tools (F12)
2. Check the Console tab for error messages
3. Look for network errors in the Network tab
4. Ensure all .js files are loading properly

## Development Guidelines

### Code Structure
- Follow the existing modular architecture
- Maintain separation of concerns between layers
- Use the event bus for communication between modules
- Keep methods focused and single-purpose

### Adding New Features
1. Identify which layer your feature belongs to
2. Create a new module or extend an existing one
3. Update the event system as needed to connect components
4. Update the documentation to describe the new functionality
5. Add tests to ensure the new functionality works as expected

### Testing
- Thoroughly test new features with the different EEG modes
- Verify that neuro-adaptations work as expected
- Ensure the game remains playable across different emotional states
- Test with the various ability combinations

### Performance Considerations
- Optimize rendering to maintain good frame rates
- Limit the number of active tanglers if performance degrades
- Keep the adaptation logic efficient to avoid frame drops
- Consider the performance impact of real-time emotional analysis

## Future Enhancements

### Planned Features
- Integration with real EEG hardware
- Advanced behavioral patterns for tanglers
- More complex adaptation strategies
- Analytics dashboard for emotional data
- Machine learning for better emotional state prediction

### Potential Improvements
- Enhanced visual effects for abilities
- Multiplayer support with social neuro-adaptation
- Mobile-friendly interface
- Accessibility options for different abilities
- Extended gameplay mechanics

## Contributing

1. Fork the repository
2. Create a new branch for your feature
3. Make your changes following the code structure and conventions
4. Submit a pull request with a detailed description of your changes

## License

This project is licensed under the MIT License - see the LICENSE file for details.