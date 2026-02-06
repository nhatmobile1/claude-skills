---
name: frontend-design-complete
description: Create distinctive, production-grade frontend interfaces with high design quality. Covers aesthetics, mobile-first patterns, modern CSS, performance (Core Web Vitals), dark mode/theming, AI-era patterns, interaction design, data visualization, fluid typography, responsive images, component architecture, forms, internationalization, cognitive accessibility, design tokens, and cascade layers. Use this as your single frontend design skill.
---

# Complete Frontend Design Guidelines

This skill guides creation of distinctive, production-grade frontend interfaces that avoid generic "AI slop" aesthetics while ensuring proper mobile responsiveness and cross-element consistency.

---

## Part 1: Design Thinking & Aesthetics

### Design Thinking

Before coding, understand the context and commit to a BOLD aesthetic direction:
- **Purpose**: What problem does this interface solve? Who uses it?
- **Tone**: Pick an extreme: brutally minimal, maximalist chaos, retro-futuristic, organic/natural, luxury/refined, playful/toy-like, editorial/magazine, brutalist/raw, art deco/geometric, soft/pastel, industrial/utilitarian, etc. There are so many flavors to choose from. Use these for inspiration but design one that is true to the aesthetic direction.
- **Constraints**: Technical requirements (framework, performance, accessibility).
- **Differentiation**: What makes this UNFORGETTABLE? What's the one thing someone will remember?

**CRITICAL**: Choose a clear conceptual direction and execute it with precision. Bold maximalism and refined minimalism both work - the key is intentionality, not intensity.

Then implement working code (HTML/CSS/JS, React, Vue, etc.) that is:
- Production-grade and functional
- Visually striking and memorable
- Cohesive with a clear aesthetic point-of-view
- Meticulously refined in every detail
- **Fully mobile responsive** (see Part 2)

### Frontend Aesthetics Guidelines

Focus on:
- **Typography**: Choose fonts that are beautiful, unique, and interesting. Avoid generic fonts like Arial and Inter; opt instead for distinctive choices that elevate the frontend's aesthetics; unexpected, characterful font choices. Pair a distinctive display font with a refined body font.
- **Color & Theme**: Commit to a cohesive aesthetic. Use CSS variables for consistency. Dominant colors with sharp accents outperform timid, evenly-distributed palettes.
- **Motion**: Use animations for effects and micro-interactions. Prioritize CSS-only solutions for HTML. Use Motion library for React when available. Focus on high-impact moments: one well-orchestrated page load with staggered reveals (animation-delay) creates more delight than scattered micro-interactions. Use scroll-triggering and hover states that surprise.
- **Spatial Composition**: Unexpected layouts. Asymmetry. Overlap. Diagonal flow. Grid-breaking elements. Generous negative space OR controlled density.
- **Backgrounds & Visual Details**: Create atmosphere and depth rather than defaulting to solid colors. Add contextual effects and textures that match the overall aesthetic. Apply creative forms like gradient meshes, noise textures, geometric patterns, layered transparencies, dramatic shadows, decorative borders, custom cursors, and grain overlays.

NEVER use generic AI-generated aesthetics like overused font families (Inter, Roboto, Arial, system fonts), cliched color schemes (particularly purple gradients on white backgrounds), predictable layouts and component patterns, and cookie-cutter design that lacks context-specific character.

### AI Slop Patterns to Avoid

These specific patterns have become telltale signs of AI-generated design. Avoid them:

**Colors:**
- Cream/off-white backgrounds (`#f8f6f3`, `#fdfcfb`, `#faf8f5` type colors)
- Terracotta/coral/rust accents (`#c45c48`, `#e07860`, `#d4715f`, `#bf4a37`)
- Orange and teal combinations
- Purple/blue gradients on white backgrounds
- Warm shadows with colored tints

**Layout & Components:**
- Generous rounded corners (12-16px+ border-radius)
- Left-border accent lines on cards (the colored vertical stripe)
- Pill-shaped tabs and buttons
- Cards with subtle warm shadows and hover lift effects
- Overly "friendly" and "approachable" feeling

**Visual Effects:**
- Texture overlays (noise, grain, paper textures)
- Glow effects and colored shadows
- Gradient backgrounds with warm color temperature
- Soft, diffused aesthetic everywhere

**Overall Aesthetic:**
- The "cozy webapp" look - warm, soft, inviting
- Designs that feel like Notion/Linear clones
- Safe, inoffensive, "premium but accessible" feeling
- Lack of sharp contrast or bold decisions

Instead, make distinctive choices: cooler color temperatures, sharper geometry, unexpected color combinations, higher contrast, or commit fully to a specific design tradition (Swiss, Japanese, Brutalist, Editorial, etc.) rather than the generic "modern SaaS" look.

Interpret creatively and make unexpected choices that feel genuinely designed for the context. No design should be the same. Vary between light and dark themes, different fonts, different aesthetics. NEVER converge on common choices (Space Grotesk, for example) across generations.

**IMPORTANT**: Match implementation complexity to the aesthetic vision. Maximalist designs need elaborate code with extensive animations and effects. Minimalist or refined designs need restraint, precision, and careful attention to spacing, typography, and subtle details. Elegance comes from executing the vision well.

---

## Part 2: Mobile-First Responsive Patterns

### Hero Sections

**Problem**: 2-column grid layouts leave empty space when one column is hidden on mobile.

```css
/* Desktop: 2-column grid */
.hero {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 64px;
  align-items: center;
}

/* Mobile: Switch to centered flex */
@media (max-width: 768px) {
  .hero {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    padding: 40px 20px;
    gap: 24px;
  }

  .hero-content {
    align-items: center;
  }

  .hero-badge {
    align-self: center;
  }

  .hero-title {
    font-size: 32px;
    text-align: center;
  }

  .hero-subtitle {
    font-size: 14px;
    text-align: center;
  }

  .hero-cta {
    flex-direction: column;
    align-items: center;
    width: 100%;
  }

  .hero-cta .btn {
    width: 100%;
    max-width: 280px;
  }

  .hero-visual {
    display: none;
  }
}
```

**Key Rule**: When hiding grid columns on mobile, switch from `display: grid` to `display: flex` to eliminate reserved empty space.

### Large Selection Lists (Accordion Pattern)

**Problem**: Horizontal scroll for many items (20+) is unusable on mobile - text gets cut off.

**Solution**: Use collapsible accordion with category headers.

```jsx
function StyleSelector({ items, categories }) {
  const [expandedCategory, setExpandedCategory] = useState(null);

  return (
    <div className="selector">
      {categories.map(category => (
        <div key={category.name} className={`category ${expandedCategory === category.name ? 'expanded' : ''}`}>
          <button
            className="category-header"
            onClick={() => setExpandedCategory(
              expandedCategory === category.name ? null : category.name
            )}
          >
            <span>{category.name}</span>
            <ChevronIcon />
          </button>
          <div className="category-items">
            {category.items.map(item => (
              <button key={item.id} className="item">{item.name}</button>
            ))}
          </div>
        </div>
      ))}
    </div>
  );
}
```

```css
@media (max-width: 768px) {
  .category-items {
    display: none;
  }

  .category.expanded .category-items {
    display: flex;
    flex-direction: column;
  }

  .chevron-icon {
    transition: transform 0.2s ease;
  }

  .category.expanded .chevron-icon {
    transform: rotate(180deg);
  }
}
```

### Form Layouts

**Problem**: Multi-column form layouts get cut off on mobile.

```css
.form-row {
  display: flex;
  gap: 16px;
}

@media (max-width: 768px) {
  .form-row {
    flex-direction: column;
  }

  .form-group {
    width: 100%;
  }
}
```

### Status/Alert Cards

**Problem**: Inconsistent text alignment when stacking horizontally-laid elements vertically.

```css
.alert {
  display: flex;
  align-items: flex-start;
  gap: 12px;
}

@media (max-width: 768px) {
  .alert {
    flex-direction: column;
    align-items: center;  /* Center the flex items */
    text-align: center;   /* Center the text within items */
    gap: 8px;
  }

  .alert strong {
    text-align: center;  /* Explicit for block elements */
  }
}
```

**Key Rule**: Stacked flex items need BOTH `align-items: center` AND `text-align: center` for proper centering.

### Grid Layouts

```css
@media (max-width: 768px) {
  .pricing-grid,
  .feature-grid,
  .team-grid,
  .stats-grid {
    grid-template-columns: 1fr;
  }
}
```

### Breakpoint Reference

```css
/* Tablet - Stack sidebars, maintain content width */
@media (max-width: 1200px) { }

/* Mobile - Full single-column, centered hero */
@media (max-width: 768px) { }

/* Small Mobile - Compact spacing, reduced font sizes */
@media (max-width: 480px) { }
```

### Mobile Font Scaling

```css
@media (max-width: 768px) {
  .hero-title {
    font-size: 32px;  /* Down from ~48px */
  }

  .section-title {
    font-size: 24px;  /* Down from ~32px */
  }

  .section-subtitle {
    font-size: 14px;  /* Down from ~16px */
  }
}
```

**Modern Alternative**: Container queries (Part 18) can replace many media queries by making components responsive to their container width rather than the viewport. For fluid font sizing without breakpoints, see Part 24.

---

## Part 3: Form Element Consistency

### Always Style as a Group

**Problem**: Styling only `.input` leaves `.select` and `.textarea` unstyled.

```css
/* WRONG - Only targets input */
.style-brutalist .input {
  border: 2px solid var(--border);
  border-radius: 0;
}

/* CORRECT - Targets all form fields */
.style-brutalist .input,
.style-brutalist .select,
.style-brutalist .textarea {
  border: 2px solid var(--border);
  border-radius: 0;
}
```

### Textarea Border Radius Exceptions

Pill-shaped inputs (border-radius: 100px) look wrong on textareas:

```css
.style-kawaii .input,
.style-kawaii .select {
  border-radius: 100px;
}

/* Textarea needs smaller radius */
.style-kawaii .textarea {
  border-radius: 20px;
}
```

### Dropdown Option Styling

`<option>` elements can't inherit backdrop-filter or complex backgrounds:

```css
.style-glassmorphism .select {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  color: white;
}

/* Options need solid backgrounds */
.style-glassmorphism .select option {
  background: #1a1a2e;
  color: white;
}
```

### Transparent Border Styles (Neomorphism, Claymorphism)

**Problem**: Styles with `border: transparent` make form controls invisible.

```css
/* These styles use transparent borders */
.style-neomorphism .radio-mark,
.style-claymorphism .radio-mark {
  border: 2px solid #B8BEC7;  /* Add visible border */
  background: var(--bg-primary);
  box-shadow: inset 2px 2px 4px rgba(163,177,198,0.3),
              inset -2px -2px 4px rgba(255,255,255,0.8);
}
```

---

## Part 4: Color Contrast Rules

### Badge/Pill Elements

Always verify badge text contrasts with its background:

```css
/* WRONG - May be invisible on light backgrounds */
.badge {
  color: white;
}

/* CORRECT - Uses semantic variable */
.badge {
  color: var(--bg-primary);  /* Inverts with background */
}
```

### Color Swatches Display

Swatches showing colors need visible borders regardless of swatch color:

```css
.color-swatch {
  border: 2px solid rgba(255, 255, 255, 0.15);
  box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.3);
}
```

### Dark Theme Form Labels

**Problem**: Assuming labels should be white/light on dark themes.

```css
/* WRONG - Hardcoded color */
.label {
  color: white;
}

/* CORRECT - Uses semantic variable */
.label {
  color: var(--text-primary);
}
```

---

## Pre-Implementation Checklist

Before finalizing any frontend design, verify:

### Aesthetics
- [ ] Committed to a bold, distinctive aesthetic direction
- [ ] Avoided AI slop patterns (cream backgrounds, terracotta accents, purple gradients)
- [ ] Used distinctive typography (not Inter, Roboto, Arial)
- [ ] Created cohesive color palette with CSS variables

### Mobile Responsiveness
- [ ] Hero section centers on mobile (not left-aligned with empty space)
- [ ] Grid layouts collapse to single column on mobile
- [ ] Large selection lists use accordion on mobile (not horizontal scroll)
- [ ] Status/alert cards center properly on mobile
- [ ] Font sizes scale appropriately for mobile

### Form Elements
- [ ] All form fields (input, select, textarea) styled consistently
- [ ] Radio buttons and checkboxes visible (especially for transparent-border styles)
- [ ] Dropdown options have readable backgrounds
- [ ] Textarea has appropriate border-radius (not pill-shaped)

### Color Contrast
- [ ] Labels use semantic color variables (not hardcoded)
- [ ] Badge/pill text contrasts with background
- [ ] Color swatches have visible borders
- [ ] Dark theme elements properly contrasted

---

## Common Issues Quick Reference

| Issue | Cause | Fix |
|-------|-------|-----|
| Hero left-aligned with empty space | Grid reserves hidden column | Switch to flex on mobile |
| Form fields cut off | Fixed-width grid | Stack vertically with flex |
| Inconsistent alert alignment | Missing align-items | Add `align-items: center` + `text-align: center` |
| Invisible form controls | Transparent borders | Add explicit borders or shadows |
| White text on light background | Hardcoded colors | Use semantic CSS variables |
| Horizontal scroll on selections | Too many items | Use accordion pattern |
| Textarea looks wrong | Pill border-radius | Use smaller radius for textarea |
| Design looks "AI-generated" | AI slop patterns | Follow aesthetic guidelines, be bold |
| Layout shift on load | Images without dimensions | Add `width`/`height` or `aspect-ratio` (Part 19) |
| Dark mode looks washed out | Colors not desaturated | Reduce saturation ~20% for dark mode (Part 20) |
| AI responses feel broken | No streaming indicator | Add typewriter cursor and phase-based loading (Part 21) |
| Specificity wars in CSS | No cascade management | Use `@layer` for explicit ordering (Part 31) |
| Content unreadable in translation | Fixed-width containers | Use logical properties and flexible layouts (Part 28) |
| Flash of wrong theme | Theme loads after paint | Run theme script in `<head>` (Part 20) |

---

Remember: Claude is capable of extraordinary creative work. Don't hold back, show what can truly be created when thinking outside the box and committing fully to a distinctive vision - while ensuring it works beautifully on every screen size.

---

## Part 5: Design Research & Inspiration Resources

Use these curated resources during the research phase to gather authentic inspiration, study proven patterns, and avoid generic design decisions.

### Curation & Reference Platforms

**Are.na** - https://www.are.na
Visual research tool for building mood boards and connecting ideas. Use for assembling contextual reference libraries, tracking design influences, and creating shareable channels documenting design processes. Think of it as "playlists for ideas" - following genuine curiosity leads to deeper creative engagement than algorithmic suggestions.

**Mobbin** - https://mobbin.com
UI pattern library with 1,150+ apps, 586,700+ screens, and 312,000+ user flows. Search by screens, UI elements, flows, or text within screenshots. Features apps from Airbnb, Uber, ChatGPT, Dropbox, Nike. Includes Figma plugin for direct download. Use to study how leading apps handle specific design challenges and explore complete user journeys.

**Logggos** - https://www.logggos.club
Curated logo gallery organized by business sectors (Tech, DTC, Agencies) and filterable by typography styles (sans-serif, script, serif), colors, and geometric shapes. Use when designing logo-adjacent elements or studying brand identity patterns.

### Icons & Visual Assets

**The Noun Project** - https://thenounproject.com
10M+ human-curated icons and photos in SVG/PNG formats. Emphasizes "Made by Humans" curation over algorithmic content. Use for quick icon discovery during design workflows, but consider creating custom icons for distinctive projects.

**Artvee** - https://artvee.com
High-resolution public domain paintings, posters, and illustrations. Categories include Abstract, Figurative, Landscape, Still Life, Religion, Mythology. All files freely usable for personal and commercial projects. Use for incorporating classical artwork, creating derivative works, or adding historical visual elements.

**Mockupworld** - https://www.mockupworld.co
Free photo-realistic PSD mockups for devices (iPhone, iPad, MacBook), packaging, print materials, and vehicles. Use to present designs in realistic contexts for client presentations or portfolio pieces.

### Site Builders for Reference

**Cargo** - https://cargo.site
Site builder for designers and artists with strong creative focus. Study Cargo sites for clean portfolio presentations and community-curated examples of quality design.

**Readymag** - https://readymag.com
Specialized for creating cool animations and extravagant transitions. Study Readymag projects for motion design inspiration and experimental layout approaches.

### Web Design Inspiration

**Godly.website** - https://godly.website
"Astronomically good web design inspiration" - 1,000+ curated exceptional websites spanning diverse industries. Features work from recognized design leaders (Metalab, Lusion, Notion, Stripe) and emerging talent. Use for studying cutting-edge design approaches.

**Minimal Gallery** - https://minimal.gallery
Hand-picked minimalist web design since 2013. Rigorous human curation (most submissions rejected). Organized by industry and design approach. Use for studying purposeful, clean design that prioritizes both visual elegance and usability.

**Brutalist Websites** - https://brutalistwebsites.com
Curated collection of brutalist web design with interviews. Key principles: technical honesty over polish, anti-commercial stance, content-first approach, bare-bones functionality. Features magazine sites, portfolios, and experimental platforms. Use to understand deliberate aesthetic rejection and information-first design.

**Landingfolio** - https://landingfolio.com
Landing page inspiration and templates organized by design approach and industry. Use for studying effective conversion-focused layouts and call-to-action patterns.

### Foundational Learning

**Degreeless.design** - https://degreeless.design
Comprehensive self-directed design education resource. Organized in progressive stages: Basics (typography, color theory, design history), UX Essentials (process, research, design systems), Advanced (industry content from Airbnb, Google). Key philosophy: "Process is the value you bring. Tools change & trends die."

**Google Fonts Knowledge** - https://fonts.google.com/knowledge
Typography guidance and principles from Google. Covers type design, font selection, pairing strategies, and web font implementation best practices.

### Blogs & Analysis

**Brand New** - https://www.underconsideration.com/brandnew/
Daily updates on logo, identity, and branding projects. Features before-and-after rebrand analysis with critical commentary. Categories: Reviewed (in-depth analysis), Noted (professional observations), Spotted (discovery-focused). Use to study branding decisions and understand what makes identity work succeed or fail.

### Experimental Design Tools

**Constraint Systems** - https://constraint.systems
Collection of experimental creative tools for unique layouts and constraint-based design exploration. Use for breaking out of conventional layout patterns.

**Whisk by Google Labs** - https://labs.google/whisk
Experimental image generation tool powered by Imagen 4. Enables "prompting with pictures" - upload reference images as creative prompts and mix ideas in new ways. Use for rapid visual exploration and concept iteration during early design phases.

### Design Systems to Study

**IBM Carbon** - https://carbondesignsystem.com
Enterprise design system emphasizing accessibility and consistency. Study for: responsive layout systems (breakpoints xs through 2xl), density options (condensed/normal), data visualization patterns, modular component architecture. Excellent reference for data-heavy applications.

**GitHub Primer** - https://primer.style
Comprehensive open-source design system with strong accessibility focus. Study for: detailed accessibility patterns and checklists, Octicons SVG icon system, design tokens (color, spacing, typography), component libraries for React/Rails.

**Material Design 3** - https://m3.material.io
Google's latest design system. Study for: typography scale (display, headline, title, label, body styles), cohesive color palette with semantic tokens, elevation system for visual hierarchy, CSS custom properties for dynamic theming.

---

## Part 6: Design System Principles

Learn from production design systems to create more cohesive, maintainable interfaces.

### Token-Based Design

Use semantic design tokens instead of hardcoded values:

```css
/* Define tokens at root level */
:root {
  /* Primitive tokens */
  --color-blue-500: #3b82f6;
  --color-gray-900: #111827;
  --spacing-4: 1rem;

  /* Semantic tokens (reference primitives) */
  --color-primary: var(--color-blue-500);
  --color-text-primary: var(--color-gray-900);
  --spacing-component-padding: var(--spacing-4);
}

/* Apply semantically */
.button {
  background: var(--color-primary);
  color: var(--color-text-on-primary);
  padding: var(--spacing-component-padding);
}
```

### Typography Scale

Establish a clear type hierarchy (inspired by Material 3):

```css
:root {
  /* Display - Hero headlines */
  --type-display-large: 57px/64px;
  --type-display-medium: 45px/52px;

  /* Headline - Section headers */
  --type-headline-large: 32px/40px;
  --type-headline-medium: 28px/36px;

  /* Title - Card titles, dialogs */
  --type-title-large: 22px/28px;
  --type-title-medium: 16px/24px;

  /* Body - Paragraph text */
  --type-body-large: 16px/24px;
  --type-body-medium: 14px/20px;

  /* Label - Buttons, form labels */
  --type-label-large: 14px/20px;
  --type-label-medium: 12px/16px;
}
```

### Elevation & Depth

Create visual hierarchy through consistent elevation (from Carbon/Material):

```css
:root {
  --elevation-1: 0 1px 2px rgba(0, 0, 0, 0.05);
  --elevation-2: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
  --elevation-3: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
  --elevation-4: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
}

/* Apply based on component importance */
.card { box-shadow: var(--elevation-1); }
.dropdown { box-shadow: var(--elevation-2); }
.modal { box-shadow: var(--elevation-4); }
```

### Density Variants

Support different density contexts (from Carbon):

```css
.component {
  --component-padding: var(--spacing-4);
}

.component--condensed {
  --component-padding: var(--spacing-2);
}

/* Data tables often need condensed density */
.data-table--condensed .table-cell {
  padding: var(--spacing-1) var(--spacing-2);
}
```

### Accessibility Patterns (from Primer)

```css
/* Visually hidden but accessible to screen readers */
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}

/* Focus visible for keyboard navigation */
.interactive:focus-visible {
  outline: 2px solid var(--color-focus);
  outline-offset: 2px;
}

/* Reduced motion preference */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

For a full three-tier token architecture (constant → semantic → contextual) with multi-theme mapping, see Part 30. For cascade management of token layers, see Part 31.

---

## Part 7: Brutalist Design Principles

For projects requiring anti-conventional aesthetics, study these brutalist principles:

### Core Philosophy

Brutalism in web design is "a reaction by a younger generation to the lightness, optimism, and frivolity of today's web design." Key principles:

1. **Technical Honesty** - Expose the scaffolding of web design rather than masking code and structure
2. **Anti-Commercial Stance** - Reject polish, persuasion, and visual manipulation
3. **Content-First** - Information hierarchy stripped to essentials; aesthetics serve function
4. **Deliberate Austerity** - Uncompromising, deliberately austere, defiantly unfashionable

### Implementation Patterns

```css
/* Brutalist typography */
body {
  font-family: monospace;
  font-size: 16px;
  line-height: 1.4;
}

/* Raw layout - no decorative margins */
.container {
  max-width: none;
  padding: 20px;
}

/* Harsh contrast */
body {
  background: #fff;
  color: #000;
}

/* Or inverted */
body.dark {
  background: #000;
  color: #fff;
}

/* Utilitarian navigation */
nav a {
  text-decoration: underline;
  color: inherit;
}

/* No hover effects or transitions */
a:hover {
  /* intentionally minimal or none */
}

/* Raw HTML elements, no embellishment */
button {
  border: 2px solid currentColor;
  background: transparent;
  padding: 8px 16px;
  font-family: inherit;
  cursor: pointer;
}
```

### When to Use Brutalism

- Artistic and experimental projects
- Anti-establishment brand positioning
- Developer tools and documentation
- Editorial/magazine content prioritizing text
- Portfolios for designers wanting to stand out

---

## Part 8: Motion Design Principles

Create intentional, impactful animations that enhance rather than distract.

### High-Impact Moments

Focus animation budget on key moments:

```css
/* Page load - staggered reveals */
.hero-content > * {
  opacity: 0;
  transform: translateY(20px);
  animation: fadeInUp 0.6s ease-out forwards;
}

.hero-content > *:nth-child(1) { animation-delay: 0ms; }
.hero-content > *:nth-child(2) { animation-delay: 100ms; }
.hero-content > *:nth-child(3) { animation-delay: 200ms; }

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

### Scroll-Triggered Effects

```css
/* Use Intersection Observer to add class when visible */
.section {
  opacity: 0;
  transform: translateY(40px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}

.section.visible {
  opacity: 1;
  transform: translateY(0);
}
```

### Hover States That Surprise

```css
/* Unexpected but delightful */
.card {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
  transform: translateY(-4px) rotate(-1deg);
  box-shadow: 8px 8px 0 var(--color-accent);
}

/* Or for brutalist/neubrutalist */
.card:hover {
  transform: translate(-4px, -4px);
  box-shadow: 4px 4px 0 #000;
}
```

### Performance Considerations

```css
/* Only animate transform and opacity for smooth 60fps */
.animate-safe {
  transition: transform 0.3s ease, opacity 0.3s ease;
  /* Avoid: width, height, margin, padding, top, left */
}

/* Use will-change sparingly for heavy animations */
.heavy-animation {
  will-change: transform;
}

/* Remove will-change after animation completes */
```

**Modern CSS Alternatives**: Scroll-driven animations (Part 18) can replace JavaScript Intersection Observer patterns. View Transitions API (Part 18) provides native page transition support. For AI-specific loading and streaming animations, see Part 21.

---

## Part 9: Foundational UX Principles

Master these timeless principles that form the foundation of effective interface design.

### Nielsen's 10 Usability Heuristics

**1. Visibility of System Status**
Keep users informed through appropriate feedback within reasonable time. Show loading states, progress indicators, and confirmation messages.

**2. Match Between System and Real World**
Use familiar language and concepts. Follow real-world conventions; make information appear in natural, logical order.

**3. User Control and Freedom**
Provide clear "emergency exits" - undo, redo, cancel buttons. Users often perform actions by mistake and need escape routes.

**4. Consistency and Standards**
Follow platform conventions. Users shouldn't wonder whether different words, situations, or actions mean the same thing.

**5. Error Prevention**
Design to prevent errors before they occur. Use confirmation dialogs for destructive actions; provide helpful constraints.

**6. Recognition Rather Than Recall**
Make elements, actions, and options visible. Minimize memory load by showing information contextually.

**7. Flexibility and Efficiency of Use**
Offer shortcuts for expert users while keeping the interface simple for novices. Support personalization.

**8. Aesthetic and Minimalist Design**
Every extra unit of information competes with relevant information. Remove elements that don't serve the user's goals.

**9. Help Users Recognize, Diagnose, and Recover from Errors**
Express errors in plain language, precisely indicate the problem, and constructively suggest solutions.

**10. Help and Documentation**
Provide searchable, task-focused documentation accessible in context when users need it.

### Key Laws of UX

**Cognitive & Attention**
- **Hick's Law**: Decision time increases with choice quantity and complexity. Minimize options to accelerate decisions.
- **Miller's Law**: Working memory holds ~7±2 items. Present information in groups of 5-9 maximum.
- **Cognitive Load**: Simplify tasks to reduce mental demand. Users have limited processing capacity.

**Visual Perception (Gestalt)**
- **Law of Proximity**: Objects near each other appear grouped. Position related items close together.
- **Law of Similarity**: Similar elements appear unified. Use consistent styling to show relationships.
- **Law of Common Region**: Boundaries create perceived grouping. Use borders/backgrounds to organize.

**Interaction**
- **Fitts's Law**: Target acquisition time depends on distance and size. Make clickable areas appropriately sized.
- **Doherty Threshold**: Response times under 400ms improve productivity. Optimize for perceived speed.
- **Jakob's Law**: Users prefer familiar patterns. Match conventions from platforms users already know.

**Memory & Experience**
- **Peak-End Rule**: Users judge experiences by peak moments and conclusions, not averages. Design memorable highs and strong endings.
- **Von Restorff Effect**: Distinctive items stand out in memory. Highlight important elements through differentiation.
- **Serial Position Effect**: Users remember first and last items best. Prioritize critical information at boundaries.

**Design Philosophy**
- **Aesthetic-Usability Effect**: Beautiful design is perceived as more usable. Visual appeal enhances perceived functionality.
- **Occam's Razor**: Prefer simpler solutions with fewer assumptions over complex ones.
- **Tesler's Law**: All systems contain irreducible complexity. Distribute it appropriately between system and user.
- **Pareto Principle**: 80% of effects stem from 20% of causes. Focus effort on high-impact elements.

---

## Part 10: Humane Design Principles

Design ethically by prioritizing user well-being over engagement metrics.

### The 7 Principles

**1. Empowering**
Prioritize value delivered to users over revenue generation.
- Give users authority over algorithms shaping their experience
- Grant control over personal data and identity management
- Technology should strengthen abilities without intruding unnecessarily
- Maintain user understanding and trust in AI decisions (human in the loop)

**2. Finite**
Respect users' time and attention as limited resources.
- Show "all caught up" indicators when content is exhausted
- Replace infinite scroll with explicit "load more" controls
- Disable autoplay; require conscious user action
- Design experiences with clear endings, not endless engagement

**3. Inclusive**
Enable and draw on the full range of human diversity.
- Build diverse teams to create broader perspectives
- Design for disabilities first; solutions often benefit everyone
- Provide control over accessibility preferences (zoom, contrast, animations)
- Don't disable platform features users depend on

**4. Intentional**
Employ friction to prevent misuse and encourage healthier habits.
- Use confirmation dialogs to minimize mistakes
- Embrace positive friction for more deliberate choices
- Provide mechanisms for users to manage consumption patterns
- Prioritize long-term user benefit over immediate engagement

**5. Respectful**
Safeguard people's time, attention, and digital well-being.
- Align notification delivery with actual urgency
- Allow personalization of notification sources, timing, formats
- Include full content in notifications rather than requiring app visits
- Design technology that adapts to user context

**6. Transparent**
Be clear about intentions, honest in actions, free of dark patterns.
- Clearly explain what users commit to when adopting products
- Articulate what data is gathered and why
- Allow users to view collected information
- Provide the right to be forgotten with easy deletion
- Avoid misdirection; separate ads from content clearly
- Make unsubscribe and exit options easily discoverable

**7. Resilient**
Ensure systems remain stable, reliable, and sustainable.
- Design for long-term user relationships, not exploitation
- Build systems that degrade gracefully
- Support user autonomy rather than dependency

### Anti-Patterns to Avoid

These manipulative patterns violate humane design principles:

- **Infinite scroll** without endpoints (violates Finite)
- **Autoplay** that consumes attention without consent (violates Respectful)
- **Dark patterns** that trick users into actions (violates Transparent)
- **Notification spam** designed to maximize engagement (violates Respectful)
- **Hidden unsubscribe** options (violates Transparent)
- **Confirmation shaming** ("No, I don't want to save money") (violates Respectful)
- **Forced continuity** with difficult cancellation (violates Empowering)

---

## Part 11: Comprehensive Accessibility Checklist

Reference checklist based on WCAG guidelines and A11Y Project standards.

### HTML & Structure
- [ ] Valid HTML (consistent browser/assistive technology support)
- [ ] `lang` attribute on `<html>` element
- [ ] Unique, descriptive page `<title>`
- [ ] Semantic landmark elements (`<nav>`, `<main>`, `<header>`, `<footer>`)
- [ ] Linear content flow (avoid problematic `tabindex` values)
- [ ] No `autofocus` attributes that disrupt navigation

### Headings
- [ ] Heading elements introduce content logically
- [ ] Only one `<h1>` per page
- [ ] Headings in logical sequence (no skipping levels)
- [ ] Headings describe the content that follows

### Keyboard Navigation
- [ ] Visible focus styles on all interactive elements
- [ ] Focus order matches visual layout logically
- [ ] Skip link to main content (visible on focus)
- [ ] All functionality accessible via keyboard
- [ ] No keyboard traps

### Images
- [ ] `alt` attributes on all `<img>` elements
- [ ] Descriptive alt text for informative images
- [ ] Empty `alt=""` for decorative images
- [ ] Text alternatives for complex graphics (charts, maps)

### Forms
- [ ] All inputs have associated `<label>` elements
- [ ] Labels use `for`/`id` pairing correctly
- [ ] Related inputs grouped with `<fieldset>` and `<legend>`
- [ ] Appropriate `autocomplete` attributes
- [ ] Error messages associated with corresponding inputs
- [ ] Don't communicate state through color alone
- [ ] Form errors displayed in list above form after submission

### Links & Buttons
- [ ] Links use `<a>` with `href` attribute
- [ ] Buttons use `<button>` element (not styled `<div>`)
- [ ] Link text is descriptive (not "click here")
- [ ] Links distinguishable not by color alone
- [ ] Warning when links open new tabs/windows

### Color & Contrast
- [ ] Normal text: 4.5:1 contrast ratio minimum
- [ ] Large text (18px+ or 14px+ bold): 3:1 minimum
- [ ] Icons and input borders: 3:1 minimum
- [ ] Information not conveyed by color alone
- [ ] Content tested in high contrast mode
- [ ] Text readable at 200% zoom

### Media
- [ ] No automatic media playback
- [ ] All media can be paused (including via spacebar)
- [ ] Video has captions
- [ ] Audio has transcripts
- [ ] No flashing content that could trigger seizures

### Motion & Animation
- [ ] `prefers-reduced-motion` media query respected
- [ ] Animations subtle, not excessive
- [ ] Parallax and decorative motion can be disabled
- [ ] Infinite scrolling can be turned off

### Mobile & Touch
- [ ] Viewport zoom not disabled
- [ ] Content works in any orientation
- [ ] No horizontal scrolling required
- [ ] Adequate spacing between touch targets (44x44px minimum)
- [ ] Touch targets easily activatable

### Cognitive Accessibility
- [ ] Content chunked into manageable sections (Part 29)
- [ ] Reduced-motion mode eliminates ALL animation, not just reduces it
- [ ] Focus mode available to reduce visual noise
- [ ] Text uses 1.5x line-height minimum, left-aligned (not justified)

---

## Part 12: Dieter Rams' 10 Principles for Good Design

These timeless principles from industrial designer Dieter Rams apply directly to interface design:

1. **Good design is innovative** - Push boundaries; don't settle for conventional solutions
2. **Good design makes a product useful** - Every element must serve the user's goals
3. **Good design is aesthetic** - Visual quality is integral, not superficial
4. **Good design makes a product understandable** - The interface explains itself
5. **Good design is unobtrusive** - Serve the user's purpose without demanding attention
6. **Good design is honest** - Don't pretend to be more than you are; no dark patterns
7. **Good design is long-lasting** - Avoid trendy elements that age quickly
8. **Good design is thorough down to the last detail** - Every pixel matters
9. **Good design is environmentally-friendly** - Optimize performance; respect resources
10. **Good design is as little design as possible** - "Less, but better" - only the essential

---

## Part 13: The 8-Point Grid System

Use multiples of 8 for all spacing, sizing, and layout decisions.

### Core Rules

```css
/* Base spacing scale */
:root {
  --space-1: 4px;   /* Half-step for icons/small text */
  --space-2: 8px;   /* Base unit */
  --space-3: 16px;  /* 2x */
  --space-4: 24px;  /* 3x */
  --space-5: 32px;  /* 4x */
  --space-6: 48px;  /* 6x */
  --space-7: 64px;  /* 8x */
  --space-8: 96px;  /* 12x */
}
```

### Why 8pt Works

- **Consistency**: All measurements follow the same rules
- **Reduced decisions**: Fewer spacing options = faster design + development
- **Multi-platform**: Most screen sizes divide evenly by 8 on at least one axis
- **Scaling**: Works cleanly at 1x, 2x, 3x resolutions

### Implementation Methods

**Hard Grid**: Display actual grid, align all elements to it (like Material Design's 4pt grid)

**Soft Grid**: Measure 8pt between elements without visible grid (better for iOS, faster workflow)

### Typography Exception

Text sizing and line-height don't always conform to 8pt while maintaining readability. Use platform guidelines and typeface-specific metrics, then build UI around established text dimensions.

---

## Part 14: Typography Scale Ratios

Use mathematical ratios for harmonious type hierarchies:

| Ratio | Name | Use Case |
|-------|------|----------|
| 1.067 | Minor Second | Subtle hierarchy, dense UI |
| 1.125 | Major Second | Conservative, professional |
| 1.200 | Minor Third | Balanced, versatile |
| 1.250 | Major Third | Clear distinction |
| 1.333 | Perfect Fourth | Strong hierarchy |
| 1.414 | Augmented Fourth | Dramatic contrast |
| 1.500 | Perfect Fifth | Bold statements |
| 1.618 | Golden Ratio | Classic proportion |

### Applying a Scale

```css
/* Using 1.250 (Major Third) with 16px base */
:root {
  --text-xs: 10px;    /* 16 ÷ 1.25 ÷ 1.25 */
  --text-sm: 13px;    /* 16 ÷ 1.25 */
  --text-base: 16px;  /* Base */
  --text-lg: 20px;    /* 16 × 1.25 */
  --text-xl: 25px;    /* 16 × 1.25² */
  --text-2xl: 31px;   /* 16 × 1.25³ */
  --text-3xl: 39px;   /* 16 × 1.25⁴ */
  --text-4xl: 49px;   /* 16 × 1.25⁵ */
}
```

**Tool**: Use https://typescale.com/ to generate scales with different ratios.

For fluid typography that scales smoothly between breakpoints using `clamp()`, see Part 24. For variable fonts and OpenType features, also Part 24.

---

## Part 15: Spatial System Approaches

### Element-First (Strict Sizing)

Prioritize component dimensions matching your spatial system:

```css
.button {
  height: 40px;  /* Fixed to grid */
  padding: 0 16px;
}
```

Best for: Buttons, form inputs, fixed-height components

### Content-First (Strict Padding)

Enforce consistent padding, let element sizes adapt:

```css
.card {
  padding: 24px;  /* Fixed padding */
  /* Height determined by content */
}
```

Best for: Cards, tables, variable-length content

---

## Part 16: Settings Philosophy

From Linear: "Settings are not a design failure."

### Key Principles

1. **Distinguish preferences from failures** - Some settings address legitimate individual differences, not poor defaults
2. **Settings as onboarding** - Use settings to educate users about capabilities
3. **Emotional connection through details** - Customization creates user attachment
4. **Respect habits** - "Create products that fit into people's lives, not the other way around"

### When to Add Settings

- User habits genuinely vary (keyboard shortcuts, themes)
- Platform conventions differ (Mac vs Windows)
- Accessibility needs vary (motion, contrast)
- Power users need efficiency (density, defaults)

### When NOT to Add Settings

- You're avoiding a design decision
- The "right" answer is knowable through research
- Adding complexity without clear user benefit

---

## Part 17: Comprehensive Learning Resources

### Self-Directed Design Education
- **Degreeless.design** - https://degreeless.design - Complete curriculum for learning design without a degree
- **Lessons of Design** - https://lessons.design - Designer reflections on craft

### Foundational Principles
- **Laws of UX** - https://lawsofux.com - 30 psychological principles
- **Nielsen Norman Group** - https://www.nngroup.com - Usability research
- **Principles.design** - https://principles.design - Design principle collections
- **Dieter Rams' 10 Principles** - https://designmuseum.org - Timeless design philosophy

### Design Process & Methodology
- **IDEO Design Kit** - https://www.designkit.org - Human-centered design methods
- **GV Design Sprints** - http://www.gv.com/sprint/ - 5-day sprint methodology
- **Design Systems** - https://www.designsystems.com - Building and maintaining systems

### Typography
- **Google Fonts Knowledge** - https://fonts.google.com/knowledge - Typography principles
- **Typescale** - https://typescale.com - Type scale generator
- **Fonts In Use** - https://fontsinuse.com - Real-world typography examples
- **Typewolf** - https://www.typewolf.com - Font recommendations
- **Type.lol** - https://type.lol - Typeface foundry directory

### Spacing & Layout
- **8-Point Grid** - https://spec.fm/specifics/8-pt-grid - Grid system methodology
- **Space, Grids and Layouts** - https://www.designsystems.com/space-grids-and-layouts/ - Spatial systems

### Ethical & Humane Design
- **Humane by Design** - https://humanebydesign.com - Ethical design patterns
- **Dark Patterns** - https://www.deceptive.design - Manipulative patterns to avoid
- **Microsoft Inclusive Design** - https://inclusive.microsoft.design - Designing for diversity

### Accessibility
- **The A11Y Project** - https://www.a11yproject.com - Community resources
- **Stark Library** - https://www.getstark.co/library/ - Accessibility toolkit
- **WebAIM** - https://webaim.org - Testing and guidance
- **WCAG Quick Reference** - https://www.w3.org/WAI/WCAG21/quickref/ - Official standards

### Design Systems Reference
- **Material Design** - https://material.io/design/ - Google's system
- **Human Interface Guidelines** - https://developer.apple.com/design/human-interface-guidelines - Apple's system
- **Awesome Design Systems** - https://github.com/alexpate/awesome-design-systems - Curated collection

### Industry Blogs & Publications
- **Google Design** - https://design.google - Google's design practice
- **Brand New** - https://www.underconsideration.com/brandnew/ - Branding analysis
- **UX Collective** - https://uxdesign.cc - UX articles and insights

### Inspiration Galleries
- **Godly.website** - https://godly.website - Exceptional websites
- **Minimal Gallery** - https://minimal.gallery - Minimalist design
- **Httpster** - http://httpster.net - Web design inspiration
- **Hoverstat.es** - https://www.hoverstat.es - Interactive design
- **Really Good Emails** - https://reallygoodemails.com - Email design
- **Landingfolio** - https://www.landingfolio.com - Landing pages
- **SaaSFrame** - https://www.saasframe.io - SaaS interfaces
- **Refero** - https://refero.design - Design references
- **Dribbble** - https://dribbble.com - Designer community

### Books (Essential Reading)
**Foundations:**
- *Thinking With Type* by Ellen Lupton
- *Graphic Design: The New Basics* by Ellen Lupton
- *Grid Systems* by Kimberly Elam
- *The Design of Everyday Things* by Don Norman

**UX & Process:**
- *Just Enough Research* by Erika Hall
- *Sprint* by Jake Knapp
- *The User Experience Team of One* by Leah Buley
- *Mismatch* by Kat Holmes (inclusive design)

### Interactive Learning
- **Kern Type Game** - https://type.method.ac - Practice kerning
- **The Bézier Game** - https://bezier.method.ac - Practice curves
- **Coolors** - https://coolors.co - Color palette generator

### Newsletters
- **HeyDesigner** - https://heydesigner.com - Curated design links
- **Degreeless Weekly** - https://degreeless.substack.com - Learning resources

### Courses
- **Shift Nudge** - https://shiftnudge.com - Interface design
- **Design+Code** - https://designcode.io - Design and development
- **Design System University** - https://designsystem.university - Building systems

### Modern CSS
- **web.dev/blog** - https://web.dev/blog - Chrome team's CSS and performance updates
- **Modern CSS** - https://moderncss.dev - Practical modern CSS solutions
- **State of CSS** - https://stateofcss.com - Annual CSS survey and trends
- **Scroll-Driven Animations** - https://scroll-driven-animations.style - Interactive demos and examples

### Performance
- **web.dev/vitals** - https://web.dev/vitals - Core Web Vitals documentation
- **PageSpeed Insights** - https://pagespeed.web.dev - Performance testing tool

### Fluid Typography
- **Utopia** - https://utopia.fyi - Fluid type and space scale generator
- **Fluid Type Scale** - https://www.fluid-type-scale.com - Type scale calculator with clamp()

### AI Interface Design
- **AI Design Patterns** - https://ai-design-patterns.com - Patterns for AI interfaces
- **AIverse Design** - https://www.aiverse.design - AI UX pattern library

---

## Part 18: Modern CSS Techniques

These features are baseline-available in all evergreen browsers (2025-2026). No polyfills needed. Use them to reduce JavaScript dependency and build more resilient interfaces.

### Container Queries

Make components responsive to their container, not the viewport. Essential for reusable component libraries.

```css
/* Define a containment context */
.card-container {
  container-type: inline-size;
  container-name: card;
}

/* Component adapts to its container width */
@container card (min-width: 400px) {
  .card {
    display: grid;
    grid-template-columns: 200px 1fr;
    gap: 16px;
  }
}

@container card (max-width: 399px) {
  .card {
    display: flex;
    flex-direction: column;
  }

  .card img {
    width: 100%;
    aspect-ratio: 16 / 9;
    object-fit: cover;
  }
}
```

**Key Rule**: Use container queries for component-level responsiveness, media queries for page-level layout. A sidebar card and a main-content card can now use the same component with different layouts.

### The :has() Selector

The most powerful CSS selector added in years. Enables parent-aware styling without JavaScript.

```css
/* Style parent based on child state */
.form-group:has(:invalid) {
  border-color: var(--color-error);
}

/* Layout changes based on content */
.card:has(> img) {
  grid-template-rows: 200px 1fr;
}

.card:not(:has(> img)) {
  grid-template-rows: 1fr;
}

/* Interactive states without JS */
.nav:has(.dropdown:focus-within) .overlay {
  opacity: 1;
  pointer-events: auto;
}

/* Style sibling based on state */
.checkbox:has(:checked) + .label {
  text-decoration: line-through;
  opacity: 0.6;
}
```

**Key Rule**: `:has()` eliminates many JavaScript DOM manipulation patterns. Before writing `classList.toggle()` in JS, check if `:has()` can achieve the same result in CSS.

### CSS Subgrid

Align nested grid children to their parent's grid tracks. Solves the perennial "align cards in a grid" problem.

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 24px;
}

.card {
  display: grid;
  grid-template-rows: subgrid;
  grid-row: span 3; /* title, description, CTA */
}

/* Titles, descriptions, and CTAs now align across all cards
   regardless of content length */
```

### View Transitions API

Animate between view states with native browser support. Replaces complex JavaScript transition libraries.

```css
/* Define elements that should morph between views */
.product-image {
  view-transition-name: product-hero;
}

.product-title {
  view-transition-name: product-title;
}

/* Style the transition */
::view-transition-old(product-hero) {
  animation: fadeOut 0.3s ease-out;
}

::view-transition-new(product-hero) {
  animation: fadeIn 0.3s ease-in;
}
```

```javascript
/* Trigger a view transition */
document.startViewTransition(() => {
  updateDOM(); /* Your state change */
});
```

Cross-reference: Part 8 (Motion Design) for animation principles.

### Scroll-Driven Animations

Replace JavaScript Intersection Observer with pure CSS scroll-triggered animations.

```css
/* Progress bar tied to page scroll */
.reading-progress {
  position: fixed;
  top: 0;
  left: 0;
  height: 3px;
  background: var(--color-primary);
  transform-origin: left;
  animation: growWidth linear;
  animation-timeline: scroll();
}

@keyframes growWidth {
  from { transform: scaleX(0); }
  to { transform: scaleX(1); }
}

/* Fade-in on scroll into view */
.section {
  animation: fadeInUp linear both;
  animation-timeline: view();
  animation-range: entry 0% entry 100%;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(40px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

**Key Rule**: Scroll-driven animations run off-main-thread, making them smoother than JavaScript-based scroll handlers. Always prefer these over Intersection Observer for visual effects.

### CSS Nesting

Write nested styles without a preprocessor. Keeps component styles co-located and readable.

```css
.card {
  padding: var(--space-4);
  border-radius: var(--radius-md);

  & .title {
    font-size: var(--text-lg);
    font-weight: 600;
  }

  & .description {
    color: var(--text-secondary);
  }

  &:hover {
    box-shadow: var(--elevation-2);
  }

  @media (max-width: 768px) {
    padding: var(--space-3);
  }
}
```

**Key Rule**: Limit nesting to 3 levels maximum. Deeper nesting creates specificity problems and is hard to read.

### Anchor Positioning

Position tooltips, popovers, and dropdowns relative to anchor elements without JavaScript positioning libraries.

```css
.trigger {
  anchor-name: --tooltip-anchor;
}

.tooltip {
  position: fixed;
  position-anchor: --tooltip-anchor;
  top: anchor(bottom);
  left: anchor(center);
  translate: -50% 8px;

  /* Auto-flip if overflowing viewport */
  position-try-fallbacks: flip-block;
}
```

### Popover API

Build dismissable overlays with zero JavaScript. Handles focus trapping, backdrop, and light-dismiss behavior natively.

```html
<button popovertarget="menu">Open Menu</button>

<div id="menu" popover>
  <nav>
    <a href="/settings">Settings</a>
    <a href="/profile">Profile</a>
    <a href="/logout">Log out</a>
  </nav>
</div>
```

```css
[popover] {
  /* Positioned in top layer automatically */
  padding: var(--space-3);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  box-shadow: var(--elevation-3);
}

/* Style the backdrop */
[popover]::backdrop {
  background: rgba(0, 0, 0, 0.3);
}
```

**Key Rule**: Use Popover API for any light-dismiss behavior (dropdown menus, tooltips, popovers) instead of custom click-outside handlers.

### Cascade Layers Preview

Organize CSS priority without fighting specificity. Deep dive in Part 31.

```css
/* Declare layer order - first declared = lowest priority */
@layer reset, base, tokens, components, utilities, overrides;

@layer components {
  .button { background: var(--color-primary); }
}

@layer utilities {
  .bg-red { background: red; } /* Wins over .button despite lower specificity */
}
```

### Quick Reference

| Feature | Replaces | Use Case |
|---------|----------|----------|
| Container queries | Media queries for components | Reusable responsive components |
| `:has()` | JS class toggling | Parent-aware styling |
| Subgrid | Manual alignment hacks | Consistent grid children |
| View Transitions | JS transition libraries | Page/state transitions |
| Scroll-driven animations | Intersection Observer | Scroll-triggered effects |
| CSS nesting | Sass/Less nesting | Scoped component styles |
| Anchor positioning | JS positioning (Popper/Floating UI) | Tooltips, dropdowns |
| Popover API | Custom modal/dropdown JS | Light-dismiss overlays |
| `@layer` | Specificity management hacks | Design system CSS ordering |

---

## Part 19: Performance-First Design (Core Web Vitals)

Beautiful design means nothing if it takes 5 seconds to load. Design decisions directly impact performance metrics.

### The Three Metrics

| Metric | Good | Needs Work | Poor | What It Measures |
|--------|------|------------|------|------------------|
| LCP (Largest Contentful Paint) | ≤ 2.5s | ≤ 4.0s | > 4.0s | Largest visible element loads |
| INP (Interaction to Next Paint) | ≤ 200ms | ≤ 500ms | > 500ms | Interactions feel instant |
| CLS (Cumulative Layout Shift) | ≤ 0.1 | ≤ 0.25 | > 0.25 | Nothing jumps around |

### CLS Prevention Patterns

Layout shift is the most common design-caused performance issue. Prevent it at the design level.

```css
/* ALWAYS set dimensions on images */
img {
  width: 100%;
  height: auto;
  aspect-ratio: 16 / 9; /* Browser reserves space before load */
}

/* Reserve space for dynamic content */
.embed-container {
  min-height: 300px;
  contain: layout;
}

/* Prevent font swap layout shift */
@font-face {
  font-family: 'Display';
  src: url('/fonts/display.woff2') format('woff2');
  font-display: swap;
  /* Match fallback metrics to reduce reflow */
  size-adjust: 105%;
  ascent-override: 90%;
  descent-override: 20%;
}
```

**Key Rule**: Every element that loads asynchronously (images, embeds, fonts, lazy content) must have its space reserved before it arrives.

### LCP Optimization

Identify your LCP element (usually a hero image or headline) and prioritize it.

```html
<!-- Preload LCP image -->
<link rel="preload" as="image" href="/hero.avif" type="image/avif">

<!-- High priority on LCP image - never lazy-load this -->
<img src="/hero.avif" alt="Hero" fetchpriority="high" width="1200" height="600">

<!-- Inline critical CSS for above-the-fold content -->
<style>
  /* Only styles needed for initial viewport */
  .hero { display: grid; grid-template-columns: 1fr 1fr; min-height: 80vh; }
  .hero-title { font-size: clamp(2rem, 5vw, 4rem); }
</style>

<!-- Defer non-critical CSS -->
<link rel="stylesheet" href="/styles.css" media="print" onload="this.media='all'">
```

### INP Optimization

Keep interactions feeling instant by yielding to the main thread.

```javascript
/* Break up long tasks */
async function handleFilterChange(filters) {
  updateFilterUI(filters);       /* Visual feedback first */
  await scheduler.yield();        /* Let browser paint */
  const results = filterData(filters);  /* Heavy computation */
  await scheduler.yield();
  renderResults(results);         /* Update DOM */
}
```

```css
/* Use CSS for interactions where possible - no JS overhead */
details[open] .content {
  animation: slideDown 0.2s ease-out;
}

/* CSS-only accordion is faster than JS accordion */
```

### Skeleton Loaders

Skeletons prevent CLS by reserving exact space for incoming content.

```css
.skeleton {
  --skeleton-base: hsl(0 0% 88%);
  --skeleton-shine: hsl(0 0% 96%);
  background: linear-gradient(
    90deg,
    var(--skeleton-base) 25%,
    var(--skeleton-shine) 50%,
    var(--skeleton-base) 75%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite linear;
  border-radius: var(--radius-sm);
}

@keyframes shimmer {
  to { background-position: -200% 0; }
}

/* Dark mode skeleton */
@media (prefers-color-scheme: dark) {
  .skeleton {
    --skeleton-base: hsl(0 0% 18%);
    --skeleton-shine: hsl(0 0% 25%);
  }
}

/* Skeleton must match exact dimensions of real content */
.skeleton-title { height: 28px; width: 60%; }
.skeleton-text { height: 16px; width: 100%; }
.skeleton-avatar { height: 48px; width: 48px; border-radius: 50%; }
```

**Key Rule**: Skeletons must match the exact dimensions of the content they replace. A mismatched skeleton is worse than no skeleton because it causes shift when real content arrives.

### Animation Performance Budget

```css
/* SAFE to animate (compositor-only, GPU-accelerated) */
.animate-safe {
  transition: transform 0.3s ease, opacity 0.3s ease;
}

/* NEVER animate (triggers layout recalculation) */
/* width, height, margin, padding, top, left, right, bottom,
   border, box-shadow (with spread changes), font-size */

/* Use will-change sparingly - only for heavy animations */
.heavy-animation {
  will-change: transform;
}
/* Remove will-change after animation completes */

/* Contain layout-heavy sections */
.animated-section {
  contain: layout paint;
}
```

### Resource Hints

```html
<!-- Preload: critical resources for THIS page -->
<link rel="preload" as="font" href="/fonts/display.woff2" type="font/woff2" crossorigin>
<link rel="preload" as="image" href="/hero.avif">

<!-- Preconnect: establish early connections to critical origins -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://api.example.com">

<!-- Prefetch: resources for NEXT likely navigation -->
<link rel="prefetch" href="/dashboard.js">

<!-- DNS Prefetch: resolve DNS for third-party domains -->
<link rel="dns-prefetch" href="https://analytics.example.com">
```

| Hint | When to Use | Impact |
|------|-------------|--------|
| `preload` | Critical above-the-fold resources | Reduces LCP |
| `preconnect` | APIs, font hosts, CDNs | Reduces connection time |
| `prefetch` | Next page resources | Faster navigation |
| `dns-prefetch` | Third-party domains | Minor latency reduction |
| `fetchpriority="high"` | LCP image/resource | Browser prioritization |

### Performance Checklist

- [ ] LCP element identified and has `fetchpriority="high"`
- [ ] All images have explicit `width`/`height` or `aspect-ratio`
- [ ] Fonts use `font-display: swap` with `size-adjust` fallback
- [ ] Skeleton loaders match exact content dimensions
- [ ] Only `transform`/`opacity` animated (never layout properties)
- [ ] Critical CSS inlined for above-the-fold content
- [ ] Resource hints applied for key assets and origins

---

## Part 20: Dark Mode & Theming

Dark mode is not "invert the colors." It requires intentional design decisions about depth, contrast, and color behavior.

### System Preference Detection

```css
/* CSS-first approach (recommended) */
:root {
  color-scheme: light dark; /* Tells browser to style form controls */

  /* Light mode tokens (default) */
  --color-surface-0: #ffffff;
  --color-surface-1: #f5f5f5;
  --color-surface-2: #ebebeb;
  --color-text-primary: #1a1a1a;
  --color-text-secondary: #666666;
  --color-border: #e0e0e0;
  --color-interactive: hsl(220, 90%, 50%);
}

@media (prefers-color-scheme: dark) {
  :root {
    --color-surface-0: #121212;
    --color-surface-1: #1e1e1e;
    --color-surface-2: #2a2a2a;
    --color-text-primary: #e5e5e5;
    --color-text-secondary: #a0a0a0;
    --color-border: rgba(255, 255, 255, 0.12);
    --color-interactive: hsl(220, 70%, 65%);
  }
}
```

### User Override Pattern

Always allow users to override system preference. Use a three-state toggle: System / Light / Dark.

```css
/* Theme applied via data attribute */
[data-theme="light"] {
  --color-surface-0: #ffffff;
  --color-text-primary: #1a1a1a;
  /* ... light tokens ... */
}

[data-theme="dark"] {
  --color-surface-0: #121212;
  --color-text-primary: #e5e5e5;
  /* ... dark tokens ... */
}
```

```javascript
/* Three-state toggle with system fallback */
function setTheme(preference) {
  if (preference === 'system') {
    document.documentElement.removeAttribute('data-theme');
    localStorage.removeItem('theme');
  } else {
    document.documentElement.setAttribute('data-theme', preference);
    localStorage.setItem('theme', preference);
  }
}

/* Restore on page load (run in <head> to prevent flash) */
const saved = localStorage.getItem('theme');
if (saved) document.documentElement.setAttribute('data-theme', saved);
```

**Key Rule**: Always default to system preference. Never force a theme. Run the restore script in `<head>` to prevent a flash of wrong theme (FOWT).

### The light-dark() CSS Function

Concise inline theme switching for simple cases.

```css
:root {
  color-scheme: light dark;
}

.text {
  color: light-dark(#1a1a1a, #e5e5e5);
}

.surface {
  background: light-dark(#ffffff, #121212);
}

.border {
  border-color: light-dark(#e0e0e0, rgba(255, 255, 255, 0.12));
}
```

Use `light-dark()` for simple one-off values. Use custom properties for values referenced in multiple places.

### Color Adjustments for Dark Mode

Colors that look great on light backgrounds often look harsh on dark backgrounds.

```css
:root {
  /* Light mode: high saturation, lower lightness */
  --color-primary: hsl(220, 90%, 50%);
  --color-success: hsl(145, 80%, 38%);
  --color-error: hsl(0, 85%, 50%);
}

@media (prefers-color-scheme: dark) {
  :root {
    /* Dark mode: reduce saturation ~20%, increase lightness */
    --color-primary: hsl(220, 70%, 65%);
    --color-success: hsl(145, 60%, 55%);
    --color-error: hsl(0, 65%, 60%);
  }
}

/* Text: never use pure white on dark. Use off-white. */
/* #e5e5e5 or rgba(255, 255, 255, 0.87) reduces eye strain */
```

**Key Rule**: Desaturate colors ~20% and increase lightness for dark mode. Pure white text on pure black is harder to read than off-white on dark gray.

### Depth Without Shadows

Shadows are nearly invisible on dark backgrounds. Use surface elevation instead.

```css
/* Dark mode depth = lighter surfaces at higher elevation */
:root {
  --surface-0: #121212; /* Base/background */
  --surface-1: #1e1e1e; /* Cards, bottom sheets */
  --surface-2: #232323; /* Raised cards, app bars */
  --surface-3: #292929; /* Modals, dropdowns */
  --surface-4: #333333; /* Tooltips, popovers */
}

/* Subtle borders for edge definition */
.card {
  background: var(--surface-1);
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.modal {
  background: var(--surface-3);
  border: 1px solid rgba(255, 255, 255, 0.12);
}

/* Light mode still uses shadows normally */
@media (prefers-color-scheme: light) {
  .card { box-shadow: var(--elevation-1); border: none; }
  .modal { box-shadow: var(--elevation-4); border: none; }
}
```

### Multi-Theme Token Architecture

Support more than just light/dark. High-contrast and brand themes use the same token system.

| Token | Light | Dark | High Contrast |
|-------|-------|------|---------------|
| `--surface-0` | `#ffffff` | `#121212` | `#000000` |
| `--text-primary` | `#1a1a1a` | `#e5e5e5` | `#ffffff` |
| `--border` | `#e0e0e0` | `rgba(255,255,255,0.12)` | `#ffffff` |
| `--interactive` | `hsl(220,90%,50%)` | `hsl(220,70%,65%)` | `hsl(220,100%,70%)` |

```css
/* Windows High Contrast Mode */
@media (forced-colors: active) {
  .button {
    border: 2px solid ButtonText;
    background: ButtonFace;
    color: ButtonText;
  }

  .button:hover {
    background: Highlight;
    color: HighlightText;
  }

  /* forced-colors uses system keywords, not custom values */
}
```

Cross-reference: Part 30 (Design Token Architecture) for the full three-tier token system.

### Image & Media in Dark Mode

```css
/* Reduce image brightness in dark mode to prevent glare */
@media (prefers-color-scheme: dark) {
  img:not([src$=".svg"]) {
    filter: brightness(0.85);
  }

  /* SVG icons using currentColor adapt automatically */
  .icon { color: var(--text-primary); }
}
```

```html
<!-- Serve different images per theme -->
<picture>
  <source srcset="/hero-dark.avif" media="(prefers-color-scheme: dark)">
  <img src="/hero-light.avif" alt="Hero illustration">
</picture>
```

### Dark Mode Anti-Patterns

| Anti-Pattern | Problem | Fix |
|-------------|---------|-----|
| Pure black (`#000`) backgrounds | Harsh contrast, eye strain | Use `#121212` or similar dark gray |
| Saturated colors on dark | Optical vibration, fatigue | Desaturate ~20%, increase lightness |
| Inverted shadows | Shadows invisible on dark | Use surface elevation (lighter = higher) |
| Forgetting scrollbar | System scrollbar clashes | `color-scheme: dark` or custom scrollbar CSS |
| Forgetting form defaults | Native inputs stay light | `color-scheme: dark` on `:root` |
| Flash of wrong theme | Theme loads after paint | Run theme script in `<head>` |

---

## Part 21: AI-Era Design Patterns

AI interfaces break traditional UI conventions: response times are unpredictable, outputs vary in length and quality, and confidence is uncertain. These patterns address the unique UX challenges of AI-powered products.

### Streaming UI

Chat and generative interfaces must handle token-by-token output gracefully.

```css
/* Streaming text with typing cursor */
.message.streaming {
  /* Content appended via JavaScript */
}

.message.streaming::after {
  content: '|';
  color: var(--color-interactive);
  animation: blink 1s step-end infinite;
  margin-left: 2px;
}

@keyframes blink {
  50% { opacity: 0; }
}

/* Auto-scroll container */
.chat-messages {
  overflow-y: auto;
  overscroll-behavior: contain;
  scroll-behavior: smooth;
}
```

```javascript
/* Smart auto-scroll: only scroll if user is at bottom */
function shouldAutoScroll(container) {
  const threshold = 100;
  const distanceFromBottom =
    container.scrollHeight - container.scrollTop - container.clientHeight;
  return distanceFromBottom < threshold;
}

/* Pause auto-scroll when user scrolls up to read history */
```

**Key Rule**: Always auto-scroll during streaming if the user is at the bottom. Stop auto-scrolling if they've scrolled up to read history. Show a "scroll to bottom" button when they're not at the latest message.

### AI Loading States

AI loading is different from traditional loading: duration is unpredictable and can range from 1 second to 2 minutes.

```css
/* Phase-based loading indicator */
.ai-loading {
  display: flex;
  align-items: center;
  gap: 8px;
  color: var(--text-secondary);
}

.ai-loading .dots span {
  display: inline-block;
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: var(--color-interactive);
  animation: pulse 1.4s ease-in-out infinite;
}

.ai-loading .dots span:nth-child(2) { animation-delay: 0.2s; }
.ai-loading .dots span:nth-child(3) { animation-delay: 0.4s; }

@keyframes pulse {
  0%, 80%, 100% { opacity: 0.3; transform: scale(0.8); }
  40% { opacity: 1; transform: scale(1); }
}

/* Show elapsed time after 3 seconds */
.ai-loading .elapsed {
  font-size: var(--text-sm);
  color: var(--text-tertiary);
  opacity: 0;
  animation: fadeIn 0.3s ease forwards 3s;
}
```

```html
<div class="ai-loading">
  <div class="dots"><span></span><span></span><span></span></div>
  <span class="phase">Analyzing your request...</span>
  <span class="elapsed">12s</span>
  <button class="cancel" aria-label="Cancel generation">Stop</button>
</div>
```

**Key Rule**: Skeleton loaders are wrong for AI content because the structure is unknown. Use animated indicators with phase text. Always show a cancel button. Show elapsed time after 3+ seconds.

### Confidence Indicators

When AI certainty varies, make it visible. Users trust AI more when it admits what it doesn't know.

```css
/* Confidence badge */
.confidence {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  padding: 2px 8px;
  border-radius: var(--radius-sm);
  font-size: var(--text-sm);
}

.confidence--high {
  background: hsl(145, 60%, 90%);
  color: hsl(145, 80%, 25%);
}

.confidence--medium {
  background: hsl(40, 80%, 90%);
  color: hsl(40, 90%, 25%);
}

.confidence--low {
  background: hsl(0, 60%, 92%);
  color: hsl(0, 70%, 30%);
}
```

```html
<!-- Source attribution inline -->
<p>
  The population of Tokyo is approximately 14 million.
  <a href="#source-1" class="source-ref" aria-label="Source 1">[1]</a>
</p>
```

### Explainability & Transparency UX

```html
<!-- Expandable reasoning panel -->
<div class="ai-response">
  <div class="response-content">...</div>
  <details class="reasoning">
    <summary>How AI reached this conclusion</summary>
    <ol class="reasoning-steps">
      <li>Analyzed 3 data sources for population statistics</li>
      <li>Cross-referenced with 2023 census data</li>
      <li>Applied seasonal adjustment factor</li>
    </ol>
  </details>
</div>
```

```css
.reasoning {
  margin-top: var(--space-3);
  padding: var(--space-3);
  background: var(--surface-1);
  border-radius: var(--radius-md);
  font-size: var(--text-sm);
}

.reasoning summary {
  cursor: pointer;
  color: var(--text-secondary);
  font-weight: 500;
}

.reasoning summary:hover {
  color: var(--text-primary);
}
```

### Human-in-the-Loop Controls

AI output should be editable, not read-only. Users need to correct, refine, and direct.

```css
/* Action bar for AI responses */
.response-actions {
  display: flex;
  gap: 4px;
  padding-top: var(--space-2);
  border-top: 1px solid var(--border);
  margin-top: var(--space-3);
}

.response-actions button {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  padding: 4px 8px;
  border: none;
  background: transparent;
  color: var(--text-secondary);
  font-size: var(--text-sm);
  border-radius: var(--radius-sm);
  cursor: pointer;
}

.response-actions button:hover {
  background: var(--surface-1);
  color: var(--text-primary);
}
```

```html
<div class="response-actions">
  <button aria-label="Copy response"><svg>...</svg> Copy</button>
  <button aria-label="Edit response"><svg>...</svg> Edit</button>
  <button aria-label="Regenerate response"><svg>...</svg> Regenerate</button>
  <button aria-label="Report issue"><svg>...</svg> Report</button>
  <div class="feedback" role="group" aria-label="Rate response">
    <button aria-label="Good response"><svg>...</svg></button>
    <button aria-label="Bad response"><svg>...</svg></button>
  </div>
</div>
```

### Error Handling for AI

AI failures need different patterns than traditional errors because users need manual fallback paths.

```html
<div class="ai-error" role="alert">
  <div class="error-icon"><!-- warning icon --></div>
  <div class="error-content">
    <p class="error-title">AI couldn't complete this request</p>
    <p class="error-detail">The model is temporarily overloaded. Your input has been saved.</p>
  </div>
  <div class="error-actions">
    <button class="retry">Try again</button>
    <button class="manual-fallback">Do it manually</button>
  </div>
</div>
```

Design principles for AI errors:
- **Explain what happened** in plain language (not error codes)
- **Preserve user input** so they don't have to re-type
- **Offer retry** with a single click
- **Provide manual fallback** so the user isn't stuck
- **Show partial results** if the AI got partway through

### User Control Over AI

```html
<!-- Settings that respect user agency -->
<div class="ai-settings">
  <label>
    Response length
    <select>
      <option>Concise</option>
      <option>Balanced</option>
      <option>Detailed</option>
    </select>
  </label>

  <label>
    <input type="checkbox" checked>
    Show confidence indicators
  </label>

  <label>
    <input type="checkbox" checked>
    Show reasoning steps
  </label>

  <button class="clear-context">Clear conversation history</button>
</div>
```

**Key Rule**: User control > perceived AI capability. Explicit controls and predictability matter more than hidden automation. Always let users stop, undo, regenerate, and edit AI output.

### AI Interface Quick Reference

| Pattern | Use When | Anti-Pattern |
|---------|----------|--------------|
| Streaming with cursor | Real-time text generation | Waiting for full response then dumping it |
| Phase-based loading | AI processing > 1 second | Generic spinner with no context |
| Confidence indicators | Output certainty varies | Presenting everything with equal authority |
| Expandable reasoning | Complex multi-step AI decisions | Black-box output with no explanation |
| Response action bar | Users need to act on AI output | Read-only AI responses |
| Manual fallback | AI unavailable or fails | Dead-end error states |

---

## Part 22: Advanced Interaction Design

Good interaction design makes an interface feel alive and responsive. Every component has multiple states, and transitions between them matter as much as the states themselves.

### Micro-Interaction Taxonomy

Micro-interactions follow a four-part structure: Trigger → Rules → Feedback → Loops/Modes.

```css
/* Button with multi-state feedback */
.button {
  transition: transform 0.1s ease, box-shadow 0.1s ease;
}

/* Hover: anticipation */
.button:hover {
  transform: translateY(-1px);
  box-shadow: var(--elevation-2);
}

/* Active: confirmation */
.button:active {
  transform: translateY(0) scale(0.98);
  box-shadow: none;
}

/* Loading: system status */
.button[aria-busy="true"] {
  pointer-events: none;
  opacity: 0.7;
}

.button[aria-busy="true"]::after {
  content: '';
  width: 14px;
  height: 14px;
  border: 2px solid currentColor;
  border-top-color: transparent;
  border-radius: 50%;
  animation: spin 0.6s linear infinite;
  margin-left: 8px;
}

/* Success: completion feedback */
.button.success {
  background: var(--color-success);
}

@keyframes spin {
  to { transform: rotate(360deg); }
}
```

**Key Rule**: Every interactive element needs at least four visual states: default, hover, active/pressed, and disabled. Important actions also need loading and success/error states.

### Gesture Design

Design for touch interfaces with gesture alternatives for keyboard/mouse users.

| Gesture | Common Use | Non-Gesture Alternative |
|---------|-----------|------------------------|
| Swipe horizontal | Dismiss, navigate | Delete button, back/forward buttons |
| Swipe vertical | Pull-to-refresh, reveal | Refresh button, scroll to load |
| Long-press | Context menu, selection | Right-click, checkbox selection |
| Pinch | Zoom | Zoom buttons, slider |
| Double-tap | Quick action, zoom | Button, toggle |

**Key Rule**: Every gesture must have a visible, tappable alternative. Gestures are shortcuts, not the only path. Include onboarding hints for discoverable gestures.

### Progressive Disclosure

Show only essential options first. Reveal complexity on demand.

```html
<!-- Zero-JS progressive disclosure with details/summary -->
<details>
  <summary>Advanced settings</summary>
  <div class="advanced-options">
    <!-- Complex options hidden until requested -->
  </div>
</details>
```

```css
details .advanced-options {
  padding-top: var(--space-3);
  animation: slideDown 0.2s ease-out;
}

@keyframes slideDown {
  from { opacity: 0; transform: translateY(-8px); }
  to { opacity: 1; transform: translateY(0); }
}

summary {
  cursor: pointer;
  color: var(--color-interactive);
  font-weight: 500;
  list-style: none;
}

summary::before {
  content: '+ ';
}

details[open] summary::before {
  content: '− ';
}
```

### State-Based Design

Every component exists in multiple states. Design all of them intentionally.

| State | Design Treatment | Example |
|-------|-----------------|---------|
| Empty | Illustration + CTA + explanation | "No messages yet. Start a conversation." |
| Loading | Skeleton matching content dimensions | Shimmer placeholders |
| Partial | Show what's available + loading indicator | 3 of 10 items loaded |
| Complete | Full content with actions | List with items |
| Error | Explain problem + retry action + manual fallback | "Couldn't load. Retry / Go to settings" |
| Offline | Cached content + offline indicator | "You're offline. Showing saved data." |

```css
/* Empty state */
.empty-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: var(--space-8) var(--space-4);
  text-align: center;
  color: var(--text-secondary);
}

.empty-state .illustration {
  width: 200px;
  height: 200px;
  margin-bottom: var(--space-4);
  opacity: 0.6;
}

.empty-state .title {
  font-size: var(--text-lg);
  color: var(--text-primary);
  margin-bottom: var(--space-2);
}

.empty-state .cta {
  margin-top: var(--space-4);
}
```

**Key Rule**: Empty states and error states are design opportunities, not afterthoughts. A well-designed empty state guides users toward their first action.

### State Transitions

Animate between states to help users understand what changed.

```css
/* Smooth transition from loading to populated */
.content-area {
  transition: opacity 0.3s ease;
}

.content-area[data-state="loading"] {
  opacity: 0.6;
}

.content-area[data-state="complete"] {
  opacity: 1;
}

/* List items enter with stagger */
.list-item {
  opacity: 0;
  transform: translateY(10px);
  animation: enterItem 0.3s ease forwards;
}

.list-item:nth-child(1) { animation-delay: 0ms; }
.list-item:nth-child(2) { animation-delay: 50ms; }
.list-item:nth-child(3) { animation-delay: 100ms; }
.list-item:nth-child(4) { animation-delay: 150ms; }
/* Cap at ~5 staggered items to avoid slow-feeling loads */

@keyframes enterItem {
  to { opacity: 1; transform: translateY(0); }
}
```

### Scroll-Based Storytelling

Use scroll position to drive narrative through content sections.

```css
/* Sticky context retention */
.story-section {
  position: relative;
  min-height: 100vh;
}

.story-section .sticky-context {
  position: sticky;
  top: 0;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.story-section .scroll-content {
  position: relative;
  z-index: 1;
}

/* Parallax done right: subtle, single-axis, respects user preference */
@media (prefers-reduced-motion: no-preference) {
  .parallax-element {
    animation: parallax linear;
    animation-timeline: scroll();
  }

  @keyframes parallax {
    from { transform: translateY(-20px); }
    to { transform: translateY(20px); }
  }
}
```

Cross-reference: Part 18 (Modern CSS) for scroll-driven animation syntax. Part 8 (Motion) for performance rules.

---

## Part 23: Data Visualization & Dashboard Design

Data-heavy interfaces require different design principles than marketing pages. Prioritize clarity, information density, and accurate representation.

### Tufte's Core Principles

Edward Tufte's foundational rules for honest, effective data graphics:

1. **Maximize data-ink ratio**: every pixel of ink should present data or aid comprehension of data. If a visual element doesn't encode data, remove it.
2. **Eliminate chart junk**: decorative gridlines, 3D effects, excessive legends, gradient fills, and ornamental elements that don't serve the data.
3. **Small multiples**: repeat the same chart type with different data slices for easy comparison. Faster to read than one complex chart.
4. **Graphical integrity**: represent quantities honestly. No truncated axes, no 3D distortion, no area tricks.

**Key Rule**: "If a visual element doesn't encode data, remove it." This applies to gridlines, backgrounds, borders, and decorative elements on charts.

### Information Density

```css
/* Sparkline: word-sized data graphic inline with text */
.sparkline {
  display: inline-block;
  width: 60px;
  height: 16px;
  vertical-align: middle;
}

.sparkline svg {
  width: 100%;
  height: 100%;
}

/* High-density table: condensed for scanning */
.data-table--dense th,
.data-table--dense td {
  padding: 4px 8px;
  font-size: var(--text-sm);
}

/* Monospace numbers for column alignment */
.data-table td.numeric {
  font-variant-numeric: tabular-nums;
  text-align: right;
  font-family: var(--font-mono);
}
```

### Dashboard Layout Patterns

```css
/* KPI bar: key metrics at top */
.kpi-bar {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: var(--space-3);
  padding: var(--space-3);
}

.kpi-card {
  padding: var(--space-3);
  background: var(--surface-1);
  border-radius: var(--radius-md);
}

.kpi-card .label {
  font-size: var(--text-sm);
  color: var(--text-secondary);
  margin-bottom: var(--space-1);
}

.kpi-card .value {
  font-size: var(--text-2xl);
  font-weight: 700;
  font-variant-numeric: tabular-nums;
}

.kpi-card .trend {
  font-size: var(--text-sm);
  margin-top: var(--space-1);
}

.kpi-card .trend--up { color: var(--color-success); }
.kpi-card .trend--down { color: var(--color-error); }

/* Grid dashboard with priority-based sizing */
.dashboard-grid {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-auto-rows: minmax(200px, auto);
  gap: var(--space-3);
}

.widget--primary { grid-column: span 8; grid-row: span 2; }
.widget--secondary { grid-column: span 4; }
.widget--full { grid-column: span 12; }

/* Mobile: single column, priority ordering */
@media (max-width: 768px) {
  .dashboard-grid {
    grid-template-columns: 1fr;
  }

  .widget--primary,
  .widget--secondary,
  .widget--full {
    grid-column: span 1;
    grid-row: span 1;
  }
}
```

### Chart Accessibility

```html
<!-- Accessible chart container -->
<figure role="img" aria-label="Monthly revenue for 2025, showing growth from $2M in January to $3.4M in December">
  <div class="chart-container">
    <!-- Chart rendered here (SVG, Canvas, etc.) -->
  </div>
  <figcaption>Monthly Revenue 2025</figcaption>
</figure>

<!-- Provide data table fallback for screen readers -->
<details class="sr-data-table">
  <summary class="visually-hidden">View data as table</summary>
  <table>
    <caption>Monthly Revenue 2025</caption>
    <thead><tr><th>Month</th><th>Revenue</th></tr></thead>
    <tbody>
      <tr><td>January</td><td>$2,000,000</td></tr>
      <!-- ... -->
    </tbody>
  </table>
</details>
```

- Don't rely on color alone to distinguish data series: add patterns, labels, or distinct shapes
- Ensure keyboard navigable data points for interactive charts
- Provide `aria-label` or linked description for every chart

### Real-Time Data Display

```css
/* Animated counter for live metrics */
.live-metric {
  font-variant-numeric: tabular-nums;
  transition: color 0.3s ease;
}

/* Flash on value change */
.live-metric.updated {
  animation: valueFlash 0.6s ease;
}

@keyframes valueFlash {
  0% { background: var(--color-interactive-subtle); }
  100% { background: transparent; }
}

/* Stale data indicator */
.data-timestamp {
  font-size: var(--text-xs);
  color: var(--text-tertiary);
}

.data-timestamp.stale {
  color: var(--color-warning);
}

.data-timestamp.stale::before {
  content: '⚠ ';
}
```

**Key Rule**: Batch real-time updates to prevent visual noise. Update at most every 1-2 seconds for numbers, 5-10 seconds for charts. Always show the timestamp of the last update.

### Table Design

```css
/* Well-structured data table */
.data-table {
  width: 100%;
  border-collapse: collapse;
}

.data-table thead {
  position: sticky;
  top: 0;
  z-index: 1;
  background: var(--surface-0);
}

.data-table th {
  text-align: left;
  padding: var(--space-2) var(--space-3);
  font-size: var(--text-sm);
  font-weight: 600;
  color: var(--text-secondary);
  border-bottom: 2px solid var(--border);
  white-space: nowrap;
  user-select: none;
}

/* Sortable column indicator */
.data-table th[aria-sort] {
  cursor: pointer;
}

.data-table th[aria-sort="ascending"]::after {
  content: ' ↑';
}

.data-table th[aria-sort="descending"]::after {
  content: ' ↓';
}

.data-table td {
  padding: var(--space-2) var(--space-3);
  border-bottom: 1px solid var(--border);
  font-size: var(--text-sm);
}

/* Subtle zebra striping */
.data-table tbody tr:nth-child(even) {
  background: var(--surface-1);
}

/* Row hover */
.data-table tbody tr:hover {
  background: var(--color-interactive-subtle);
}

/* Sticky first column for wide tables */
@media (max-width: 768px) {
  .data-table-wrapper {
    overflow-x: auto;
  }

  .data-table th:first-child,
  .data-table td:first-child {
    position: sticky;
    left: 0;
    background: var(--surface-0);
    z-index: 1;
  }
}
```

Use pagination for data tables (not infinite scroll). Virtual scrolling only for datasets > 1,000 rows.

### Color in Data Visualization

| Palette Type | Use Case | Example |
|-------------|----------|---------|
| Sequential | Continuous data (0-100) | Light blue → dark blue |
| Diverging | Positive/negative around center | Red ← neutral → green |
| Categorical | Distinct groups (max 8-10) | Distinct hues per category |

Always test charts with colorblind simulators (deuteranopia, protanopia, tritanopia). Cross-reference: Color Palette skill for generation tools.

---

## Part 24: Fluid & Responsive Typography

Stop using breakpoints for font sizes. Use fluid typography that scales smoothly between any viewport width.

### CSS clamp() for Fluid Type

```css
/* Syntax: clamp(minimum, preferred, maximum) */
/* preferred uses viewport units for smooth scaling */

:root {
  --text-xs: clamp(0.625rem, 0.55rem + 0.3vw, 0.75rem);
  --text-sm: clamp(0.75rem, 0.65rem + 0.4vw, 0.875rem);
  --text-base: clamp(0.875rem, 0.75rem + 0.5vw, 1rem);
  --text-lg: clamp(1rem, 0.8rem + 0.8vw, 1.25rem);
  --text-xl: clamp(1.25rem, 0.9rem + 1.4vw, 1.75rem);
  --text-2xl: clamp(1.5rem, 1rem + 2vw, 2.25rem);
  --text-3xl: clamp(1.875rem, 1rem + 3.5vw, 3rem);
  --text-4xl: clamp(2.25rem, 1rem + 5vw, 4rem);
}

/* Apply semantically */
h1 { font-size: var(--text-4xl); }
h2 { font-size: var(--text-3xl); }
h3 { font-size: var(--text-2xl); }
body { font-size: var(--text-base); }
.caption { font-size: var(--text-sm); }
```

**Key Rule**: Set `min` for mobile readability, `max` for desktop restraint, `preferred` for smooth scaling. Use https://utopia.fyi/ to generate fluid scales.

### Variable Fonts

One font file, infinite weights and widths. Better performance and design flexibility.

```css
@font-face {
  font-family: 'Display';
  src: url('/fonts/display-variable.woff2') format('woff2-variations');
  font-weight: 100 900;
  font-display: swap;
}

/* Fine-tuned weight hierarchy */
.heading { font-weight: 720; }
.subheading { font-weight: 580; }
.body { font-weight: 400; }
.caption { font-weight: 350; }

/* Animate weight on interaction */
.nav-link {
  font-weight: 400;
  transition: font-weight 0.2s ease;
}

.nav-link:hover,
.nav-link[aria-current="page"] {
  font-weight: 650;
}

/* Responsive weight: bolder on large screens, lighter on small */
h1 {
  font-weight: clamp(600, 500 + 2vw, 800);
}
```

Performance benefit: one variable font file replaces multiple static font files, significantly improving LCP. Cross-reference: Part 19 (Performance) for font loading.

### Line-Length Optimization

Optimal line length for readability: 45-75 characters per line. 66 characters is ideal.

```css
/* Constrain content width with ch units */
.prose {
  max-width: 65ch;
  margin-inline: auto;
}

/* Responsive: shorter lines on mobile */
@media (max-width: 768px) {
  .prose {
    max-width: 55ch;
  }
}

/* Wide layout with constrained text */
.section {
  width: 100%;
  padding: var(--space-8) var(--space-4);
}

.section .content {
  max-width: 65ch;
  margin-inline: auto;
}
```

### OpenType Features

Unlock typographic refinement built into quality fonts.

```css
/* Tabular numbers for aligned data columns */
.data-value {
  font-variant-numeric: tabular-nums;
}

/* Oldstyle numbers for body text (more readable inline) */
.prose {
  font-variant-numeric: oldstyle-nums;
}

/* Fractions */
.recipe-amount {
  font-variant-numeric: diagonal-fractions;
}

/* Small caps for labels and abbreviations */
.abbreviation {
  font-variant-caps: all-small-caps;
  letter-spacing: 0.05em;
}

/* Ligatures for refined body text */
.prose {
  font-variant-ligatures: common-ligatures contextual;
}
```

Cross-reference: Part 23 (Data Viz) for tabular numbers in tables.

### Text Rendering & Wrapping

```css
/* Optimize legibility for headings (enables kerning + ligatures) */
h1, h2, h3 {
  text-rendering: optimizeLegibility;
}

/* Balanced headings: prevent orphans */
h1, h2, h3 {
  text-wrap: balance;
}

/* Pretty body text: avoid single-word last lines */
p {
  text-wrap: pretty;
}

/* Font smoothing: use judiciously, test on both light and dark */
body {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

---

## Part 25: Responsive Image Strategies

Images are typically the largest assets on a page and the most common LCP element. Get them right for both aesthetics and performance.

### Format Hierarchy

```
AVIF (best compression) → WebP (wide support) → JPEG (fallback)
SVG for icons, logos, illustrations
PNG only for transparency where AVIF/WebP unavailable
```

```html
<!-- Format fallback chain -->
<picture>
  <source srcset="/hero.avif" type="image/avif">
  <source srcset="/hero.webp" type="image/webp">
  <img src="/hero.jpg" alt="Hero image" width="1200" height="600">
</picture>
```

### Art Direction with picture

Serve different crops for different viewports. Not just different sizes -- different compositions.

```html
<!-- Portrait crop on mobile, landscape on desktop -->
<picture>
  <source
    srcset="/hero-portrait.avif"
    media="(max-width: 768px)"
    type="image/avif"
    width="600" height="800">
  <source
    srcset="/hero-landscape.avif"
    media="(min-width: 769px)"
    type="image/avif"
    width="1200" height="600">
  <img src="/hero-landscape.jpg" alt="Product hero" width="1200" height="600">
</picture>
```

Use `<picture>` when the image composition changes per viewport (art direction). Use `srcset` when the same image is just served at different resolutions.

### srcset and sizes

```html
<!-- Resolution switching: same image, different sizes -->
<img
  srcset="
    /product-400.avif 400w,
    /product-800.avif 800w,
    /product-1200.avif 1200w,
    /product-1600.avif 1600w"
  sizes="
    (max-width: 768px) 100vw,
    (max-width: 1200px) 50vw,
    33vw"
  src="/product-800.jpg"
  alt="Product photo"
  width="800"
  height="600"
  loading="lazy">
```

**Key Rule**: Always include `sizes`. Without it, the browser assumes the image is 100vw and downloads the largest version. The `sizes` attribute tells the browser how wide the image will actually be rendered.

### Lazy Loading

```html
<!-- LCP image: eager load, high priority -->
<img src="/hero.avif" alt="Hero" fetchpriority="high" decoding="async"
     width="1200" height="600">

<!-- Below-the-fold images: lazy load -->
<img src="/feature.avif" alt="Feature" loading="lazy" decoding="async"
     width="800" height="600">
```

**Key Rule**: Never lazy-load the LCP image. Use `fetchpriority="high"` on the LCP image and `loading="lazy"` on everything below the fold. Cross-reference: Part 19 (Performance) for LCP optimization.

### aspect-ratio CSS Property

Prevent CLS by reserving space before images load. Replaces the old padding-bottom hack.

```css
/* Fixed aspect ratio container */
.image-container {
  aspect-ratio: 16 / 9;
  width: 100%;
  overflow: hidden;
}

.image-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Responsive video embed */
.video-embed {
  aspect-ratio: 16 / 9;
  width: 100%;
}

.video-embed iframe {
  width: 100%;
  height: 100%;
  border: 0;
}
```

### object-fit / object-position

Create uniform image grids despite varied source dimensions.

```css
/* Uniform card images */
.card-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
  object-position: center top; /* Focus on faces/content */
}

/* Avatar: always square, always centered */
.avatar {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  object-fit: cover;
  object-position: center;
}

/* Contain for logos (show full logo, no cropping) */
.partner-logo {
  width: 120px;
  height: 60px;
  object-fit: contain;
}
```

---

## Part 26: Component Architecture Patterns

Structure components for reuse, composition, and maintainability. Design systems need architectural patterns, not just visual tokens.

### Headless UI Pattern

Separate behavior from presentation. Build logic once, style infinitely.

```jsx
/* Headless hook: manages dropdown behavior */
function useDropdown() {
  const [isOpen, setIsOpen] = useState(false);
  const triggerRef = useRef(null);
  const menuRef = useRef(null);

  /* Keyboard navigation, focus management, outside click */
  useEffect(() => {
    if (!isOpen) return;
    const handleEscape = (e) => { if (e.key === 'Escape') setIsOpen(false); };
    document.addEventListener('keydown', handleEscape);
    return () => document.removeEventListener('keydown', handleEscape);
  }, [isOpen]);

  return {
    isOpen,
    toggle: () => setIsOpen(!isOpen),
    close: () => setIsOpen(false),
    triggerProps: { ref: triggerRef, onClick: () => setIsOpen(!isOpen), 'aria-expanded': isOpen },
    menuProps: { ref: menuRef, role: 'menu', hidden: !isOpen },
  };
}

/* Styled implementation: your design system's look */
function StyledDropdown({ items }) {
  const { isOpen, triggerProps, menuProps, close } = useDropdown();
  return (
    <div className="dropdown">
      <button className="dropdown-trigger" {...triggerProps}>Options</button>
      <ul className="dropdown-menu" {...menuProps}>
        {items.map(item => (
          <li key={item.id} role="menuitem">
            <button onClick={() => { item.action(); close(); }}>{item.label}</button>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

**Key Rule**: Build behavior once, style infinitely. Headless components handle accessibility (keyboard nav, focus management, ARIA) so every styled implementation gets it for free.

### Compound Components

Components that work together with shared implicit state.

```jsx
/* Tab component API: compound structure */
<Tabs defaultTab="overview">
  <TabList>
    <Tab id="overview">Overview</Tab>
    <Tab id="features">Features</Tab>
    <Tab id="pricing">Pricing</Tab>
  </TabList>
  <TabPanel id="overview">...</TabPanel>
  <TabPanel id="features">...</TabPanel>
  <TabPanel id="pricing">...</TabPanel>
</Tabs>
```

Use compound components when: multiple sub-elements share state, the structure is stable, and customization is at the content level (not the structural level).

### CSS Cascade Layers for Components

```css
/* Component library in its own layer */
@layer components {
  .button {
    padding: var(--space-2) var(--space-4);
    border-radius: var(--radius-md);
    font-weight: 500;
  }

  .card {
    padding: var(--space-4);
    background: var(--surface-1);
    border-radius: var(--radius-lg);
  }
}

/* Consumer overrides always win without specificity battles */
@layer overrides {
  .button.custom-cta {
    border-radius: 0;
    text-transform: uppercase;
  }
}
```

Cross-reference: Part 31 (CSS Cascade Layers) for full layer architecture.

### Design Token Inheritance

Components inherit tokens from their context through CSS custom property scoping.

```css
/* Base component tokens */
.card {
  --card-padding: var(--space-4);
  --card-bg: var(--surface-1);
  padding: var(--card-padding);
  background: var(--card-bg);
}

/* Context-scoped overrides */
.hero .card {
  --card-padding: var(--space-6);
  --card-bg: var(--surface-2);
}

.sidebar .card {
  --card-padding: var(--space-3);
}

/* Component respects context without knowing about it */
```

Cross-reference: Part 30 (Design Token Architecture) for the full three-tier system.

### Component API Principles

| Principle | Good API | Bad API |
|-----------|----------|---------|
| Composition over configuration | `<Card><CardHeader/><CardBody/></Card>` | `<Card title="..." body="..." headerIcon="...">`|
| Sensible defaults | `<Button>Label</Button>` renders primary | Every prop required |
| Consistent naming | `variant`, `size` across all components | `type`, `kind`, `style`, `mode` mixed |
| Accessibility built-in | ARIA roles auto-applied | Requires manual aria props |
| Style escape hatches | `className` or `style` prop available | No way to customize |

---

## Part 27: Advanced Form Design

Forms are where design meets user patience. Every friction point costs conversions.

### Error State Best Practices

```css
/* Inline error: validate on blur, not on every keystroke */
.form-group.has-error .input {
  border-color: var(--color-error);
  box-shadow: 0 0 0 3px rgba(var(--color-error-rgb), 0.15);
}

.form-group .error-message {
  display: none;
  font-size: var(--text-sm);
  color: var(--color-error);
  margin-top: var(--space-1);
}

.form-group.has-error .error-message {
  display: flex;
  align-items: center;
  gap: 4px;
}

/* Use :user-invalid for CSS-only validation styling */
/* Only shows error AFTER user has interacted with the field */
input:user-invalid {
  border-color: var(--color-error);
}

input:user-invalid + .error-message {
  display: block;
}

input:user-valid {
  border-color: var(--color-success);
}
```

```html
<!-- Error associated with input via aria-describedby -->
<div class="form-group">
  <label for="email">Email</label>
  <input id="email" type="email" required
         aria-describedby="email-error" aria-invalid="true">
  <p id="email-error" class="error-message" role="alert">
    <svg aria-hidden="true"><!-- error icon --></svg>
    Please enter a valid email (e.g., name@company.com)
  </p>
</div>
```

**Key Rule**: Error messages must be specific ("Password must include a number") not generic ("Invalid password"). Show errors on blur, not on every keystroke. Never show errors before the user has interacted with a field.

### Progressive Enhancement

Start with native HTML validation. Layer JavaScript on top for better UX.

```html
<!-- HTML-first: works without JavaScript -->
<form method="POST" action="/submit">
  <input type="email" required autocomplete="email"
         pattern="[^@]+@[^@]+\.[^@]+" minlength="5">
  <input type="password" required minlength="8"
         autocomplete="new-password">
  <button type="submit">Sign up</button>
</form>
```

```javascript
/* JavaScript enhances the form, doesn't replace native validation */
const form = document.querySelector('form');

/* Only add novalidate when JS is available */
form.setAttribute('novalidate', '');

form.addEventListener('submit', (e) => {
  /* Custom validation UX with better error messages */
  if (!form.checkValidity()) {
    e.preventDefault();
    showCustomErrors(form);
  }
});
```

### Form Accessibility Deep-Dive

```html
<!-- Group related inputs with fieldset and legend -->
<fieldset>
  <legend>Shipping address</legend>

  <div class="form-group">
    <label for="street">Street address</label>
    <input id="street" type="text" autocomplete="street-address" required>
  </div>

  <div class="form-row">
    <div class="form-group">
      <label for="city">City</label>
      <input id="city" type="text" autocomplete="address-level2" required>
    </div>
    <div class="form-group">
      <label for="zip">ZIP code</label>
      <input id="zip" type="text" autocomplete="postal-code"
             inputmode="numeric" pattern="[0-9]*" required>
    </div>
  </div>
</fieldset>

<!-- Required field indicator -->
<label for="name">
  Full name <span class="required" aria-label="required">*</span>
</label>
```

Key attributes:
- `autocomplete`: helps browsers and password managers fill fields correctly
- `inputmode="numeric"`: shows number keyboard on mobile for non-number inputs (ZIP, credit card)
- `aria-describedby`: links error messages and help text to inputs
- `aria-invalid`: announces error state to screen readers

### Multi-Step Form Patterns

```css
/* Step indicator */
.step-indicator {
  display: flex;
  gap: var(--space-2);
  margin-bottom: var(--space-6);
}

.step {
  display: flex;
  align-items: center;
  gap: var(--space-2);
  font-size: var(--text-sm);
  color: var(--text-secondary);
}

.step.active {
  color: var(--color-interactive);
  font-weight: 600;
}

.step.completed {
  color: var(--color-success);
}

.step .number {
  width: 28px;
  height: 28px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 2px solid currentColor;
  font-size: var(--text-xs);
  font-weight: 700;
}

.step.completed .number::after {
  content: '✓';
}

.step-connector {
  flex: 1;
  height: 2px;
  background: var(--border);
}

.step-connector.completed {
  background: var(--color-success);
}
```

Form principles:
- Validate each step before allowing advancement
- Preserve data on back navigation (never lose user input)
- Show a summary/review step before final submission
- Single-column forms convert better than multi-column
- Labels above inputs (not beside) for mobile and faster scanning

Cross-reference: Part 3 (Form Element Consistency) for styling rules.

---

## Part 28: Internationalization & RTL Design

If your interface will ever be translated, build for it from day one. Retrofitting RTL and text expansion is painful.

### Logical CSS Properties

Replace physical properties (left/right/top/bottom) with logical ones. They automatically adapt to writing direction.

```css
/* WRONG - Only works for LTR */
.sidebar {
  margin-left: 16px;
  padding-right: 24px;
  border-left: 2px solid var(--border);
  text-align: left;
}

/* CORRECT - Works for both LTR and RTL */
.sidebar {
  margin-inline-start: 16px;
  padding-inline-end: 24px;
  border-inline-start: 2px solid var(--border);
  text-align: start;
}
```

| Physical Property | Logical Property |
|-------------------|------------------|
| `margin-left` | `margin-inline-start` |
| `margin-right` | `margin-inline-end` |
| `margin-top` | `margin-block-start` |
| `margin-bottom` | `margin-block-end` |
| `padding-left` | `padding-inline-start` |
| `padding-right` | `padding-inline-end` |
| `border-left` | `border-inline-start` |
| `text-align: left` | `text-align: start` |
| `float: left` | `float: inline-start` |
| `width` | `inline-size` |
| `height` | `block-size` |

**Key Rule**: Every new CSS you write should use logical properties. There is no downside -- they work identically to physical properties in LTR and automatically adapt for RTL.

### RTL Design Considerations

```css
/* Set direction on root */
html[dir="rtl"] {
  direction: rtl;
}

/* Icons that need mirroring (directional meaning) */
html[dir="rtl"] .icon-arrow-forward,
html[dir="rtl"] .icon-chevron-right,
html[dir="rtl"] .icon-reply {
  transform: scaleX(-1);
}

/* Icons that DON'T mirror (universal meaning) */
/* checkmarks, close/X, search, download, play, pause */

/* Bidirectional text isolation */
.mixed-direction-text {
  unicode-bidi: isolate;
}
```

### Text Expansion & Contraction

Design for variable text lengths. Never hardcode widths on text containers.

| Language | Typical Change from English |
|----------|----------------------------|
| German | +30% longer |
| French | +20% longer |
| Finnish | +30-40% longer |
| Chinese | -50% shorter |
| Japanese | -40% shorter |
| Korean | -30% shorter |
| Arabic | +25% longer |

```css
/* Flexible button: accommodates translation expansion */
.button {
  padding-inline: var(--space-4);
  white-space: nowrap;
  min-inline-size: 0; /* Don't force minimum width */
  /* Let text determine width */
}

/* Truncation safety for constrained areas */
.nav-label {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  max-inline-size: 160px;
}
```

### Cultural Color Considerations

| Color | Western | East Asian | Middle Eastern |
|-------|---------|-----------|----------------|
| Red | Danger, stop | Prosperity, luck | Danger |
| White | Purity, clean | Mourning, death | Purity |
| Green | Go, success, nature | Youth, fertility | Islam (sacred), paradise |
| Yellow | Caution, warmth | Royalty, sacred | Happiness, prosperity |
| Black | Mourning, elegance | Power, formality | Mourning, mystery |
| Purple | Royalty, luxury | Nobility | Wealth |

**Key Rule**: Test color semantics with your target audience. Never assume universal meaning. Semantic color tokens like `--color-error` are safer than `--color-red` because their meaning transcends cultural interpretation.

### Number & Date Formatting

```javascript
/* Always use Intl APIs for locale-aware formatting */

/* Numbers */
new Intl.NumberFormat('de-DE').format(1234567.89);
// → "1.234.567,89"

new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' })
  .format(1234.50);
// → "$1,234.50"

/* Dates */
new Intl.DateTimeFormat('ja-JP', { dateStyle: 'long' })
  .format(new Date());
// → "2025年1月30日"
```

---

## Part 29: Cognitive Accessibility

Accessibility isn't just about screen readers. Design for how brains work -- including brains that work differently.

### Designing for ADHD

```css
/* Focus mode: reduce visual noise on demand */
[data-focus-mode="true"] .sidebar,
[data-focus-mode="true"] .notifications,
[data-focus-mode="true"] .decorative {
  display: none;
}

[data-focus-mode="true"] .main-content {
  max-width: 65ch;
  margin-inline: auto;
}

[data-focus-mode="true"] .nav {
  /* Simplified navigation */
  opacity: 0.4;
  transition: opacity 0.2s;
}

[data-focus-mode="true"] .nav:hover,
[data-focus-mode="true"] .nav:focus-within {
  opacity: 1;
}
```

Key principles for ADHD:
- Reduce visual noise: clear hierarchy, minimal competing elements
- Chunk information: short paragraphs, bullet points, clear headings
- Provide focus mode: ability to hide sidebar, notifications, decorative elements
- Undo support: forgiveness for impulsive actions
- Clear progress indicators: show where the user is and what's left

### Designing for Autism Spectrum

```css
/* Sensory-reduced mode */
[data-sensory-reduced="true"] {
  --transition-speed: 0s;
  --animation-speed: 0s;
}

[data-sensory-reduced="true"] * {
  animation-duration: 0s !important;
  transition-duration: 0s !important;
}

[data-sensory-reduced="true"] .decorative-bg,
[data-sensory-reduced="true"] .particle-effect,
[data-sensory-reduced="true"] .video-background {
  display: none;
}
```

Key principles:
- Predictable layouts: consistent navigation placement, no surprise modals
- Clear, literal language: no idioms in button labels ("Get started" not "Jump in")
- Warn before changes: transitions, redirects, automatic content updates
- Consistent patterns: same action should always look and work the same way

### Designing for Dyslexia

```css
/* Dyslexia-friendly typography */
.content {
  font-family: 'Open Sans', 'Verdana', sans-serif; /* Avoid serif and italic */
  font-size: 1rem;    /* Minimum 16px */
  line-height: 1.6;   /* 1.5x minimum */
  letter-spacing: 0.02em;
  word-spacing: 0.05em;
  text-align: left;   /* NEVER justify - irregular spacing is harder to read */
}

/* Avoid pure white backgrounds (glare) */
.content {
  background: #fafafa; /* Slight off-white reduces contrast fatigue */
  color: #2d2d2d;      /* Dark gray, not pure black */
}

/* Adequate paragraph spacing */
.content p + p {
  margin-top: 1.2em;
}

/* Short line lengths improve tracking */
.content {
  max-width: 60ch;
}
```

**Key Rule**: These patterns benefit ALL readers, not just those with dyslexia. Good reading ergonomics are universal.

### Vestibular Disorder Considerations

```css
/* Comprehensive reduced motion -- go further than the basics */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }

  /* Remove parallax, zoom, and rotation effects */
  .parallax { transform: none !important; }
  .zoom-on-hover:hover { transform: none !important; }

  /* Disable video backgrounds */
  .video-background video { display: none; }
  .video-background { background-image: url('/static-fallback.jpg'); }

  /* Remove scroll-driven animations */
  * { animation-timeline: none !important; }
}
```

Some users need ZERO motion, not just reduced motion. Provide an explicit "disable all animations" toggle beyond what `prefers-reduced-motion` offers.

Cross-reference: Part 8 (Motion), Part 11 (Accessibility Checklist).

### Aging-Friendly Patterns

- Touch targets: 48px minimum (larger than the standard 44px)
- Contrast: target 7:1 for body text (higher than WCAG AA 4.5:1)
- Default text: 18px minimum body size
- Navigation: fewer levels, clearer labels, no hover-only reveals
- Error recovery: generous timeouts, clear confirmation dialogs, large undo buttons

### Cognitive Load Reduction

| Principle | Implementation |
|-----------|----------------|
| One primary action per screen | Single prominent CTA, secondary actions visually subdued |
| Progressive disclosure | Hide advanced options behind "More" or `<details>` |
| Consistent patterns | Same action looks and works the same everywhere |
| Meaningful defaults | Pre-select the most common option |
| Chunked information | Break long forms into steps, long text into sections |
| Clear wayfinding | Breadcrumbs, progress bars, "you are here" indicators |

Cross-reference: Part 9 (UX Principles) for Hick's Law and Miller's Law.

---

## Part 30: Design Token Architecture

Tokens are the single source of truth for your design system. Get the architecture right and theming, maintenance, and consistency follow naturally.

### Three-Tier Token Structure

```css
/* TIER 1: Constant/Primitive tokens - raw values, never used directly in components */
:root {
  --primitive-blue-50: #eff6ff;
  --primitive-blue-500: #3b82f6;
  --primitive-blue-700: #1d4ed8;
  --primitive-gray-50: #f9fafb;
  --primitive-gray-900: #111827;
  --primitive-radius-sm: 4px;
  --primitive-radius-md: 8px;
  --primitive-space-1: 4px;
  --primitive-space-2: 8px;
  --primitive-space-4: 16px;
  --primitive-space-6: 24px;
}

/* TIER 2: Semantic tokens - purpose-based, reference primitives */
:root {
  --color-interactive: var(--primitive-blue-500);
  --color-interactive-hover: var(--primitive-blue-700);
  --color-surface: var(--primitive-gray-50);
  --color-text-primary: var(--primitive-gray-900);
  --radius-component: var(--primitive-radius-md);
  --spacing-component-padding: var(--primitive-space-4);
}

/* TIER 3: Component tokens - scoped to specific components */
.button {
  --button-bg: var(--color-interactive);
  --button-bg-hover: var(--color-interactive-hover);
  --button-padding: var(--spacing-component-padding);
  --button-radius: var(--radius-component);

  background: var(--button-bg);
  padding: var(--button-padding);
  border-radius: var(--button-radius);
}

.button:hover {
  background: var(--button-bg-hover);
}
```

**Flow**: Primitive → Semantic → Component. Components only reference component tokens. Semantic tokens only reference primitives. This creates clean separation of concerns.

### Naming Conventions

Pattern: `category-subcategory-variant-state`

| Category | Examples |
|----------|---------|
| `color-` | `color-text-primary`, `color-surface-elevated`, `color-border-subtle` |
| `spacing-` | `spacing-component-gap`, `spacing-section-padding` |
| `typography-` | `typography-heading-size`, `typography-body-weight` |
| `elevation-` | `elevation-card`, `elevation-modal` |
| `radius-` | `radius-button`, `radius-input`, `radius-card` |
| `motion-` | `motion-duration-fast`, `motion-easing-default` |

**Key Rule**: Names describe purpose, never appearance. Use `--color-interactive`, not `--color-blue`. Use `--color-error`, not `--color-red`. When the brand color changes from blue to green, only primitive tokens change.

### Multi-Theme Token Mapping

```css
/* Theme mapping through semantic tokens */
[data-theme="light"] {
  --color-surface: #ffffff;
  --color-surface-elevated: #f5f5f5;
  --color-text-primary: #1a1a1a;
  --color-text-secondary: #666666;
  --color-border: #e0e0e0;
  --color-interactive: hsl(220, 90%, 50%);
}

[data-theme="dark"] {
  --color-surface: #121212;
  --color-surface-elevated: #1e1e1e;
  --color-text-primary: #e5e5e5;
  --color-text-secondary: #a0a0a0;
  --color-border: rgba(255, 255, 255, 0.12);
  --color-interactive: hsl(220, 70%, 65%);
}

[data-theme="high-contrast"] {
  --color-surface: #000000;
  --color-surface-elevated: #1a1a1a;
  --color-text-primary: #ffffff;
  --color-text-secondary: #e0e0e0;
  --color-border: #ffffff;
  --color-interactive: hsl(220, 100%, 70%);
}
```

Components don't change at all between themes -- only the semantic token values change. Cross-reference: Part 20 (Dark Mode) for implementation patterns.

### Token Maintenance

- **Audit regularly**: search for hardcoded values (`#`, `rgb(`, `hsl(`, `px` outside tokens)
- **Deprecation strategy**: rename → alias old to new → remove old after migration
- **Avoid token explosion**: don't create `--button-primary-hover-border-color` if `--color-interactive-hover` works
- **Document usage**: each token should have a description of where and when to use it
- **W3C Design Tokens format**: use JSON tokens as source of truth if integrating with design tools

```json
{
  "color": {
    "interactive": {
      "$value": "{primitive.blue.500}",
      "$type": "color",
      "$description": "Primary interactive elements: buttons, links, toggles"
    }
  }
}
```

### Quick Reference

| Tier | Changes When | Example |
|------|-------------|---------|
| Primitive | Brand refresh, new palette | `--primitive-blue-500: #3b82f6` |
| Semantic | Feature redesign, new patterns | `--color-interactive: var(--primitive-blue-500)` |
| Component | Component-specific tweaks | `--button-bg: var(--color-interactive)` |

---

## Part 31: CSS Cascade Layers

Cascade layers solve specificity wars in design systems. They give you explicit control over which styles win, regardless of selector complexity.

### Why Layers Matter

```css
/* WITHOUT layers: specificity battles */
.component .button { background: blue; }        /* specificity: 0-2-0 */
.sidebar .component .button { background: red; } /* specificity: 0-3-0, wins */
.button.primary { background: green; }           /* specificity: 0-2-0, loses to red */

/* WITH layers: explicit priority */
@layer components, overrides;

@layer components {
  .component .button { background: blue; }
}

@layer overrides {
  .button.primary { background: green; } /* Wins because overrides layer > components layer */
}
```

**Key Rule**: Layers give you explicit control over which styles win. A simple selector in a higher-priority layer beats a complex selector in a lower-priority layer.

### Layer Ordering for Design Systems

```css
/* Declare order: first = lowest priority, last = highest */
@layer reset, base, tokens, layouts, components, utilities, overrides;

@layer reset {
  /* Normalize or CSS reset */
  *, *::before, *::after { box-sizing: border-box; margin: 0; }
}

@layer base {
  /* Default element styles */
  body { font-family: var(--font-body); color: var(--color-text-primary); }
  a { color: var(--color-interactive); }
}

@layer tokens {
  /* Design token definitions */
  :root { --color-primary: #3b82f6; /* ... */ }
}

@layer layouts {
  /* Page structure */
  .container { max-width: 1200px; margin-inline: auto; }
  .grid { display: grid; }
}

@layer components {
  /* Component library */
  .button { /* ... */ }
  .card { /* ... */ }
}

@layer utilities {
  /* Utility classes (always beat components) */
  .sr-only { position: absolute; width: 1px; height: 1px; overflow: hidden; }
  .hidden { display: none; }
}

@layer overrides {
  /* Project-specific overrides */
}
```

### Importing Third-Party CSS into Layers

```css
/* Wrap third-party CSS in a low-priority layer */
@import url('normalize.css') layer(reset);
@import url('component-library.css') layer(components);

/* Your styles in higher-priority layers always win */
@layer overrides {
  .their-button { /* Your customization */ }
}
```

### Nested Layers

```css
/* Organize complex component libraries */
@layer components {
  @layer buttons {
    .button { /* base button */ }
    .button--primary { /* primary variant */ }
  }

  @layer forms {
    .input { /* base input */ }
    .select { /* base select */ }
  }

  @layer cards {
    .card { /* base card */ }
  }
}

/* Reference nested layers */
@layer components.buttons {
  .button--custom { /* additional button style */ }
}
```

### Migration Strategy

Adopt layers incrementally in existing projects:

1. Wrap your existing CSS in a single layer: `@layer legacy { /* all existing CSS */ }`
2. New CSS goes in properly named layers
3. Gradually move code from `legacy` into structured layers
4. Unlayered CSS always beats layered CSS -- use this sparingly for critical overrides

Cross-reference: Part 26 (Component Architecture) for component-scoped layer patterns.

---

## Extended Pre-Implementation Checklist

Before finalizing any frontend design, verify:

### Aesthetics
- [ ] Committed to a bold, distinctive aesthetic direction
- [ ] Avoided AI slop patterns (cream backgrounds, terracotta accents, purple gradients)
- [ ] Used distinctive typography (not Inter, Roboto, Arial)
- [ ] Created cohesive color palette with CSS variables
- [ ] Researched inspiration from curated galleries (Godly, Minimal Gallery, Brutalist)

### Design System
- [ ] Established design tokens (colors, spacing, typography)
- [ ] Created consistent elevation/shadow system
- [ ] Defined typography scale with clear hierarchy
- [ ] Supported density variants if needed for data-heavy UI

### UX Heuristics
- [ ] System status visible (loading states, progress, confirmations)
- [ ] Language matches user expectations (no jargon)
- [ ] Undo/cancel options available for user control
- [ ] Consistent patterns throughout interface
- [ ] Error prevention through constraints and confirmations
- [ ] Recognition over recall (visible options, contextual help)
- [ ] Shortcuts available for power users
- [ ] Minimal design (no competing irrelevant information)

### Humane Design
- [ ] No infinite scroll without endpoints
- [ ] No autoplay media
- [ ] Clear exit/unsubscribe options
- [ ] No dark patterns or confirmation shaming
- [ ] User data practices transparent
- [ ] Respects user attention (appropriate notifications)

### Mobile Responsiveness
- [ ] Hero section centers on mobile (not left-aligned with empty space)
- [ ] Grid layouts collapse to single column on mobile
- [ ] Large selection lists use accordion on mobile (not horizontal scroll)
- [ ] Status/alert cards center properly on mobile
- [ ] Font sizes scale appropriately for mobile

### Form Elements
- [ ] All form fields (input, select, textarea) styled consistently
- [ ] Radio buttons and checkboxes visible (especially for transparent-border styles)
- [ ] Dropdown options have readable backgrounds
- [ ] Textarea has appropriate border-radius (not pill-shaped)
- [ ] All inputs have associated labels
- [ ] Error messages associated with inputs

### Color & Contrast
- [ ] Labels use semantic color variables (not hardcoded)
- [ ] Badge/pill text contrasts with background
- [ ] Color swatches have visible borders
- [ ] Dark theme elements properly contrasted
- [ ] Normal text: 4.5:1 contrast ratio minimum
- [ ] Large text/icons: 3:1 contrast ratio minimum
- [ ] Information not conveyed by color alone

### Accessibility
- [ ] Valid semantic HTML structure
- [ ] Proper heading hierarchy (one h1, logical sequence)
- [ ] Keyboard navigation works (visible focus, logical order)
- [ ] Skip link to main content provided
- [ ] All images have appropriate alt text
- [ ] Media has captions/transcripts
- [ ] Touch targets 44x44px minimum

### Spacing & Grid
- [ ] Using consistent spacing scale (8pt grid recommended)
- [ ] All spacing uses design tokens (not arbitrary values)
- [ ] Typography follows a mathematical scale ratio
- [ ] Elements align to pixel grid for crisp rendering

### Dieter Rams Principles
- [ ] Every element serves the user's goals (useful)
- [ ] Interface explains itself (understandable)
- [ ] Design doesn't demand unnecessary attention (unobtrusive)
- [ ] No deceptive elements or dark patterns (honest)
- [ ] Attention to every detail (thorough)
- [ ] Only essential elements included (as little design as possible)

### Motion
- [ ] Animations serve purpose (not just decoration)
- [ ] High-impact moments prioritized (page load, key interactions)
- [ ] Only transform/opacity animated for performance
- [ ] `prefers-reduced-motion` media query implemented
- [ ] No content that flashes more than 3 times per second

### Modern CSS (Part 18)
- [ ] Used container queries for component-level responsiveness where appropriate
- [ ] Leveraged `:has()` for parent-aware styling (reducing JavaScript)
- [ ] Considered CSS nesting (max 3 levels depth)
- [ ] Used Popover API for light-dismiss behaviors instead of custom JS

### Performance (Part 19)
- [ ] LCP element identified and optimized (`fetchpriority="high"`, preload)
- [ ] All images have explicit `width`/`height` or `aspect-ratio` (CLS prevention)
- [ ] Font loading uses `font-display: swap` with `size-adjust` fallback
- [ ] Skeleton loaders match exact dimensions of replaced content
- [ ] Only `transform`/`opacity` animated (no layout-triggering properties)
- [ ] Resource hints applied (preload, preconnect, prefetch)

### Dark Mode & Theming (Part 20)
- [ ] System preference detected via `prefers-color-scheme`
- [ ] User override available with three-state toggle (System/Light/Dark)
- [ ] Colors desaturated ~20% for dark mode
- [ ] No pure black backgrounds (use `#121212` or similar)
- [ ] Elevation through surface lightness, not shadows in dark mode
- [ ] `forced-colors` media query handled for Windows High Contrast

### AI Interfaces (Part 21)
- [ ] Streaming content has visible typing indicator and auto-scroll
- [ ] AI loading states communicate progress phases (not just spinners)
- [ ] Confidence levels visible when AI certainty varies
- [ ] User can cancel, undo, regenerate, and edit AI output
- [ ] Error states offer manual fallback when AI is unavailable

### Interaction Design (Part 22)
- [ ] Every state has a designed view (empty, loading, error, partial, complete)
- [ ] Gestures have non-gesture alternatives for accessibility
- [ ] Progressive disclosure used for complex features
- [ ] State transitions animated smoothly

### Data Visualization (Part 23)
- [ ] Charts have text alternatives for screen readers
- [ ] Color is not the only way to distinguish data series
- [ ] Tables have sticky headers and clear sort indicators
- [ ] Real-time data batched to prevent visual noise

### Typography (Part 24)
- [ ] Font sizes use `clamp()` for fluid scaling
- [ ] Line length constrained to 45-75 characters
- [ ] `text-wrap: balance` applied to headings
- [ ] Tabular numbers used for data columns

### Images (Part 25)
- [ ] Images served in AVIF/WebP with JPEG fallback
- [ ] LCP image uses `fetchpriority="high"` and is not lazy-loaded
- [ ] All images have `aspect-ratio` or explicit dimensions
- [ ] `sizes` attribute included on responsive images

### Component Architecture (Part 26)
- [ ] Components use design token inheritance
- [ ] Accessibility baked into components (not opt-in)
- [ ] CSS organized with cascade layers

### Forms (Part 27)
- [ ] Error messages are specific and appear inline with the field
- [ ] Validation triggers on blur, not on every keystroke
- [ ] Multi-step forms preserve data on back navigation
- [ ] All inputs use appropriate `autocomplete` attributes

### Internationalization (Part 28)
- [ ] CSS uses logical properties (`margin-inline`, `padding-block`)
- [ ] Layout accommodates 30% text expansion for translation
- [ ] Color semantics tested with target audience

### Cognitive Accessibility (Part 29)
- [ ] Body text at 1.5x line-height minimum, left-aligned
- [ ] One primary action per screen
- [ ] Reduced-motion mode is comprehensive (zero motion option)
- [ ] Focus mode available to reduce visual noise

### Design Tokens (Part 30)
- [ ] Tokens follow three-tier structure (constant → semantic → contextual)
- [ ] Token names describe purpose, not appearance
- [ ] Theme switching uses semantic tokens only (no hardcoded values)

### Cascade Layers (Part 31)
- [ ] CSS organized with `@layer` declarations
- [ ] Third-party CSS wrapped in low-priority layers
- [ ] Component styles don't rely on specificity to override
