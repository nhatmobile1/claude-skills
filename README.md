# Claude Code Custom Skills

A collection of custom skills for Claude Code that extend its capabilities with specialized knowledge and best practices.

## Skills Included

### frontend-design-complete (Recommended)

**All-in-one frontend design skill** that combines the built-in `/frontend-design` aesthetic guidelines with comprehensive mobile responsiveness and cross-element styling consistency. Use this single skill instead of invoking multiple frontend skills.

**Key Features:**
- Bold aesthetic direction and AI-slop avoidance (from built-in skill)
- Mobile layout patterns (hero sections, forms, navigation)
- Form element consistency across inputs, selects, textareas
- Color contrast and visibility guidelines
- Pre-implementation checklist
- Common issues quick reference

**Invoke:** `/frontend-design-complete`

---

### frontend-design-v2

Extended frontend design guidelines with comprehensive mobile responsiveness and cross-element styling consistency. Use alongside the built-in `/frontend-design` skill for production-grade, mobile-first interfaces.

**Note:** Consider using `/frontend-design-complete` instead, which merges this with the built-in skill.

**Key Features:**
- Mobile layout patterns (hero sections, forms, navigation)
- Form element consistency across inputs, selects, textareas
- Color contrast and visibility guidelines
- Pre-implementation checklist
- Common issues quick reference

**Invoke:** `/frontend-design-v2`

---

### color-palette

Create distinctive, accessible color palettes for UI/web design that avoid generic AI aesthetics. Includes domain-specific curated palettes, color theory guidance, and accessibility validation tools.

**Key Features:**
- Domain-specific palettes (Tech/SaaS, E-commerce, Healthcare, Finance, Creative, Food)
- Color harmony generation (complementary, triadic, analogous)
- WCAG accessibility validation (AA/AAA contrast checking)
- Anti-AI-slop guidelines to avoid overused patterns
- Python scripts for palette generation and contrast checking

**Includes:**
- `references/color-palette-ui-design-reference.md` - Comprehensive color guide
- `scripts/generate_palette.py` - Generate color scales and harmonies
- `scripts/check_contrast.py` - Validate WCAG contrast ratios

**Invoke:** `/color-palette`

---

### design-styles

Comprehensive web design aesthetics guide with 40+ design styles. Use when applying a specific aesthetic (glassmorphism, brutalist, minimalist, etc.) or when recommending styles based on industry, audience, or brand.

**Key Features:**
- 40+ documented design styles with examples
- Style recommendations by industry, audience, and brand personality
- Color palettes, typography, and layout principles for each style
- Real-world examples and implementation guidance
- Quick reference table for style comparison

**Includes:**
- `references/design-styles-comprehensive-reference.md` - Full style guide

**Invoke:** `/design-styles`

## Installation

### Option 1: Symlink (Recommended)

This method keeps your skills synced automatically and makes the repo portable across machines.

1. Clone this repository:
   ```bash
   git clone https://github.com/YOUR_USERNAME/claude-skills.git ~/Documents/projects/claude-skills
   ```

2. Remove existing skills directory and create symlink:
   ```bash
   # Backup existing skills if needed
   mv ~/.claude/skills ~/.claude/skills-backup

   # Create symlink
   ln -s ~/Documents/projects/claude-skills/skills ~/.claude/skills
   ```

3. Verify the symlink:
   ```bash
   ls -la ~/.claude/skills
   # Should show: skills -> /Users/YOUR_USERNAME/Documents/projects/claude-skills/skills
   ```

**Benefits:**
- Any skills you add to this repo are immediately available in Claude Code
- Easy to version control and share
- Portable across machines (just clone and symlink)

### Option 2: Clone and Configure

1. Clone this repository:
   ```bash
   git clone https://github.com/YOUR_USERNAME/claude-skills.git
   ```

2. Add to your Claude Code settings (`.claude/settings.json`):
   ```json
   {
     "plugins": [
       "/path/to/claude-skills"
     ]
   }
   ```

### Option 3: Direct Copy

Copy the skill folders to your local Claude skills directory:
```bash
cp -r skills/* ~/.claude/skills/
```

**Note:** With this method, you'll need to re-copy whenever you update skills.

## Usage

Once installed, invoke skills in Claude Code:

```
/frontend-design-complete
/color-palette
/design-styles
```

Or reference in your prompts:
```
Please use the frontend-design-complete skill guidelines when building this interface.
```

### Recommended Workflow

For frontend projects, invoke these skills together for best results:

```
/frontend-design-complete
/color-palette
/design-styles
```

1. **design-styles** - Choose your aesthetic direction
2. **color-palette** - Generate an accessible, distinctive color scheme
3. **frontend-design-complete** - Implement with aesthetics AND mobile responsiveness

## Contributing

Feel free to add new skills or improve existing ones:

1. Create a new folder under `skills/`
2. Add a `SKILL.md` file with the skill definition
3. Follow the skill format with YAML frontmatter

## Skill Format

```markdown
---
name: skill-name
description: Brief description of what the skill does
---

# Skill Content

Your skill instructions, guidelines, code examples, etc.
```

## Version History

### frontend-design-complete

- **v1.0** (2025-01-11): Initial release
  - Merged built-in frontend-design aesthetic guidelines
  - Mobile responsiveness patterns
  - Form element consistency
  - Color contrast guidelines
  - Pre-implementation checklist
  - Common issues quick reference

### frontend-design-v2

- **v1.0** (2025-01-11): Initial release
  - Mobile responsiveness patterns
  - Form element consistency
  - Color contrast guidelines
  - 13 documented issue fixes from real-world implementation

### color-palette

- **v1.0** (2025-01-08): Initial release
  - Domain-specific palette curation
  - Color harmony generation scripts
  - WCAG contrast validation
  - Anti-AI-slop guidelines

### design-styles

- **v1.0** (2025-01-09): Initial release
  - 40+ design styles documented
  - Style recommendations by criteria
  - Comprehensive reference guide

## License

MIT License - Feel free to use and modify.
