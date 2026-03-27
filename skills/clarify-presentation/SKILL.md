# clarify-presentation

Asks targeted clarification questions to enrich presentation requirements and fill gaps identified during transcript analysis.

---

## Purpose
Fill gaps in presentation requirements by asking focused questions based on the analysis output, ensuring sufficient detail for high-quality presentation generation.

## Input
- JSON from `working/analyse-output.json` (from analyse-presentation-requirements skill)
- Analysis of what information is missing or unclear

## Output
- Enriched JSON with complete presentation specifications
- All gaps filled with user-provided clarifications

## Process

### 1. Gap Analysis
Load the analysis JSON and review:
- `gaps_identified` field for explicit gaps
- `confidence_assessment` scores for areas needing improvement
- Content areas that are sparse or unclear
- Visual requirements that need specification

### 2. Targeted Questions
Ask focused questions only for identified gaps. Group questions by category:

**Content Clarification Questions:**
- "What specific data points or metrics should be highlighted?"
- "What key message do you want the audience to remember?"
- "Are there any success stories or case studies to include?"
- "What level of detail is appropriate for [specific topic]?"

**Structure and Flow Questions:**
- "How much time will you have for the presentation?"
- "Should there be Q&A time built into the structure?"
- "Do you need an executive summary slide?"
- "Are there natural break points or sections?"

**Visual and Design Questions:**
- "Where do you envision images or charts being most effective?"
- "Do you have existing brand guidelines to follow?"
- "Are there specific types of charts (bar, line, pie) preferred?"
- "Should screenshots or mockups be included?"

**Infographic Clarification Questions:**
- "For the [data/process] mentioned, would an infographic help explain it better than text?"
- "What type of infographic would work best: data visualisation, process flow, timeline, or comparison?"
- "What's the key message this infographic should communicate?"
- "Do you have the specific data or steps that should be included?"
- "Should the infographic be simple and clean, or detailed and comprehensive?"
- "Are there existing examples or styles you'd like to reference?"

**Supporting Materials Questions:**
- "I found [X] data matrices/tables - which are most important for the presentation?"
- "For the quotes in [filename], which resonate most with your key messages?"
- "Should the data from [matrix file] be shown as charts, tables, or infographics?"
- "Which testimonials would have the strongest impact on your audience?"
- "How should we integrate the reference material from [filename] - as supporting evidence or main content?"
- "Do you want to highlight specific data comparisons from your matrices?"

**Audience and Context Questions:**
- "What's the audience's familiarity with [specific topics]?"
- "Are there sensitive topics that need careful handling?"
- "What actions do you want the audience to take after the presentation?"
- "Are there competing priorities or objections to address?"

### 3. Question Prioritization
**Limit: Maximum 5 questions per round**

Ask questions in order of importance:
1. **Critical gaps** that would prevent generation (ask these first)
2. **High-impact areas** that significantly affect quality
3. **Enhancement questions** that would improve the final result

If you have more than 5 questions total, prioritize the most critical ones for the first round and continue in subsequent rounds.

### 4. Response Integration
For each answer:
- Update the appropriate JSON fields
- Ask follow-up questions if the response raises new needs
- Validate that the response resolves the identified gap

### 5. Enriched JSON Structure
Extend the original JSON with:

```json
{
  [original fields from analyse-output.json],
  "clarifications_added": {
    "content_details": {
      "specific_data_points": ["array of confirmed metrics"],
      "key_messages_refined": ["array of priority messages"],
      "content_sources": ["array of where to get content"],
      "detail_levels": "string - how detailed to be"
    },
    "structure_details": {
      "confirmed_slide_count": "number",
      "slide_sequence": ["array of slide types in order"],
      "time_allocation": "string - time per section",
      "interaction_points": ["array of Q&A or interaction moments"]
    },
    "visual_details": {
      "image_specifications": ["array of specific image needs"],
      "chart_specifications": ["array of chart types and data"],
      "infographic_specifications": [
        {
          "type": "data_visualisation|process_flow|timeline|comparison|hierarchy|geographic|icon_array",
          "purpose": "string - key message to communicate",
          "data_source": "string - where data comes from",
          "data_points": ["array of specific data to include"],
          "complexity": "simple|moderate|complex",
          "style_preference": "string - visual style notes",
          "slide_location": "string - which slide this goes on",
          "size": "full_slide|half_slide|quarter_slide"
        }
      ],
      "placeholder_locations": ["array of where placeholders go"],
      "design_preferences": "string - style and branding notes"
    },
    "supporting_materials_usage": {
      "selected_matrices": [
        {
          "filename": "string",
          "usage_type": "infographic|table|chart|supporting_data",
          "presentation_location": "string - which slide",
          "priority": "high|medium|low"
        }
      ],
      "selected_quotes": [
        {
          "quote_text": "string",
          "attribution": "string",
          "placement_strategy": "slide_content|callout_box|testimonial_slide",
          "slide_location": "string"
        }
      ],
      "reference_integration": [
        {
          "content": "string - what to include",
          "usage": "supporting_evidence|background_context|key_statistic",
          "presentation_method": "text|infographic|callout"
        }
      ]
    },
    "audience_context": {
      "knowledge_level": "string - audience expertise",
      "decision_makers": ["array of key audience members"],
      "preferred_tone": "string - formal, casual, technical, etc.",
      "call_to_action": "string - what audience should do next"
    }
  },
  "final_confidence": {
    "content_readiness": "high/medium/low",
    "structure_readiness": "high/medium/low",
    "visual_readiness": "high/medium/low",
    "generation_readiness": "high/medium/low"
  },
  "ready_for_generation": true/false
}
```

## Question Flow Guidelines

### Start with Context
"Based on your transcript, I need to clarify a few details to create the best possible presentation."

### Limit Questions Per Round
**IMPORTANT:** Ask maximum 5 questions at a time to avoid overwhelming the user. If more clarification is needed:
- Process the first 5 most critical questions
- Wait for user responses and integrate them
- Ask the next batch of up to 5 questions if needed
- Continue in rounds until all gaps are filled

### Group Related Questions
Don't jump between topics - ask all content questions, then structure questions, etc.

### Use Transcript Context
"You mentioned [something from transcript] - can you elaborate on..."

### Validate Understanding
After each group: "Let me confirm I understand [topic] correctly..."

### Multi-Round Process
If you have more than 5 questions:
1. "I have a few questions to help create the best presentation. Let me start with the most important ones:"
2. Ask first 5 questions
3. After responses: "Thank you! I have a few more questions to ensure we get everything right:"
4. Continue until all critical gaps are addressed

### Conclude Clearly
"Great! I now have everything needed to generate your presentation."

## Quality Checks

Before finalizing, ensure:
- All `gaps_identified` items are addressed
- Confidence levels are now "medium" or "high"
- Sufficient detail exists for each proposed slide
- Visual requirements are specific enough for placeholder creation
- Content sources and key messages are clear

## Output Requirements
- Save enriched JSON to: `working/clarify-output.json`
- Set `ready_for_generation: true` only when all critical gaps are filled
- Include summary of what was clarified

## Guidelines for Questions

### Be Specific
Instead of "What images do you want?", ask "For the slide about [topic], what type of visual would best support the message?"

### Reference the Transcript
"You mentioned [specific point] - should this be a main slide or supporting detail?"

### Offer Options
"For showing the results, would you prefer a bar chart, line graph, or data table?"

### Validate Assumptions
"I'm assuming [interpretation] - is that correct?"

### Stay Focused
Only ask questions that directly impact presentation generation - avoid nice-to-have details.