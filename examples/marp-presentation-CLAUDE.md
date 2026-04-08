# CLAUDE.md - Marp Presentation Project Example

This is an example CLAUDE.md file for a project using the Marp agent to create professional presentations.

## Project Purpose

This project contains presentation slides created with Marp (Markdown Presentation Ecosystem). Slides are written in markdown and exported to HTML for distribution.

## Repository Structure

```
my-presentation/
├── slides.md              # Main presentation file
├── assets/                # Images and diagrams
│   ├── logo.png
│   ├── architecture-diagram.png
│   ├── metrics-chart.png
│   └── team-photo.jpg
├── output/                # Generated HTML presentations
│   └── presentation.html
├── README.md              # Build instructions
└── CLAUDE.md              # This file (instructions for Claude)
```

## Before You Start

Before asking Claude to create slides, ensure your project is ready:

- [ ] Directory structure exists (`slides.md`, `assets/`, `output/`)
- [ ] If you want images: collect and place them in `assets/` directory with descriptive names
- [ ] Decide your audience type: **Technical** (developers/engineers) or **Non-Technical** (executives/stakeholders)
- [ ] Outline 3-5 key points you want to cover
- [ ] Have Marp CLI installed (`npm install -g @marp-team/marp-cli`) or ready to install

## Using the Marp Agent

When creating presentations, tell Claude:

**For Technical Audiences** (developers, engineers, architects):
```
Create a presentation about [TOPIC] for a technical audience.
Key points: [LIST YOUR KEY POINTS]
Duration: [PRESENTATION LENGTH/SLIDE COUNT]
Include images: [YES/NO]
```

Claude will use the technical template with:
- Code examples and syntax highlighting
- Architecture diagrams
- Technical terminology and implementation details
- Metrics and benchmarks

**For Non-Technical Audiences** (executives, stakeholders, customers):
```
Create a presentation about [TOPIC] for a business audience.
Key points: [LIST YOUR KEY POINTS]
Duration: [PRESENTATION LENGTH/SLIDE COUNT]
Include images: [YES/NO]
```

Claude will use the non-technical template with:
- Simple language, no jargon
- Business value and ROI focus
- Customer success stories
- Visual storytelling

## HTML Output

After creating slides, Claude will ask:
- **Render automatically**: Claude runs marp CLI to generate `output/presentation.html`
- **Manual render**: You run marp CLI yourself later

## Build Commands

### Install Marp CLI (one-time setup)
```bash
npm install -g @marp-team/marp-cli
```

### Generate HTML
```bash
# Standard HTML export
marp slides.md -o output/presentation.html

# HTML with specific theme
marp slides.md --theme gaia -o output/presentation.html

# Watch mode (auto-rebuild on changes)
marp -w slides.md -o output/presentation.html

# Allow local files (for custom fonts/assets)
marp slides.md --allow-local-files -o output/presentation.html
```

## Image Guidelines

**Workflow for Images:**
1. When you ask for slides with images, Claude will check if `assets/` directory has files
2. If `assets/` is empty and you requested images: Claude will STOP and ask you to add images first
3. If `assets/` has images: Claude references them by name in the slides

**Image Naming Convention:**
All images should be placed in `assets/` with descriptive names:
- **Logos**: `logo.png`, `company-logo.png`
- **Diagrams**: `architecture-diagram.png`, `system-flow.png`
- **Charts**: `metrics-chart.png`, `roi-graph.png`
- **Photos**: `team-photo.jpg`, `product-screenshot.png`

**Recommended dimensions:**
- Full-width images: 1920x1080 (16:9 ratio)
- Diagrams: 1600x900 minimum
- Logos: 512x512 or vector (SVG)

**Quick Rule:** Want images? Add files to `assets/` directory first, THEN ask Claude to create slides.

## Step-by-Step Workflow

**Step 1: Plan Your Content**
- Decide audience type (technical or non-technical)
- List 3-5 key points you want to cover
- Estimate presentation duration and target slide count

**Step 2: Prepare Assets** (if using images)
- Collect all images you want in the presentation
- Place them in `assets/` directory with descriptive names
- Verify files are there before moving to Step 3

**Step 3: Create Slides with Claude**
Tell Claude your topic, audience type, and key points (see examples below).

Claude will:
- Ask if you want images (if yes, checks `assets/` directory)
- Stop if you said "yes" to images but `assets/` is empty
- Continue and create `slides.md` if assets are ready
- Ask if you want HTML rendered automatically or manually
- Generate complete presentation file

**Step 4: Build HTML**
Choose one:
- **Let Claude do it**: If you chose automatic rendering, Claude runs marp and creates `output/presentation.html`
- **Do it yourself**: Run `marp slides.md -o output/presentation.html` in terminal

Review the HTML file in your browser and iterate as needed.

**Step 5: Present**
Open `output/presentation.html` in a browser for full interactivity and animations.

## Claude's Responsibilities

When Claude creates presentations for this project:

1. **Confirm audience type** - If not explicitly stated, ask (technical or non-technical)
2. **Check assets directory** - BEFORE generating slides, if user wants images:
   - Verify `assets/` directory exists
   - List files in it
   - If empty → STOP and ask user to add images first
   - If files present → reference them by name in slides
3. **Apply correct template** - Use technical template (code, diagrams, technical terms) or non-technical template (simple language, business value, ROI)
4. **Create focused slides** - One main idea per slide, minimal text, maximum visual impact
5. **Generate complete slides.md** - Include:
   - Marp frontmatter: `marp: true`, `theme: default` (or gaia/uncover), `paginate: true`
   - Title slide with topic
   - Agenda/outline slide
   - Content slides (5-15 depending on duration)
   - Closing/Q&A slide
6. **Offer HTML rendering** - Ask if Claude should run marp automatically or user will do it later
7. **Update README.md** - Include build commands if file exists, or create it with instructions

## Common Tasks

**Create a new presentation:**
```
Create a presentation about [TOPIC] for a [technical/non-technical] audience.
Key points:
- [Point 1]
- [Point 2]
- [Point 3]
Duration: [X minutes / approximately Y slides]
Include images: [YES/NO]
Auto-render HTML: [YES/NO]
```

**Example - Technical Presentation:**
```
Create a presentation about microservices architecture for a technical audience.
Key points:
- Service design principles
- API contract management
- Deployment and scaling strategies
Duration: 30 minutes (12-15 slides)
Include images: YES
Auto-render HTML: YES
```

**Example - Business Presentation:**
```
Create a presentation about Q4 product roadmap for executives.
Key points:
- Market opportunity
- Feature development plan
- Expected ROI
Duration: 20 minutes (10-12 slides)
Include images: NO
Auto-render HTML: YES
```

**Update existing slides:**
```
Update slides.md to add a new slide about [TOPIC] after the [SECTION NAME] section.
Content: [Brief description of what should be on the new slide]
```

**Review and improve slides:**
```
Review slides.md and suggest improvements for clarity and engagement for a [AUDIENCE TYPE] audience.
```

**Rebuild HTML output:**
```
Run marp to regenerate output/presentation.html from the current slides.md
```

## Important Notes

**Themes & Styling:**
- This project uses default Marp themes (`default`, `gaia`, `uncover`) for maximum compatibility
- Fonts are handled automatically by themes—no custom fonts needed
- All presentations export cleanly to HTML without special configuration

**Slide Content:**
- Keep content concise—aim for minimal text, maximum visual impact
- Use bullet points, not paragraphs
- One main idea per slide
- Include speaker notes if needed (markdown syntax: `<!-- Comment -->`)

**Images in Slides:**
- Reference images as: `![alt text](assets/image-name.png)`
- Always include descriptive alt text for accessibility
- Images render correctly in HTML output

**Marp Frontmatter Template:**
```markdown
---
marp: true
theme: default
paginate: true
---
```

**Common Issues & Solutions:**

| Issue | Solution |
|-------|----------|
| Images not showing in HTML | Verify `assets/` directory exists and is relative to `slides.md` |
| Theme doesn't apply | Ensure frontmatter has `theme: [name]` (default/gaia/uncover) |
| HTML won't open in browser | Use full path: `/absolute/path/to/output/presentation.html` or serve via local server |
| Marp CLI not found | Run `npm install -g @marp-team/marp-cli` to install globally |
| Markdown not rendering | Check for syntax errors or mismatched quotes in frontmatter |
