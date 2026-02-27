# Style Guide — benjaminaltieri.com

Reference for maintaining consistent tone, voice, and visual identity across the site.

## Writing Tone

- **First-person, direct** — "I build systems that..." not "Systems are built that..."
- **Professional but human** — conversational without being casual. No corporate jargon.
- **Narrative framing** — describe career and experience as a story arc (embedded roots, cloud expansion, AI/ML pivot), not a resume dump.
- **Personal touches welcome** — family, music, climate interests can be woven in where natural. The site represents a whole person, not just a skill set.
- **No em-dashes** — use commas, periods, or parentheses instead.
- **Concise** — short paragraphs, clear sentences. Let the content breathe.

## Brand & Visual Identity

### Terminal Aesthetic

The site's identity is rooted in a developer/systems-engineer terminal feel:

- **Logo**: `:: SYSTEM_LOG` — evokes a system prompt or log output
- **Typography split**: Monospaced fonts (JetBrains Mono) for headings and navigation establish the technical feel. Sans-serif (Inter) for body text keeps long-form content readable. Fira Code is reserved for actual code blocks.
- **Color**: Red/coral accent (`var(--accent)`) on a dark background. The accent is used for borders, titles, hover states, and skill pills — never for large background fills.
- **Interactions**: Hover effects use subtle horizontal translation (`translateX(4px)`) with accent box-shadows, giving a "cursor stepping into" feel rather than typical web hover patterns.

### CSS Patterns

All custom styling follows these patterns (see `static/custom.css`):

- **Use theme CSS variables** — `var(--accent)`, `var(--accent-alpha-20)`, `var(--accent-alpha-70)`, `var(--color)`. Never hardcode the accent color.
- **Accent borders, translucent fills** — boxes get `border: 2px solid var(--accent)` with backgrounds like `rgba(255, 98, 102, 0.05)` or `var(--accent-alpha-20)`.
- **Pill/badge pattern for skills/tags** — `display: inline-block`, small padding, `var(--accent-alpha-20)` background, `var(--accent-alpha-70)` border, monospaced font.
- **Responsive at 768px** — grid layouts collapse to single column, font sizes scale down slightly.

### The Full System Stack

The About page's signature visual element. Design principles:

- **Grid layout**: Sidebar (Platform & Automation) + 3 stacked main layers (Hardware, Edge, Cloud)
- **Each layer**: Accent border, header with title + italic context line, flex-wrapped skill pills
- **Represents career breadth** — update the skills within layers as your stack evolves, but preserve the layered architecture metaphor (hardware to cloud)
- **All in JetBrains Mono** — reinforces the terminal aesthetic within the visualization

## Content Structure Patterns

### Section pages (`_index.md`)
Use heading hierarchy: `# Welcome!` or `# Hi, I'm Ben` as the page opener, then `##` for major sections, with short prose paragraphs between them.

### Blog posts (when published)
Front matter should include `title`, `date`, `description`, and at least one taxonomy (`categories` or `tags`). Keep descriptions under ~120 characters for clean meta tag output.

### Embedded HTML
Raw HTML blocks within Markdown (like the System Stack) are acceptable for interactive or complex visual elements. Style them via `custom.css` classes, not inline styles.
