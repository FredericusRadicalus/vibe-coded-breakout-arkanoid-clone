# Code Documentation

This document provides detailed technical documentation for the Breakout Game codebase.

## Table of Contents
1. [Architecture Overview](#architecture-overview)
2. [Game Objects](#game-objects)
3. [Game Loop](#game-loop)
4. [Collision Detection](#collision-detection)
5. [Power-Up System](#power-up-system)
6. [Sound System](#sound-system)
7. [Key Functions](#key-functions)
8. [Extension Guide](#extension-guide)

---

## Architecture Overview

The game uses a **single-file architecture** with all HTML, CSS, and JavaScript in `breakout.html`.

### Core Structure
```
HTML
├── Canvas Element (835x600)
├── UI Controls (score, lives, speed slider)
└── JavaScript Game Engine
    ├── Game State Management
    ├── Object Definitions (paddle, ball, bricks, power-ups)
    ├── Physics Engine
    ├── Collision Detection
    ├── Rendering System
    ├── Input Handling
    └── Audio System
```

### Game State Variables
```javascript
let gameRunning = false;      // Is game active?
let gamePaused = false;       // Is game paused?
let ballLaunched = false;     // Has ball been launched?
let score = 0;                // Current score
let lives = 3;                // Remaining lives
let ballSpeed = 3;            // Current ball speed
let brickRowOffset = 0;       // Brick downward offset (moving bricks malus)
```

---

## Game Objects

### Paddle Object
```javascript
const paddle = {
    width: 100,        // Paddle width in pixels
    height: 15,        // Paddle height in pixels
    x: canvas.width / 2 - 50,  // X position (center)
    y: canvas.height - 40,      // Y position (near bottom)
    speed: 8,          // Movement speed
    dx: 0              // Current velocity
};
```

### Ball Object
```javascript
const ball = {
    x: canvas.width / 2,   // X position
    y: canvas.height / 2,  // Y position
    radius: 8,             // Ball radius
    dx: 0,                 // X velocity
    dy: 0                  // Y velocity
};
```

### Brick Object Structure
```javascript
{
    x: number,          // X position
    baseY: number,      // Base Y position (for moving bricks)
    y: number,          // Current Y position
    status: 1 | 0,      // 1 = visible, 0 = destroyed
    color: string       // Hex color code
}
```

### Power-Up Object Structure
```javascript
{
    x: number,          // X position
    y: number,          // Y position
    width: 30,          // Width
    height: 30,         // Height
    type: string,       // Power-up type identifier
    color: string,      // Hex color code
    symbol: string,     // Display symbol (emoji/char)
    beneficial: boolean,// True if helpful, false if malus
    dy: 2               // Fall speed
}
```

---

## Game Loop

The game uses `requestAnimationFrame` for a smooth 60 FPS loop.

### Update Cycle
```javascript
function update() {
    if (!gameRunning || gamePaused) return;
    
    // 1. Update positions
    movePaddle();
    moveBall();
    moveExtraBalls();
    movePowerUps();
    moveLasers();
    
    // 2. Check collisions
    brickCollision();
    
    // 3. Render frame
    draw();
    
    // 4. Request next frame
    requestAnimationFrame(update);
}
```

### Rendering Order
1. Clear canvas
2. Draw bricks
3. Draw paddle
4. Draw power-ups
5. Draw lasers
6. Draw balls
7. Draw particles
8. Draw power-up indicators

---

## Collision Detection

### Ball-Brick Collision (Directional)
```javascript
// Calculate overlaps on all sides
const overlapLeft = ballRight - brickLeft;
const overlapRight = brickRight - ballLeft;
const overlapTop = ballBottom - brickTop;
const overlapBottom = brickBottom - ballTop;

// Find smallest overlap
const minOverlap = Math.min(overlapLeft, overlapRight, overlapTop, overlapBottom);

// Bounce based on collision direction
if (minOverlap === overlapLeft || minOverlap === overlapRight) {
    ball.dx *= -1;  // Horizontal bounce
} else {
    ball.dy *= -1;  // Vertical bounce
}
```

This prevents the ball from getting stuck between bricks by determining the most likely collision direction.

### Paddle-Ball Collision (Spin Control)
```javascript
// Calculate where on paddle the ball hit (0 to 1)
const hitPos = (ball.x - paddle.x) / paddle.width;

// Convert to angle (-60° to +60°)
const angle = (hitPos - 0.5) * Math.PI / 3;

// Apply angle to velocity
ball.dx = ballSpeed * Math.sin(angle);
ball.dy = -ballSpeed * Math.cos(angle);
```

This gives players control over ball direction based on where it hits the paddle.

---

## Power-Up System

### Power-Up Types Array
```javascript
const powerUpTypes = [
    { 
        type: 'extraLife', 
        color: '#4169E1',      // Royal blue
        symbol: '♥', 
        beneficial: true, 
        chance: 0.03           // 3% spawn chance
    },
    // ... more power-ups
];
```

### Spawn Mechanism
```javascript
function spawnPowerUp(x, y) {
    const totalChance = powerUpTypes.reduce((sum, p) => sum + p.chance, 0);
    const roll = Math.random();
    
    if (roll > totalChance) return;  // No spawn
    
    // Select power-up based on weighted probability
    let cumulative = 0;
    for (let powerUpType of powerUpTypes) {
        cumulative += powerUpType.chance;
        if (roll <= cumulative) {
            powerUps.push({ /* create power-up */ });
            break;
        }
    }
}
```

### Power-Up Application
Each power-up type has specific logic in the `applyPowerUp()` function:

```javascript
switch(powerUp.type) {
    case 'extraLife':
        lives++;
        break;
    
    case 'laser':
        activePowerUps.laser.active = true;
        activePowerUps.laser.endTime = now + 5000;  // 5 seconds
        break;
    
    // ... more cases
}
```

### Timed Power-Ups
Uses timestamps to track duration:
```javascript
activePowerUps.laser = {
    active: false,
    endTime: 0    // Timestamp when effect ends
};

// Later, in game loop:
const now = Date.now();
if (activePowerUps.laser.active && now < activePowerUps.laser.endTime) {
    // Power-up is still active
}
```

---

## Sound System

### Web Audio API Setup
```javascript
const AudioContext = window.AudioContext || window.webkitAudioContext;
const audioCtx = new AudioContext();
```

### Sound Generation Pattern
```javascript
function playSound() {
    // 1. Create oscillator (tone generator)
    const oscillator = audioCtx.createOscillator();
    
    // 2. Create gain node (volume control)
    const gainNode = audioCtx.createGain();
    
    // 3. Connect nodes
    oscillator.connect(gainNode);
    gainNode.connect(audioCtx.destination);
    
    // 4. Configure sound
    oscillator.frequency.value = 200;  // Pitch
    oscillator.type = 'sine';          // Wave shape
    
    // 5. Fade out
    gainNode.gain.setValueAtTime(0.3, audioCtx.currentTime);
    gainNode.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.1);
    
    // 6. Play
    oscillator.start(audioCtx.currentTime);
    oscillator.stop(audioCtx.currentTime + 0.1);
}
```

### Sound Effects Guide
- **Paddle Hit**: 200Hz sine wave, 0.1s duration
- **Wall Bounce**: 300Hz square wave, 0.05s duration  
- **Brick Break**: 800→200Hz sawtooth sweep, 0.15s duration
- **Power-Up**: 400→800Hz (good) or 600→200Hz (bad), 0.2s duration

---

## Key Functions

### createBricks()
Creates the brick grid with proper positioning.
```javascript
function createBricks() {
    for (let row = 0; row < brickInfo.rows; row++) {
        for (let col = 0; col < brickInfo.cols; col++) {
            bricks[row][col] = {
                x: col * (brickInfo.width + brickInfo.padding) + brickInfo.offsetX,
                baseY: row * (brickInfo.height + brickInfo.padding) + brickInfo.offsetY,
                y: row * (brickInfo.height + brickInfo.padding) + brickInfo.offsetY + brickRowOffset,
                status: 1,
                color: brickColors[row]
            };
        }
    }
}
```

### resetBall()
Returns ball to starting position on paddle.
```javascript
function resetBall() {
    ball.x = canvas.width / 2;
    ball.y = canvas.height / 2;
    ball.dx = 0;
    ball.dy = 0;
    ball.radius = 8;
    ballLaunched = false;  // Must click to launch
}
```

### createParticles()
Generates particle effect on brick destruction.
```javascript
function createParticles(x, y, color) {
    for (let i = 0; i < 8; i++) {
        particles.push({
            x: x,
            y: y,
            vx: (Math.random() - 0.5) * 6,  // Random X velocity
            vy: (Math.random() - 0.5) * 6,  // Random Y velocity
            color: color,
            life: 30  // Frames until disappears
        });
    }
}
```

---

## Extension Guide

### Adding a New Power-Up

1. **Add to powerUpTypes array:**
```javascript
{ 
    type: 'shield', 
    color: '#FFD700', 
    symbol: '🛡', 
    beneficial: true, 
    chance: 0.04 
}
```

2. **Add case to applyPowerUp():**
```javascript
case 'shield':
    activePowerUps.shield.active = true;
    activePowerUps.shield.endTime = Date.now() + 10000;
    break;
```

3. **Add to activePowerUps object:**
```javascript
activePowerUps.shield = { active: false, endTime: 0 };
```

4. **Implement logic in game loop:**
```javascript
// In moveBall(), check if shield is active
if (activePowerUps.shield.active && now < activePowerUps.shield.endTime) {
    // Shield logic here
}
```

### Adding a New Brick Type

1. **Add type property to brick:**
```javascript
{
    x: number,
    y: number,
    status: 1,
    color: string,
    type: 'multi-hit',  // New property
    hits: 3             // Hits remaining
}
```

2. **Update collision detection:**
```javascript
if (brick.type === 'multi-hit') {
    brick.hits--;
    if (brick.hits <= 0) {
        brick.status = 0;  // Destroy
    }
} else {
    brick.status = 0;  // Regular brick
}
```

3. **Update rendering:**
```javascript
if (brick.type === 'multi-hit') {
    // Draw with visual indicator (number, different color, etc.)
}
```

### Creating Levels

```javascript
const levels = [
    {
        rows: 6,
        cols: 10,
        speed: 3,
        layout: 'standard'  // All bricks
    },
    {
        rows: 8,
        cols: 12,
        speed: 4,
        layout: 'pyramid'   // Custom pattern
    }
];

function loadLevel(levelIndex) {
    const level = levels[levelIndex];
    brickInfo.rows = level.rows;
    brickInfo.cols = level.cols;
    ballSpeed = level.speed;
    createBricks();  // With custom layout logic
}
```

---

## Performance Considerations

### Optimization Tips
1. **Limit particle count** - Cap at reasonable number (e.g., 100)
2. **Reuse objects** - Don't create new objects every frame
3. **Early exit loops** - Break when collision found
4. **Batch similar operations** - Group canvas state changes
5. **Avoid layout thrashing** - Minimize DOM reads/writes

### Memory Management
- Clear arrays when resetting game
- Remove event listeners if dynamically added
- Stop audio oscillators when finished
- Filter arrays to remove dead objects

---

## Browser Compatibility Notes

### Web Audio API
- May require user interaction before playing sounds
- Some browsers need vendor prefixes
- Always check for `AudioContext` availability

### Pointer Lock API
- Requires user gesture (click)
- May be blocked by browser security settings
- Provide fallback to regular mouse movement

### Canvas Performance
- Generally excellent across modern browsers
- Use `willReadFrequently: true` for frequent `getImageData()`
- Consider `imageSmoothingEnabled = false` for pixel art

---

## Debugging Tips

### Common Issues

**Ball gets stuck:**
- Check collision detection logic
- Verify direction calculations
- Add small position offset on collision

**Power-ups don't work:**
- Check timestamp logic (`Date.now()`)
- Verify power-up type strings match
- Console.log active power-up state

**Bricks disappear:**
- Check `brickRowOffset` calculations
- Verify `baseY` vs `y` usage
- Check win condition logic

**Sounds don't play:**
- Ensure AudioContext is resumed
- Check for user interaction requirement
- Verify oscillator start/stop times

### Debug Mode
Add this for development:
```javascript
const DEBUG = true;

if (DEBUG) {
    // Draw collision boxes
    // Log game state
    // Show FPS counter
}
```

---

## Credits

Built with vanilla JavaScript and passion for classic arcade games! 🎮

For questions or contributions, see CONTRIBUTING.md
