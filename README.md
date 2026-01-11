# Claude Code Custom Skills

A collection of custom skills for Claude Code that extend its capabilities with specialized knowledge and best practices.

## Skills Included

### frontend-design-v2

Extended frontend design guidelines with comprehensive mobile responsiveness and cross-element styling consistency. Use alongside the built-in `/frontend-design` skill for production-grade, mobile-first interfaces.

**Key Features:**
- Mobile layout patterns (hero sections, forms, navigation)
- Form element consistency across inputs, selects, textareas
- Color contrast and visibility guidelines
- Pre-implementation checklist
- Common issues quick reference

## Installation

### Option 1: Clone and Configure

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

### Option 2: Direct Copy

Copy the skill folders to your local Claude skills directory:
```bash
cp -r skills/* ~/.claude/skills/
```

## Usage

Once installed, invoke skills in Claude Code:

```
/frontend-design-v2
```

Or reference in your prompts:
```
Please use the frontend-design-v2 skill guidelines when building this interface.
```

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

### frontend-design-v2

- **v1.0** (2025-01-11): Initial release
  - Mobile responsiveness patterns
  - Form element consistency
  - Color contrast guidelines
  - 13 documented issue fixes from real-world implementation

## License

MIT License - Feel free to use and modify.
