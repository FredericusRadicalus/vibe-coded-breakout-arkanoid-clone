# Changelog

All notable changes to the Breakout Game will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2025-12-14

### Added - Major Update: Multi-Level System & Special Bricks 🎮

#### Level System
- **4 Progressive Levels** with increasing difficulty
- Level 1: Classic - Standard bricks only (6 rows)
- Level 2: Discovery - Introduces Glowing and Invisible bricks (7 rows)
- Level 3: Fortress - Introduces Wall bricks with defensive layout (8 rows)
- Level 4: Ultimate Challenge - All brick types combined (8 rows)
- Level progression screen between levels
- Ball speed increases with each level (3.0 → 4.5)
- Score and lives carry over between levels
- Level name displayed in top-right corner

#### New Brick Types
- **Wall Bricks** (Gray):
  - Require 3 hits to destroy
  - Color changes with each hit (Dark → Medium → Light Gray)
  - Display remaining hit count on brick
  - Create defensive barriers in levels
  
- **Glowing Bricks** (Gold with ✧ symbol):
  - Destroy all 8 surrounding bricks when hit
  - Glowing visual effect with shadow
  - Create chain reactions when placed near each other
  - High-value strategic targets
  
- **Invisible Bricks**:
  - Completely invisible at start
  - First hit makes them semi-transparent (revealed)
  - Second hit destroys them
  - Add exploration and surprise elements

#### New Power-Ups
- **Trampoline** (═ Green line):
  - Creates safety net above paddle
  - Bounces ball back up one time
  - Disappears after single use
  - Positioned at paddle level
  
- **Glow Extender** (✧ Gold):
  - Spreads glowing effect to adjacent bricks
  - Converts standard bricks into glowing bricks
  - Creates potential for massive chain reactions
  - Strategic tool for advanced players

### Enhanced Features

#### User Interface
- Improved power-up indicators with fade-out effect in last second
- Speed Up power-up now shows in indicator list
- Trampoline status display
- Better level transition screens
- Game Over screen with restart prompt
- Win screen after completing all 4 levels

#### Controls & Shortcuts
- **S Key**: Restart/continue game from any screen
- **1-4 Keys**: Jump directly to specific level (debug feature)
- **P Key**: Pause only works during active gameplay
- Updated instruction text with all shortcuts
- Improved keyboard control handling

#### Game Mechanics
- Moving Bricks malus now stops at 50% screen height (safer limit)
- Trampoline positioned at paddle level for proper safety net
- Level completion check works correctly with all brick types
- Proper state clearing between levels

### Fixed

#### Critical Fixes
- **Crash prevention**: Added null checks in brick collision handling
- **State deadlocks**: Fixed game state management to prevent freezing
- **Level transitions**: Properly clear all effects when advancing levels
- **Game Over handling**: Correct state management prevents stuck screens

#### Gameplay Fixes
- Moving Bricks malus limited to 300px (50% of screen) instead of 400px
- Trampoline Y position corrected to match paddle level
- Speed Up power-up properly tracked and displayed
- Power-up indicators now show all active effects
- Pause function only works when game is running

#### Visual Fixes
- All power-up labels now appear correctly in top-left
- Power-up indicators fade out smoothly before expiring
- Level name display doesn't overlap with indicators
- Proper brick rendering for all types

### Technical Improvements
- Enhanced collision detection with safety checks
- Improved state management for level progression
- Better memory cleanup between levels
- Optimized brick destruction calculations
- Added comprehensive error prevention

### Documentation
- Updated README with all new features
- Added level strategies and tips
- Documented all brick types in detail
- Explained new power-ups
- Added keyboard shortcuts reference

---

## [1.0.0] - 2025-12-13

### Added
- Initial release of Breakout Game
- Core gameplay mechanics (paddle, ball, bricks)
- 6 rows of rainbow-colored bricks (10 bricks each)
- Adjustable ball speed slider (1-8)
- 3-life system (only lose life when all balls are gone)
- Mouse controls with pointer lock support
- Keyboard controls (arrow keys)
- Click-to-launch ball mechanic
- Ball sticks to paddle until clicked

#### Power-Up System
- **Helpful Power-Ups (Blue):**
  - Extra Life (+1 life)
  - Extra Ball (adds another ball)
  - Multiply Balls (doubles all active balls)
  - Laser Gun (5-second duration, shoot with SPACE)
  - Large Ball (1.5x size for 10 seconds)

- **Malus Power-Ups (Red):**
  - Instant Death (-1 life)
  - Speed Up (1.5x faster for 3 seconds)
  - Moving Bricks (descend on paddle hits, max 75% screen)
  - Small Ball (0.5x size for 10 seconds)
  - Invincible Bricks (can't destroy for 5 seconds)

#### Visual Effects
- Particle effects on brick destruction
- Glowing ball and paddle
- Active power-up indicators
- Rainbow gradient brick rows
- Smooth animations

#### Sound Effects
- Paddle hit sound ("boing")
- Wall bounce sound ("beep")
- Brick break sound (crunchy)
- Power-up collection sounds (ascending/descending tones)
- Web Audio API procedural generation

#### Game Features
- Score tracking (10 points per brick, 5 per power-up)
- Pause functionality (P key)
- Multiple simultaneous balls support
- Improved collision detection (prevents ball sticking)
- Directional bounce based on collision angle
- Paddle-position-based ball spin
- Win/lose conditions with overlay messages

### Technical Details
- Single-file HTML5 Canvas implementation
- No external dependencies (vanilla JavaScript)
- ~15KB total file size
- Pointer Lock API integration
- Web Audio API for sound
- 60 FPS game loop using requestAnimationFrame
- Responsive canvas sizing (835x600px)
- Browser compatibility: Chrome, Firefox, Safari, Opera

### Documentation
- Comprehensive README.md
- CONTRIBUTING.md guidelines
- MIT License
- .gitignore configuration
- Code comments for future enhancements

---

## [Unreleased]

### Planned Features
- Additional levels (expand to 8-10 total)
- More special brick types (Portal, Regenerating, Speed)
- High score persistence (localStorage)
- Mobile touch controls
- Fullscreen mode
- Combo system
- Achievement system
- Custom themes/skins
- Level editor

---

## Version History

- **2.0.0** (2025-12-14) - Multi-Level System & Special Bricks
- **1.0.0** (2025-12-13) - Initial Release

---

[2.0.0]: https://github.com/yourusername/breakout-game/releases/tag/v2.0.0
[1.0.0]: https://github.com/yourusername/breakout-game/releases/tag/v1.0.0
[Unreleased]: https://github.com/yourusername/breakout-game/compare/v2.0.0...HEAD
