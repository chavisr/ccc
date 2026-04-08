# CLAUDE.md - Marp Presentation Project Example

This is an example CLAUDE.md file for a project using the Marp agent to create professional presentations.

## Project Purpose

This project contains presentation slides created with Marp (Markdown Presentation Ecosystem). Slides are written in markdown and exported to PDF for distribution.

## Repository Structure

```
my-presentation/
├── slides.md              # Main presentation file
├── assets/                # Images and diagrams
│   ├── logo.png
│   ├── architecture-diagram.png
│   ├── metrics-chart.png
│   └── team-photo.jpg
├── output/                # Generated PDFs
│   └── presentation.pdf
├── README.md              # Build instructions
└── CLAUDE.md              # This file (instructions for Claude)
```

## Using the Marp Agent

When working on presentations in this project, Claude should use the `marp-slides` agent from the ccc repository.

### For Technical Presentations
When creating slides for technical audiences (developers, engineers, architects):
```
Use the marp-slides.md agent with technical template
- Include code examples
- Show architecture diagrams
- Use technical terminology
- Focus on implementation details
```

### For Business Presentations
When creating slides for non-technical audiences (executives, stakeholders, customers):
```
Use the marp-slides.md agent with non-technical template
- Simple language, no jargon
- Focus on business value
- Include customer stories
- Emphasize ROI and outcomes
```

### PDF Rendering Option
The agent will ask whether to:
- **Render PDF automatically**: Agent runs marp CLI to generate output/presentation.pdf
- **User renders manually**: User runs marp command themselves after slides are created

## Build Commands

### Install Marp CLI (one-time setup)
```bash
npm install -g @marp-team/marp-cli
```

### Generate PDF
```bash
# Standard PDF export
marp slides.md -o output/presentation.pdf

# High-quality PDF (for printing)
marp slides.md --pdf-outline --pdf-notes -o output/presentation.pdf

# Watch mode (auto-rebuild on changes)
marp -w slides.md -o output/presentation.pdf
```

### Other Export Formats
```bash
# HTML (for web viewing)
marp slides.md -o output/presentation.html

# PowerPoint (if needed)
marp slides.md -o output/presentation.pptx
```

## Image Guidelines

**IMPORTANT**: The agent will check the `assets/` directory before creating slides. If you want images in your presentation but the assets/ directory is empty, the agent will STOP and ask you to add images first.

All images should be placed in the `assets/` directory with descriptive names:

- **Logos**: `logo.png`, `company-logo.png`
- **Diagrams**: `architecture-diagram.png`, `system-flow.png`
- **Charts**: `metrics-chart.png`, `roi-graph.png`
- **Photos**: `team-photo.jpg`, `product-screenshot.png`

**Recommended dimensions:**
- Full-width images: 1920x1080 (16:9 ratio)
- Diagrams: 1600x900 minimum
- Logos: 512x512 or vector (SVG)

## Presentation Workflow

1. **Plan Content**
   - Identify audience type (technical/non-technical)
   - Outline key sections (3-5 main points)
   - Determine slide count based on presentation length

2. **Prepare Images** (if needed)
   - If you want images, add them to `assets/` directory BEFORE creating slides
   - Agent will check for images and stop if directory is empty

3. **Create Slides**
   - Use Claude with marp-slides agent
   - Provide topic and key points
   - Agent will ask about:
     - Audience type (technical/non-technical)
     - Topic and key points
     - Duration and slide count
     - Do you want images? (If yes, checks assets/ directory)
     - PDF rendering preference
   - Agent generates complete slides.md

4. **Build PDF**
   - **Option A**: Agent renders PDF automatically (if chosen in step 2)
   - **Option B**: Run `marp slides.md -o output/presentation.pdf` yourself
   - Review PDF output
   - Iterate on content as needed

5. **Present**
   - Use PDF for presenting
   - Or use HTML with speaker notes if needed

## Agent Instructions

When Claude works on this project:

1. **Always ask about audience type first** (technical vs non-technical)
2. **Use the appropriate template** based on audience
3. **Reference images from assets/** - assume they exist
4. **Keep slides focused** - one main idea per slide
5. **Include build commands** in README.md if missing
6. **Verify frontmatter** includes marp: true, theme, paginate

## Common Tasks

**Create new presentation:**
```
Claude, use the marp-slides agent to create a presentation about [TOPIC] for [AUDIENCE TYPE]
```

**Update existing slides:**
```
Claude, update slides.md to add a new section about [TOPIC] after slide X
```

**Review presentation:**
```
Claude, review slides.md and suggest improvements for [AUDIENCE TYPE]
```

## Notes

- This project uses default Marp themes for easy PDF export
- Fonts are handled automatically by themes (no custom fonts needed)
- All presentations should export cleanly to PDF without errors
- Keep slide content concise - aim for minimal text, maximum impact
