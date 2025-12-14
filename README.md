# 🎮 Breakout Game

A modern, feature-rich implementation of the classic Breakout/Arkanoid game built with HTML5 Canvas and vanilla JavaScript. Features 4 progressive levels, multiple brick types, power-ups, and extensive gameplay mechanics. No dependencies required - just open and play!

![Game Preview](screenshot.png)

## ✨ Features

### Core Gameplay
- **4 Progressive Levels** - Increasing difficulty with unique brick layouts
- **3 Brick Types** - Standard, Wall (multi-hit), Glowing (explosive), and Invisible bricks
- **Smooth physics** - Realistic ball bouncing with paddle position-based spin
- **Responsive controls** - Mouse (with pointer lock) or keyboard
- **Multiple balls** - Manage several balls simultaneously
- **Life system** - 3 lives, lose one only when all balls are gone
- **Score tracking** - Points for bricks + power-up bonuses + level progression

### 🧱 Brick Types

**Standard Bricks**
- Classic single-hit bricks in rainbow colors
- Foundation of all levels

**Wall Bricks** (Gray with number)
- Require **3 hits** to destroy
- Color changes with each hit: Dark → Medium → Light Gray
- Display remaining hit count
- Create defensive barriers

**Glowing Bricks** (Gold with ✧)
- **Explosive chain reaction** - destroys all 8 surrounding bricks!
- Glowing visual effect
- Strategic placement creates massive scoring opportunities

**Invisible Bricks** (Hidden)
- Completely invisible until first hit
- **First hit**: Becomes semi-transparent (revealed)
- **Second hit**: Destroyed
- Adds surprise element and exploration

### 🎁 Power-Up System

**Helpful Power-Ups (Blue/Green/Gold)**
- ♥ **Extra Life** - Gain +1 life
- ● **Extra Ball** - Add another ball to the field
- ×× **Multiply Balls** - Double all active balls
- ⚡ **Laser** - Shoot lasers for 5 seconds (SPACE key)
- ◉ **Large Ball** - 1.5x bigger ball for 10 seconds
- ═ **Trampoline** - Safety net that saves you once
- ✧ **Glow Extender** - Spreads glowing effect to adjacent bricks

**Malus Power-Ups (Red)**
- ☠ **Instant Death** - Lose 1 life immediately
- » **Speed Up** - Ball moves 1.5x faster for 3 seconds
- ↓ **Moving Bricks** - Bricks descend when ball hits paddle (max 50% screen)
- ○ **Small Ball** - Ball shrinks to 0.5x size for 10 seconds
- ✖ **Invincible Bricks** - Can't destroy bricks for 5 seconds

### 🎯 4 Unique Levels

**Level 1: Classic** ⭐
- 6 rows of standard bricks
- Ball speed: 3.0
- Learn the basic mechanics
- Perfect for beginners

**Level 2: Discovery** ⭐⭐
- 7 rows with mixed brick types
- Introduces **Glowing Bricks** (explosive chains)
- Introduces **Invisible Bricks** (hidden surprises)
- Ball speed: 3.5
- Strategic brick hunting

**Level 3: Fortress** ⭐⭐⭐
- 8 rows with defensive layout
- Top rows protected by **Wall Bricks** (3 hits each)
- **Glowing Bricks** for tactical opportunities
- Ball speed: 4.0
- Patience and precision required

**Level 4: Ultimate Challenge** ⭐⭐⭐⭐
- 8 rows with **ALL brick types**
- Wall bricks create barriers
- Glowing bricks enable chain reactions
- Invisible bricks hide in gaps
- Ball speed: 4.5
- Master all mechanics to win!

### 🔊 Sound Effects
- **Paddle hit** - Satisfying "boing" (200Hz sine wave)
- **Wall bounce** - Quick "beep" (300Hz square wave)
- **Brick break** - Crunchy "break" sound (800→200Hz sweep)
- **Power-ups** - Ascending (good) or descending (bad) tones
- All sounds procedurally generated using Web Audio API

### 🎨 Visual Polish
- Rainbow-colored brick rows
- Particle effects on brick destruction
- Glowing effects for special bricks
- Active power-up indicators with fade-out
- Smooth animations
- Level name display
- Professional UI design

## 🎮 Controls

| Action | Control |
|--------|---------|
| **Move Paddle** | Arrow Keys or Mouse |
| **Launch Ball** | Click on canvas |
| **Shoot Laser** | SPACE (when laser active) |
| **Pause/Unpause** | P |
| **Restart Game** | S |
| **Adjust Speed** | Slider (1-8) |
| **Jump to Level** | 1-4 keys (debug) |
| **Start Game** | Start Game button |

### Pointer Lock
Click the canvas to lock your mouse pointer, allowing you to control the paddle without the cursor leaving the game area!

## 🚀 Getting Started

### Installation
No installation needed! Just download and open in a browser.

```bash
# Clone the repository
git clone https://github.com/yourusername/breakout-game.git

# Navigate to directory
cd breakout-game

# Open in browser
open breakout.html
```

Or simply download `breakout.html` and double-click to play.

### Browser Compatibility
- ✅ Chrome/Edge (recommended)
- ✅ Firefox
- ✅ Safari
- ✅ Opera

Requires a modern browser with HTML5 Canvas and Web Audio API support.

## 📖 How to Play

1. Click **Start Game** to begin Level 1
2. Click the **canvas** to launch the ball
3. **Move the paddle** to keep the ball in play
4. **Break all bricks** to advance to the next level
5. Collect **blue/green/gold power-ups** and avoid **red ones**
6. Complete all **4 levels** to win!

### Pro Tips & Strategies 💡
- **Ball control**: Hit the ball with different parts of the paddle to control angle
- **Power-up priority**: Collect Extra Life and Trampoline early for insurance
- **Glowing chains**: Position ball to trigger glowing bricks near clusters
- **Glow Extender combo**: Use it to spread glowing effect, then trigger massive explosions
- **Wall brick strategy**: Focus on one at a time, use laser power-up for efficiency
- **Invisible hunting**: Watch for gaps in brick patterns - they might be invisible!
- **Moving bricks**: Keep bricks from descending by clearing quickly
- **Multiple balls**: Spread them out to cover more area and clear faster
- **Trampoline timing**: Save it for when you're overwhelmed or on your last life

## 🏗️ Technical Details

### Built With
- **HTML5 Canvas** - Rendering engine
- **Vanilla JavaScript** - Game logic (no frameworks!)
- **Web Audio API** - Procedural sound generation
- **Pointer Lock API** - Mouse capture

### File Structure
```
breakout-game/
├── breakout.html       # Main game file (complete, standalone)
├── README.md          # This file
├── CONTRIBUTING.md    # Contribution guidelines
├── CHANGELOG.md       # Version history
├── DOCS.md            # Technical documentation
├── LICENSE            # MIT License
└── screenshot.png     # Game preview image
```

### Code Architecture
- **Level system** - 4 unique levels with different brick layouts
- **Brick types** - Standard, Wall, Glowing, Invisible with unique behaviors
- **Object-oriented design** - Separate entities (paddle, ball, bricks, power-ups)
- **Game loop** - requestAnimationFrame for smooth 60 FPS
- **Advanced collision detection** - Directional overlap prevents ball sticking
- **State management** - Clean separation of game state and rendering
- **Power-up system** - Timed effects with visual indicators

### Performance
- **Lightweight** - Single ~20KB HTML file
- **Efficient** - Runs at 60 FPS on most devices
- **No dependencies** - Pure vanilla JavaScript
- **Instant load** - No external resources
- **Safe code** - Null checks prevent crashes

## 🎓 Advanced Mechanics

### Glowing Brick Chains
Hit one glowing brick → destroys 8 adjacent bricks → can trigger other glowing bricks in a chain reaction! Strategic placement can clear entire sections.

### Glow Extender Strategy
1. Identify cluster of standard bricks
2. Use Glow Extender to convert adjacent bricks to glowing
3. Trigger one glowing brick to start chain reaction
4. Watch the points rack up!

### Wall Brick Tactics
- Requires patience - 3 hits per brick
- Laser power-up is highly effective
- Create openings to reach bricks behind
- Color changes: Gray → Light Gray → Lighter Gray

### Invisible Brick Detection
- Look for "gaps" in brick patterns
- Use Extra Ball to explore safely
- First hit reveals position
- Second hit destroys

## 🔮 Future Enhancements

### Planned Features
- [ ] More levels (8-10 total)
- [ ] High score persistence (localStorage)
- [ ] Difficulty settings (Easy/Normal/Hard)
- [ ] Additional brick types (Portal, Regenerating, Speed)
- [ ] Combo system for consecutive hits
- [ ] Achievement system
- [ ] Mobile touch controls
- [ ] Fullscreen mode
- [ ] Custom themes/skins
- [ ] Level editor

See [CHANGELOG.md](CHANGELOG.md) for version history and [DOCS.md](DOCS.md) for technical details.

## 🤝 Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Quick Start for Contributors
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Test thoroughly in multiple browsers
4. Commit your changes (`git commit -m 'Add some amazing feature'`)
5. Push to the branch (`git push origin feature/amazing-feature`)
6. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Classic Breakout (Atari, 1976) - Original game concept
- Arkanoid (Taito, 1986) - Power-up system inspiration
- HTML5 game development community

## 📧 Contact

Your Name - [@yourhandle](https://twitter.com/yourhandle)

Project Link: [https://github.com/yourusername/breakout-game](https://github.com/yourusername/breakout-game)

---

**Enjoy breaking bricks!** 🎮✨

Current Version: **2.0.0** - Now with 4 levels and special brick types!

If you like this project, give it a ⭐ on GitHub!
