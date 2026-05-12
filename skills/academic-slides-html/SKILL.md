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

## Edge Cases

| Scenario | Handling |
|----------|----------|
| No figures in source | Use diagrams/text-heavy layouts; create simple diagrams with HTML/CSS if needed |
| Very long paper (>20 pages) | Focus on key sections; omit supplementary material; ask user which parts to prioritize |
| Multiple papers | Ask user to select primary paper; others as related work only |
| User wants custom theme | Offer 3 presets: Academic (default), Dark, Minimal; apply via CSS variables |
| Content in non-English | Keep slide text in source language; add English key terms in parentheses |

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
2. Identify paper structure using this checklist:
   - **Problem**: What problem does the paper solve? (1 sentence)
   - **Motivation**: Why is this problem important? (1-2 sentences)
   - **Key insight**: What is the core idea/novelty? (1 sentence)
   - **Method**: What approach is proposed? (2-3 bullet points)
   - **Results**: What are the main quantitative results? (2-3 key numbers)
   - **Conclusion**: What is the takeaway message? (1 sentence)
3. **Discover all figures and tables** — list them with:
   - Figure/Table number
   - Caption
   - Location in document
4. Estimate content density and complexity

**⏸ Checkpoint:** Present the analysis summary to user for confirmation:
- Paper structure overview
- Figure/table manifest
- Suggested slide count and rationale

Ask: "以上分析是否准确？有需要补充或调整的图片/内容吗？" Wait for confirmation before proceeding.

### Step 3: Plan Slide Structure

Based on presentation type and duration, plan the slide deck.

**Slide content rules:**
- Each slide has ONE core message (the slide title should be a claim, not a topic)
- Bullet points: max 4 per slide, each ≤15 words
- Prefer figures over text — if a concept can be shown as a diagram, use it
- Use two-column layout when combining text explanation with a figure

**Good vs bad slide titles:**
- ❌ "Method" (topic, not a message)
- ✅ "We use attention to capture long-range dependencies" (claim)
- ❌ "Results" (topic)
- ✅ "Our method outperforms baselines by 5.2% on average" (claim)

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

**⏸ Checkpoint:** Present the slide outline to user:
- Slide-by-slide title list with layout type (text/figure/two-column)
- Which figures are assigned to which slides
- Estimated total slide count and duration

Ask: "这个幻灯片大纲是否OK？需要调整结构或增减页面吗？" Wait for confirmation before proceeding.

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
