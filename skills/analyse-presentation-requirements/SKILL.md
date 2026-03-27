# analyse-presentation-requirements

Analyses meeting transcripts and supporting materials to extract presentation requirements and content specifications.

---

## Purpose
Extract structured presentation requirements from meeting transcripts and supporting materials (matrices, quotes, reference documents) to build comprehensive PowerPoint presentations.

## Input
- **Primary:** Transcript file from `transcripts/` folder containing meeting discussion about presentation needs
- **Supporting:** Additional files containing matrices, quotes, data tables, or reference materials
- **File Types:** .txt, .docx, .csv, .xlsx, .md files supported

## Output
- Structured JSON with presentation requirements
- Human-readable summary for user review

## Process

### 1. File Inventory and Categorisation
First, identify and categorise all input files:

**Primary Source Analysis:**
- Identify the main transcript file containing presentation requirements discussion
- Extract basic context: meeting type, participants, objectives

**Supporting Materials Analysis:**
- **Matrix/Table Files (.csv, .xlsx):** Extract data structures, identify potential infographic content
- **Quote Files (.txt, .docx, .md):** Extract testimonials, insights, key statements
- **Reference Documents:** Extract relevant facts, statistics, background information
- **Mixed Content Files:** Identify different content types within single files

### 2. Primary Transcript Analysis
Read the specified transcript and identify:

**Presentation Context:**
- Purpose and objective of the presentation
- Target audience (internal team, clients, stakeholders, etc.)
- Presentation setting (meeting, conference, workshop, etc.)
- Timeline and deadlines mentioned

**Content Requirements:**
- Key topics and themes to cover
- Specific data points, metrics, or results to include
- Messages and takeaways the team wants to convey
- Any existing content or sources mentioned

**Structure Preferences:**
- Number of slides discussed
- Preferred slide types (content, image-heavy, data charts, etc.)
- Flow and narrative structure
- Special requirements (interactive elements, appendices, etc.)

**Visual Requirements:**
- Images, charts, or diagrams mentioned
- Infographic needs (data visualisation, process flows, timelines, comparisons, etc.)
- Complex data that would benefit from visual representation
- Branding or template preferences
- Visual style discussions
- Any specific design requests

**Constraints and Considerations:**
- Time limits for presentation delivery
- Technical constraints mentioned
- Approval processes or stakeholders to consider
- Sensitive information to handle carefully

### 3. Supporting Materials Analysis

**Matrix and Table Processing:**
- Extract data structures and relationships
- Identify comparative information suitable for infographics
- Note data visualisation opportunities
- Capture column headers, data types, and key insights

**Quote and Testimonial Processing:**
- Extract impactful quotes with attribution
- Categorise by theme or topic relevance
- Identify emotional impact and credibility factors
- Note context and appropriate usage scenarios

**Reference Document Processing:**
- Extract key facts, statistics, and supporting evidence
- Identify background information that adds context
- Note regulatory or compliance considerations
- Capture expert insights or authoritative sources

**Integration Strategy:**
- Map supporting content to transcript requirements
- Identify gaps that supporting materials can fill
- Suggest optimal placement within presentation structure
- Note dependencies between different content sources

### 4. JSON Structure
Produce JSON with this structure:

```json
{
  "presentation_context": {
    "purpose": "string - main objective",
    "audience": "string - who will see this",
    "setting": "string - where it will be presented",
    "timeline": "string - when it's needed"
  },
  "content_requirements": {
    "key_topics": ["array of main topics"],
    "key_messages": ["array of key takeaways"],
    "data_points": ["array of metrics/results to include"],
    "existing_sources": ["array of mentioned source materials"]
  },
  "structure_preferences": {
    "slide_count_estimate": "number or range",
    "preferred_slide_types": ["array of slide types needed"],
    "narrative_flow": "string - desired story progression",
    "special_requirements": ["array of special needs"]
  },
  "visual_requirements": {
    "image_needs": ["array of image requirements"],
    "chart_needs": ["array of data visualization needs"],
    "infographic_needs": [
      {
        "type": "data_visualisation|process_flow|timeline|comparison|hierarchy|geographic|icon_array",
        "purpose": "string - what this infographic should communicate",
        "data_source": "string - where the data comes from",
        "complexity": "simple|moderate|complex",
        "priority": "high|medium|low"
      }
    ],
    "template_preference": "string - template style discussed",
    "branding_notes": "string - branding considerations"
  },
  "supporting_materials": {
    "matrices_and_tables": [
      {
        "filename": "string - source file name",
        "content_type": "data_table|comparison_matrix|survey_results|statistics",
        "key_data": ["array of important data points"],
        "infographic_potential": "high|medium|low",
        "suggested_usage": "string - how to incorporate into presentation"
      }
    ],
    "quotes_and_testimonials": [
      {
        "filename": "string - source file name",
        "quote_text": "string - the actual quote",
        "attribution": "string - who said it",
        "theme": "string - topic or category",
        "impact_level": "high|medium|low",
        "suggested_placement": "string - where in presentation this fits"
      }
    ],
    "reference_materials": [
      {
        "filename": "string - source file name",
        "content_summary": "string - what this document contains",
        "key_insights": ["array of important points"],
        "supporting_evidence": ["array of facts/statistics"],
        "relevance_to_presentation": "string - how this supports the presentation"
      }
    ]
  },
  "constraints": {
    "time_limits": "string - presentation time constraints",
    "technical_constraints": ["array of technical limitations"],
    "approval_requirements": ["array of approval needs"],
    "sensitivity_notes": "string - confidential content considerations"
  },
  "gaps_identified": ["array of areas needing clarification"],
  "confidence_assessment": {
    "overall": "high/medium/low",
    "content_clarity": "high/medium/low",
    "structure_clarity": "high/medium/low",
    "visual_clarity": "high/medium/low"
  }
}
```

### 3. Human-Readable Summary
Generate a clear summary covering:

**🎯 Presentation Purpose**
[Purpose and audience in plain language]

**📋 Key Content Areas**
[Main topics and messages identified]

**🏗️ Proposed Structure**
[Slide count and types suggested]

**🎨 Visual Requirements**
[Images, charts, infographics, and design needs]

**📂 Supporting Materials Found**
[Summary of matrices, quotes, and reference materials available]

**⚠️ Areas Needing Clarification**
[What gaps were identified]

**📊 Confidence Level: [High/Medium/Low]**
[Brief explanation of confidence assessment]

## Guidelines

### Content Extraction
- Focus on explicit requirements mentioned in the transcript discussion
- Note implicit needs based on context
- Identify conflicting requirements that need resolution
- Flag areas where the discussion was unclear or incomplete

### Supporting Materials Integration
- **Matrices/Tables:** Assess data structure, identify visualisation opportunities, note comparative elements
- **Quotes:** Evaluate impact and relevance, suggest thematic grouping, consider placement strategy
- **References:** Extract key facts and supporting evidence, identify authoritative sources, note compliance considerations
- **Content Mapping:** Connect supporting materials to transcript requirements, identify synergies and gaps

### Structure Analysis
- Infer appropriate slide types from content discussions
- Consider presentation flow and narrative structure
- Account for audience expectations and setting
- Note any accessibility or technical requirements

### Gap Identification
- What content exists vs. what needs to be created
- Which visual elements are defined vs. need specification
- Areas where team consensus wasn't clear
- Technical details that weren't discussed

### Confidence Assessment
Rate confidence based on:
- **High:** Clear requirements, good detail, team consensus
- **Medium:** Most requirements clear but some gaps or ambiguity
- **Low:** Vague requirements, significant gaps, conflicting input

## Output Files
- Save JSON to: `working/analyse-output.json`
- Display human-readable summary to user
- Include confidence assessment and next steps