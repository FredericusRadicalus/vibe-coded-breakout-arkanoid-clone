# Changelog

All notable changes to the Breakout Game will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2024-12-13

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
- Multiple levels with progression
- Special brick types (multi-hit, explosive, etc.)
- High score persistence (localStorage)
- Mobile touch controls
- Fullscreen mode
- Combo system
- Achievement system
- Custom themes/skins
- Boss levels
- Difficulty settings

---

## Version History

- **1.0.0** (2024-12-13) - Initial Release

---

[1.0.0]: https://github.com/yourusername/breakout-game/releases/tag/v1.0.0
[Unreleased]: https://github.com/yourusername/breakout-game/compare/v1.0.0...HEAD
