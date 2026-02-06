# Claude Skills

A curated collection of reusable Claude Code skills for frontend design and iOS development.

## Purpose

Extend Claude with production-grade design and development guidelines that prioritize distinctive aesthetics, accessibility, and best practices while avoiding generic AI-generated patterns.

## Skills Included

**Frontend (3 skills):**
- `frontend-design-complete` - All-in-one: aesthetics, mobile, modern CSS, performance, dark mode, AI patterns, accessibility (recommended)
- `color-palette` - Domain-specific palettes, WCAG validation, color harmony
- `design-styles` - 40+ documented design aesthetics with recommendations

**iOS (4 skills):**
- `ios-development` - Comprehensive Swift/SwiftUI patterns, MVVM, networking, testing
  - `ios-app-planner` - Planning & architecture
  - `ios-coding-best-practices` - Swift conventions
  - `ios-ui-review` - HIG compliance, accessibility

## File Structure

```
claude-skills/
├── README.md                    # Installation & usage guide
├── skills/
│   ├── frontend/
│   │   ├── frontend-design-complete/  # Recommended all-in-one
│   │   ├── color-palette/
│   │   │   ├── SKILL.md
│   │   │   ├── references/
│   │   │   └── scripts/         # Python utilities
│   │   └── design-styles/
│   └── ios-development/
│       ├── SKILL.md
│       ├── ios-app-planner/
│       ├── ios-coding-best-practices/
│       └── ios-ui-review/
```

## Key Features

- **Anti-AI-slop guidelines** - Avoid generic cream backgrounds, purple gradients, rounded corners
- **Modern CSS** - Container queries, :has(), scroll-driven animations, view transitions, cascade layers
- **Performance-first** - Core Web Vitals, CLS prevention, font loading, image optimization
- **Dark mode & theming** - Token architecture, system preference detection, multi-theme support
- **AI-era patterns** - Streaming UI, confidence indicators, human-in-the-loop controls
- **Mobile-first responsive patterns** - Real-world edge cases and solutions
- **Accessibility-first** - WCAG contrast, cognitive accessibility, internationalization
- **Modern Swift best practices** - async/await, SwiftData, MVVM with repositories
- **Pre-implementation checklists** - 31 Parts with comprehensive verification

## Installation

Three options:
1. **Symlink** to `~/.claude/skills` (recommended)
2. **Clone** directly into project
3. **Copy** specific skill folders

## Usage

Invoke in Claude Code:
- `/frontend-design-complete`
- `/color-palette`
- `/ios-development`

## Status

Active development, last updated Feb 2026
