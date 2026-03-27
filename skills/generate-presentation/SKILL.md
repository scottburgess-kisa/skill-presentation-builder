# generate-presentation

Generates a complete PowerPoint presentation from enriched requirements using the specified template and presentation tools.

---

## Purpose
Create a polished PowerPoint presentation based on enriched requirements from the clarify-presentation skill, using the appropriate template and including all specified content and placeholders.

## Input
- JSON from `working/clarify-output.json` (enriched presentation requirements)
- Template specifications from `templates/` directory
- Access to `presentation-tools.py` for generation

## Output
- Complete PowerPoint presentation saved to `output/` folder
- Presentation includes all specified slides with proper formatting
- Image placeholders where visual content was requested

## Process

### 1. Requirements Loading
Load the enriched JSON and extract:
- **Template choice:** From `visual_details.template_preference` or default to DEFRA
- **Slide structure:** From `clarifications_added.structure_details.slide_sequence`
- **Content details:** All content requirements and messaging
- **Visual specifications:** Image and chart placement requirements

### 2. Template Configuration
Based on the template choice:
- Load template specification from `templates/[template].md`
- Configure colors, fonts, and layout dimensions
- Prepare brand assets and logos
- Set up placeholder styling

### 3. Slide Generation Sequence
Generate slides in this order:

**Cover Slide:**
- Use presentation context purpose as title
- Apply template-specific supplier/branding rules
- Include appropriate date and version info
- Follow template cover slide specifications

**Section Dividers (if applicable):**
- Create dividers for major content sections
- Use section titles from content structure
- Apply template section divider formatting

**Content Slides:**
- Generate based on slide_sequence array
- Map content to appropriate slide types:
  - Standard content slides for text-heavy content
  - Image Left/Right for visual-supported content
  - Two Column for comparisons or side-by-side info
- Include all key messages and data points
- Apply proper text formatting and hierarchy

**Visual Placeholders:**
- Create placeholders for all specified images
- Use template placeholder specifications
- Label clearly: `[ Insert image - [description] ]`
- Position according to slide layout requirements

**Infographic Placeholders:**
- Create detailed infographic placeholders based on `infographic_specifications`
- Use template infographic placeholder styling (distinct from image placeholders)
- Include comprehensive specification within placeholder:
  - Type and purpose
  - Data points to include
  - Style preferences
  - Size and positioning requirements
- Label format: `[ INFOGRAPHIC: [Type] - [Purpose] ]`

### 4. Content Mapping Strategy

**Key Messages → Slide Titles and Headers**
- Use `key_messages_refined` for prominent slide titles
- Ensure message hierarchy matches intended flow

**Data Points → Content Details**
- Include `specific_data_points` in appropriate slides
- Format metrics and results prominently
- Create chart placeholders where data visualization is needed

**Topics → Slide Content**
- Map `key_topics` to individual slides or sections
- Ensure comprehensive coverage without duplication
- Match detail level to audience knowledge level

**Infographics → Visual Communication**
- Map `infographic_specifications` to appropriate slides
- Choose optimal slide layouts for each infographic type
- Include detailed specifications for designers/tools
- Ensure infographics support rather than compete with key messages

### 5. Quality Assurance
Before saving, verify:
- All slides follow template specifications exactly
- Placeholder boxes are properly sized and positioned
- Text formatting matches template requirements
- Slide sequence matches clarified structure
- All key content areas are covered

### 6. File Naming and Output
Save presentation as:
`[presentation_purpose]_[date].pptx`

For example:
- `Project_Alpha_Update_2024-03-27.pptx`
- `Q4_Results_Presentation_2024-03-27.pptx`
- `Client_Proposal_Presentation_2024-03-27.pptx`

## Implementation Notes

### Using presentation-tools.py
The skill should invoke the existing `presentation-tools.py` with:
- Template parameter from JSON requirements
- Content structure derived from enriched requirements
- All visual placeholder specifications

### Slide Type Selection
Choose appropriate slide types based on content:

**Standard Content Slides:**
- Text-heavy topics
- Lists and bullet points
- Process explanations

**Image Left/Right Slides:**
- Content with supporting visuals
- Before/after comparisons
- Process diagrams with explanation

**Two Column Slides:**
- Comparisons (pros/cons, before/after)
- Side-by-side information
- Options or alternatives

### Placeholder Management
For each visual requirement:
- Determine optimal slide position
- Create placeholder with template styling
- Include descriptive label from requirements
- Note in generation summary for user reference

## Error Handling

### Missing Content
If critical content is missing:
- Flag the issue in generation summary
- Create placeholder slide with clear [TO DO] markers
- Continue with remaining slides

### Template Issues
If template problems occur:
- Fall back to DEFRA template
- Note the issue in generation summary
- Complete presentation with available template

### Technical Failures
If presentation-tools.py fails:
- Save progress made so far
- Report specific error details
- Suggest manual completion steps

## Output Summary
After successful generation, provide:

```
✅ Presentation Generated Successfully!

📄 **File:** [filename.pptx]
📊 **Template:** [template used]
📈 **Structure:** [X slides total]
   • Cover slide
   • [X] content slides
   • [X] slides with image placeholders
   • [X] slides with infographic placeholders

🖼️ **Placeholders Created:** [X total]
   • **Images:** [List specific image placeholder descriptions]
   • **Infographics:** [List infographic types and purposes]

📝 **Key Content Included:**
   • [List main topics covered]
   • [Note any data points included]

⚠️ **Manual Steps Required:**
   • Replace image placeholders with actual images
   • Create infographics based on detailed specifications provided
   • [Any other manual tasks needed]
```

## Guidelines for Quality

### Content Accuracy
- Include all key messages without omission
- Ensure data points are prominently featured
- Match tone to audience and context requirements

### Visual Layout
- Follow template specifications exactly
- Ensure proper spacing and alignment
- Create meaningful placeholder labels

### Professional Polish
- Consistent formatting throughout
- Proper slide transitions and flow
- Clear call-to-action if specified

### User Experience
- Generate presentation ready for immediate review
- Include clear instructions for completing placeholders
- Provide summary of what was created