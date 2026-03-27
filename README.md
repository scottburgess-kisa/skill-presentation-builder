# Presentation Builder

This skill provides comprehensive functionality for working with branded PowerPoint presentations using configurable templates:

## Skill: [SKILL.md](SKILL.md)

**Convert Mode:** Converts existing PowerPoint files to specified template format, replacing images with placeholder boxes for manual insertion.

**Create Mode:** Creates new presentations from scratch using specified template and user content specifications.

**Transcript Mode:** Structured workflow that analyses meeting transcripts about presentation requirements, asks clarification questions, and generates tailored presentations with detailed infographic specifications.

**Template System:** Supports multiple presentation styles - defaults to DEFRA, can use any configured template.

## Template Resources

- **[templates/](templates/)** - Template specifications (defra.md, corporate.md, etc.)
- **assets/** - Template-specific brand assets organised by template name
- **presentation-tools.py** - Python implementation

## File Structure

```
skill-presentation-builder/
├── SKILL.md                     # Main skill definition
├── presentation-tools.py        # Implementation script
├── transcript-workflow.md       # Transcript-to-presentation workflow
├── input/                       # 📥 Source presentations for conversion
├── output/                      # 📤 Generated presentations
├── transcripts/                 # 📝 Meeting transcripts for analysis
├── working/                     # 🔧 Workflow intermediate files
├── skills/                      # 🛠️ Workflow stage implementations
│   ├── analyse-presentation-requirements/
│   ├── clarify-presentation/
│   └── generate-presentation/
├── templates/
│   ├── defra.md                # DEFRA government template
│   ├── corporate.md            # Corporate template example
│   └── README.md               # Template system documentation
├── assets/
│   ├── defra/                  # DEFRA brand assets
│   │   ├── cover_bg.png
│   │   ├── logo_wide.png
│   │   └── logo_tall.png
│   └── corporate/              # Corporate template assets
├── example/
│   └── reformat Defra slide.pptx
└── .claude/
    └── settings.json           # Permissions configuration
```

## Usage

### Convert Mode (Existing Presentations)

**How to trigger:** Place `.pptx` files in the `input/` folder

**Examples:**
```bash
# Convert with default DEFRA template
# 1. Place your-presentation.pptx in input/
# 2. Run the skill
/presentation-converter

# Convert with different template
/presentation-converter --template=corporate
```

**Result:** Creates `your-presentation-placeholders.pptx` in `output/` folder

### Create Mode (New Presentations)

**How to trigger:** Provide content specifications without input files

**Examples:**
```bash
# Create new DEFRA presentation
/presentation-converter "Create presentation about project status with slides:
- Cover: Project Alpha Update
- Section: Overview
- Content: Key achievements (needs image)
- Two column: Next steps vs Risks"

# Create with different template
/presentation-converter --template=corporate "Create sales deck with..."
```

**Result:** Creates descriptively-named presentation in `output/` folder

### Transcript Mode (Workflow-Based)

**How to trigger:** Request the transcript workflow with meeting transcript and supporting materials

**Examples:**
```bash
# Run enhanced transcript workflow
# 1. Place files in transcripts/:
#    - meeting-transcript.txt (required)
#    - data-matrix.csv (optional)
#    - customer-quotes.docx (optional)
#    - reference-materials/ (optional)
# 2. Request workflow execution
"Please run the transcript-workflow.md with my materials"

# Process includes:
# - Analyse transcript and supporting materials
# - Process matrices, quotes, and reference documents
# - Select template and structure
# - Ask clarification questions to fill gaps
# - Generate presentation with integrated content and infographics
```

**Result:**
- Structured 4-stage process from multiple inputs to presentation
- Integrated matrices, quotes, and supporting content
- Interactive clarification to ensure quality
- Final presentation in `output/` folder ready for review

### Template Options

**Default (DEFRA):** Government branding, Equal Experts supplier
**Corporate:** Clean business template
**Custom:** Add your own in `templates/` directory

### Adding New Templates

1. Create `templates/your-template.md` following the format in existing templates
2. Add brand assets to `assets/your-template/`
3. Use with `--template=your-template`