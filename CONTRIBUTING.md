# Contributing to Breakout Game

Thank you for considering contributing to this project! 🎉

## 🚀 Quick Start

1. Fork the repository
2. Clone your fork: `git clone https://github.com/yourusername/breakout-game.git`
3. Create a branch: `git checkout -b feature/your-feature-name`
4. Make your changes
5. Test thoroughly in multiple browsers
6. Commit: `git commit -m "Add: your feature description"`
7. Push: `git push origin feature/your-feature-name`
8. Open a Pull Request

## 📋 Development Guidelines

### Code Style

- **Use vanilla JavaScript** - No frameworks or libraries
- **Keep it in one file** - Maintain the single-file architecture
- **Comment complex logic** - Help others understand your code
- **Use meaningful variable names** - Prefer clarity over brevity
- **Consistent indentation** - Use 4 spaces (not tabs)

### Naming Conventions

```javascript
// Variables and functions: camelCase
let ballSpeed = 3;
function movePaddle() { }

// Constants: UPPER_CASE
const MAX_LIVES = 5;

// Objects: camelCase
const paddle = { x: 0, y: 0 };
```

### Testing

Before submitting a PR, test your changes in:
- ✅ Chrome/Edge
- ✅ Firefox
- ✅ Safari
- ✅ Opera (if possible)

Test scenarios:
- Game start/restart
- Ball physics and collisions
- Power-up collection and effects
- Life loss and game over
- Win condition
- Pause/resume functionality
- Speed slider
- Keyboard and mouse controls

## 🎯 Areas for Contribution

### High Priority
- [ ] Mobile touch controls
- [ ] High score persistence (localStorage)
- [ ] Additional levels
- [ ] Fullscreen mode

### Medium Priority
- [ ] Special brick types (multi-hit, explosive, etc.)
- [ ] Combo system
- [ ] Achievement system
- [ ] Custom themes

### Nice to Have
- [ ] Particle effect improvements
- [ ] Additional sound effects
- [ ] Screen shake on impacts
- [ ] Boss levels

## 💡 Feature Requests

Have an idea? Great! Please:

1. Check existing issues first
2. Open a new issue with the `enhancement` label
3. Describe the feature and its benefits
4. Include mockups or examples if applicable

## 🐛 Bug Reports

Found a bug? Please report it:

1. Check if it's already reported
2. Open a new issue with the `bug` label
3. Include:
   - Browser and version
   - Steps to reproduce
   - Expected behavior
   - Actual behavior
   - Screenshots/GIFs if helpful

## 📝 Commit Messages

Use clear, descriptive commit messages:

```
Add: New feature description
Fix: Bug fix description
Update: Change to existing feature
Remove: Removal of feature/code
Refactor: Code reorganization
Docs: Documentation changes
Style: Code style improvements
```

Examples:
```
Add: Explosive brick type with chain reaction
Fix: Ball getting stuck between bricks
Update: Increase power-up spawn rate
Refactor: Collision detection system
Docs: Add installation instructions
```

## 🔍 Code Review Process

1. All PRs require review before merging
2. Maintain backward compatibility
3. Keep changes focused and atomic
4. Update README.md if adding features
5. Add comments for complex algorithms

## ⚠️ Important Notes

### What NOT to do:
- ❌ Add external dependencies (jQuery, React, etc.)
- ❌ Split into multiple files (keep single-file architecture)
- ❌ Break existing features without discussion
- ❌ Add tracking/analytics code
- ❌ Include copyrighted assets without permission

### What TO do:
- ✅ Keep code vanilla JavaScript
- ✅ Maintain single-file structure
- ✅ Test thoroughly before submitting
- ✅ Write clear documentation
- ✅ Follow existing code patterns
- ✅ Be respectful and constructive

## 🎮 Adding New Power-Ups

If adding a new power-up:

1. Add to `powerUpTypes` array with appropriate properties
2. Add case to `applyPowerUp()` switch statement
3. Add visual indicator if it's a timed effect
4. Test interaction with existing power-ups
5. Balance spawn rate appropriately
6. Document in README.md

Example:
```javascript
// In powerUpTypes array:
{ 
    type: 'slowMotion', 
    color: '#9370DB', 
    symbol: '⏱', 
    beneficial: true, 
    chance: 0.03 
}

// In applyPowerUp():
case 'slowMotion':
    // Implementation
    break;
```

## 🏗️ Adding Special Bricks

For new brick types:

1. Add type property to brick object
2. Update collision detection logic
3. Add visual distinction (color, icon, animation)
4. Update win condition if needed
5. Document behavior in code comments
6. Add to README future enhancements

## 🤔 Questions?

- Open an issue with the `question` label
- Check existing issues and discussions
- Be patient - this is a community project

## 📜 License

By contributing, you agree that your contributions will be licensed under the MIT License.

## 🙏 Thank You!

Every contribution, no matter how small, is appreciated. Happy coding! 🎮✨
