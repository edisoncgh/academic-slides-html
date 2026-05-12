---
name: academic-slides-html
description: "Generate academic presentation design drafts as single HTML files with embedded images. Outputs a self-contained HTML slide deck (CSS scroll-snap, 16:9, static) plus a Markdown speaking script. Use when user wants to create academic slides, presentation design, paper talk, thesis defense, group meeting report, or literature review slides."
---

# Academic Slides HTML

Generate academic presentation **design drafts** as self-contained single HTML files. The output helps users understand "how to present this paper" rather than producing a ready-to-use PPT.

## Core Value

**Narrative design > Visual design.** Focus on:
- Constructing logical storytelling chains
- Controlling presentation rhythm
- Defining what each slide should communicate

## Output Artifacts

| Artifact | Purpose |
|----------|---------|
| `{topic}.html` | Self-contained slide deck (double-click to open in browser) |
| `{topic}-script.md` | Speaking script with per-slide talking points |

## When to Use

- Academic paper presentation
- Thesis defense
- Group meeting progress report
- Literature review / survey talk
- Conference talk preparation

## Prerequisites

**Input format: Markdown is strongly recommended.**

If user provides PDF or docx:
1. Suggest converting to Markdown first using `MarkItDown`, `OfficeCLI`, or similar tools
2. Proceed with the converted Markdown

## Workflow

### Step 1: Gather Information

Ask user these questions **one at a time**:

**Q1: Presentation type?**
- Paper presentation (own work)
- Paper presentation (others' work)
- Group meeting progress report
- Literature review / survey

**Q2: Presentation duration?** (in minutes)

**Q3: Input source?**
- Provide Markdown file path
- Paste content directly

### Step 2: Analyze Content

1. Read the input content
2. Identify paper structure (abstract, methods, experiments, conclusions)
3. **Discover all figures and tables** — list them with:
   - Figure/Table number
   - Caption
   - Location in document
4. Estimate content density and complexity

### Step 3: Plan Slide Structure

Based on presentation type and duration, plan the slide deck:

| Presentation Type | Default Structure |
|-------------------|-------------------|
| Paper (own) | Title → Motivation → Related Work → Method → Experiments → Conclusion → Q&A |
| Paper (others) | Title → Problem → Approach → Key Results → Insights → Q&A |
| Group meeting | Background → Work 1 → Work 2 → ... → Next Steps |
| Literature review | Theme → Approach A → Approach B → ... → Comparison → Summary |

**Slide count heuristic:**
- Short talk (10-15 min): 8-12 slides
- Standard talk (20-25 min): 15-20 slides
- Long talk (30+ min): 20-30 slides

Adjust based on content density. Prioritize clarity over completeness.

### Step 4: Extract and Assign Images

This is critical to avoid "text-only" slides.

**4.1 Image Discovery**
- Parse the document for all Figure/Table references
- Create a manifest: `{number}, {caption}, {location}`

**4.2 Image Extraction** (if source is PDF)
- Use PyMuPDF or similar to extract figures
- Save as PNG files temporarily

**4.3 Image Assignment**
- Map each figure to the most relevant slide
- Consider narrative flow: introduce figures when they support the story
- Key figures (architecture, main results) get dedicated slides
- Minor figures can be grouped or omitted

**4.4 Image Embedding**
- Convert all images to base64
- Embed directly in HTML (self-contained file)

### Step 5: Generate HTML

See [references/html-template.md](references/html-template.md) for:
- HTML structure
- CSS specifications
- Slide layout patterns

**Key constraints:**
- Single self-contained HTML file
- CSS scroll-snap for slide navigation
- 16:9 aspect ratio
- System fonts: Chinese (SimSun/SimHei), English (Times New Roman)
- Pure static, no JavaScript interactions
- All images base64 embedded

### Step 6: Generate Speaking Script

Create `{topic}-script.md` with:

```markdown
# Speaking Script: {Topic}

## Slide 1: {Title}
**Key point:** {What to emphasize}
**Talking points:**
- {Point 1}
- {Point 2}
**Transition:** {How to connect to next slide}

## Slide 2: {Title}
...
```

### Step 7: Output Summary

```
Slide Deck Complete!

Topic: {topic}
Type: {presentation type}
Slides: {count}
Duration: {estimated minutes}

Artifacts:
- {topic}.html (open in browser)
- {topic}-script.md (speaking guide)
```

## Design Philosophy

- **Charts over text**: Figures and diagrams are the primary content
- **Minimal text**: Each slide has one core message
- **Academic formality**: Clean, professional, conference-ready
- **Self-contained**: Single HTML file, no external dependencies
- **Presentation-ready**: 16:9 ratio, optimized for projection

## References

| File | Content |
|------|---------|
| [references/html-template.md](references/html-template.md) | HTML structure and CSS specs |
| [references/slide-layouts.md](references/slide-layouts.md) | Layout patterns for different slide types |
| [references/image-handling.md](references/image-handling.md) | Image extraction and embedding guide |
