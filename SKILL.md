# presentation-builder

Comprehensive PowerPoint presentation toolkit using configurable templates. Supports converting existing presentations, creating new presentations from specifications, and structured workflow from meeting transcripts.

## Template Selection

**Default:** DEFRA template (`templates/defra.md`)
**Override:** Specify alternative template with `--template=<name>` (e.g., `--template=corporate`)

Available templates in `templates/` directory.

---

## Modes

### Convert Mode (default)
Converts source `.pptx` files to the specified template, replacing images with labelled placeholder boxes.

**Trigger:** When `input/` folder contains `.pptx` files, or user explicitly requests conversion.

### Create Mode
Creates new presentations using the specified template from user content specifications.

**Trigger:** When user provides content outline/specifications without source files.

### Transcript Mode
Structured workflow that analyses meeting transcripts about presentation requirements and guides through clarification to create tailored presentations.

**Trigger:** When user requests "transcript workflow" or "run transcript-workflow.md"

**Process:** Multi-stage workflow including transcript analysis, requirement clarification, and guided presentation generation.

---

## Convert Mode Workflow

1. Read and analyse each `.pptx` in `input/`
2. Rebuild using the specified template rules and formatting
3. Draw a placeholder box wherever the source had an image
4. Normalise body text spacing: always insert exactly one blank line between the slide title and the first bullet, stripping any existing leading blank lines from the source first
5. Save to `output/` with `-placeholders` appended before the extension (e.g. `source.pptx` → `source-placeholders.pptx`)
6. Report which slides have placeholders

### Conversion Rules
- Map each source slide to the closest template slide type as defined in the selected template
- Preserve all text content and data — do not invent or omit content
- Apply template colours, fonts, and layout dimensions exactly as specified
- Follow template-specific branding rules (supplier, logos, etc.)
- If the source has no clear cover slide, create one using the deck title and today's date
- If the source has section breaks or divider slides, convert them to template Section Divider slides
- If a source slide has a significant image alongside text, use appropriate image layout (match the side from the source) and draw a placeholder in the image cell
- If a source slide has content that would benefit from side-by-side layout (comparisons, lists, etc.), use template Two Column layout
- Do **not** extract, copy, or process images from the source file
- All other slides become standard Content slides
- Process all files in `input/` in a single run unless told otherwise

### Placeholder Labels for Conversion
`[ Insert image — source slide N ]` (1-based slide numbers from the original presentation)

---

## Create Mode Workflow

1. Take user content requirements for slides (titles, bullet points, layout preferences)
2. Create a new presentation using the specified template rules and formatting
3. Build slides using the template layouts and styling
4. Apply template colours, fonts, and branding exactly as specified
5. Save to `output/` with descriptive filename
6. Report slide structure and any special layouts used

### Creation Rules
- Always start with a template-compliant cover slide following template branding rules
- Use today's date and version 1.0 unless specified otherwise
- Map user content to the most appropriate template slide types
- For image requirements, create placeholder boxes with appropriate labels
- Maintain consistent template branding throughout
- Follow exact typography and layout specifications from the selected template

### Content Input Formats
Accept content in various formats:
- Simple bullet point lists
- Slide-by-slide specifications
- Topic outlines with subtopics
- Mixed content with image requirements

### Placeholder Labels for Creation
`[ Insert image — slide N ]` (1-based slide numbers)

---

## Reporting

### Convert Mode
```
ℹ Placeholders added in "Example Deck.pptx":
  • Slide 2 "Who we 'spoke' to:" — image left (source slide 2)
  • Slide 4 "Policy vs. Code Mismatches" — image left (source slide 4)
```

### Create Mode
```
ℹ Created "Project Overview.pptx":
  • Slide 1: Cover slide
  • Slide 2: Section divider "Introduction"
  • Slide 3: Content — image right "Key findings"
  • Slide 4: Two column text "Comparison"
```

---

## Implementation

Use `presentation-tools.py` for both conversion and creation logic, ensuring it follows the selected template specification exactly.

### Template Configuration

The script reads template specifications from `templates/<template-name>.md` and applies the defined:
- Colours, fonts, and dimensions
- Slide layouts and positioning
- Asset paths and branding elements
- Placeholder styling

### Adding New Templates

1. Create `templates/your-template.md` following the template format (see `templates/defra.md` as example)
2. Add corresponding assets to `assets/your-template/`
3. Use with `--template=your-template`

---

## Transcript Mode Workflow

### Purpose
Transform meeting transcripts about presentation needs into polished PowerPoint presentations through a structured 4-stage process.

### Workflow Stages

**Stage 1 — Analyse All Input Materials**
- Extract presentation requirements from meeting transcript
- Process supporting materials: matrices, quotes, reference documents
- Identify purpose, audience, content needs, and structure preferences
- Generate structured analysis with confidence assessment

**Stage 2 — Template and Structure Selection**
- Recommend appropriate template based on requirements
- Propose slide structure and content organization
- Confirm approach with user before proceeding

**Stage 3 — Clarify and Enrich**
- Ask targeted questions to fill identified gaps
- Refine content specifications and visual requirements
- Ensure sufficient detail for high-quality generation

**Stage 4 — Generate Presentation**
- Create presentation using enriched requirements
- Apply specified template and formatting
- Include content, image placeholders, and detailed infographic specifications
- Provide final presentation ready for user review

### File Structure for Transcript Mode
```
transcripts/                    — input files for presentation building
├── [meeting-transcript].txt    — primary transcript (required)
├── [matrices].csv/.xlsx        — data tables and comparisons (optional)
├── [quotes].txt/.docx          — testimonials and insights (optional)
└── supporting-materials/       — additional reference documents
working/                        — intermediate analysis files (managed automatically)
output/                         — final generated presentations (shared with other modes)
skills/                         — workflow stage implementations
```

### Starting Transcript Workflow
To use transcript mode, say:
"Please run the transcript-workflow.md with my materials"

Then place your files in the `transcripts/` folder:
- **Required:** Meeting transcript about presentation requirements
- **Optional:** Supporting materials (matrices, quotes, reference documents)

### Implementation
Transcript mode uses the existing `presentation-tools.py` for final generation, but adds structured analysis and clarification stages to ensure high-quality results from meeting discussions.