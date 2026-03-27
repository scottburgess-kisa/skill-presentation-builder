# Workflow: Content to Presentation

## Purpose
This workflow takes meeting transcripts and supporting materials (matrices, quotes, reference documents) about presentation requirements and transforms them into a polished PowerPoint presentation through a series of structured stages. Each stage builds on the last, passing enriched data forward.

## Overview
Stage 1 — Analyse all input materials for presentation requirements
Stage 2 — Template and structure selection
Stage 3 — Targeted clarify and enrich presentation details
Stage 4 — Generate presentation

---

## Stage 1 — Analyse Input Materials for Presentation Requirements

### Instructions
1. Ask the user about their input materials:
   "What files do you have for this presentation?

   **Primary source (required):**
   - Meeting transcript discussing presentation requirements

   **Supporting materials (optional):**
   - Matrices or tables for data presentation
   - Quote collections for testimonials/insights
   - Reference documents with key information

   All files should be in the transcripts/ folder.
   What is your main transcript filename, and do you have any supporting files?"

2. Run the analyse-presentation-requirements skill:
   Follow all instructions in:
   skills/analyse-presentation-requirements/SKILL.md

   **IMPORTANT:** Pass all identified files to the skill:
   - Primary transcript file (main source of requirements)
   - Supporting files (matrices, quotes, reference materials)

   The skill will process each file type appropriately and integrate findings.

3. Save the JSON output to:
   working/analyse-output.json

4. Display the human readable summary to the user.

5. Ask the user:
   "Does this summary look accurate?
   Reply yes to continue or tell me anything that
   needs correcting before we move on."

6. If the user requests corrections, update the JSON
   in working/analyse-output.json accordingly and
   display the corrected summary.

7. Once the user confirms, move to Stage 2.

---

## Stage 2 — Template and Structure Selection

### Instructions
1. Load the JSON from: working/analyse-output.json

2. Review the presentation requirements and assess:
   - **Template suitability:** Which template (DEFRA, corporate, etc.) best fits the context
   - **Presentation structure:** How many slides, what types of layouts needed
   - **Content readiness:** What information is available vs. what needs clarification

3. Present the analysis to the user in this format:

---
Here is my analysis of your presentation requirements:

🎨 **Recommended Template:** [Template name]
   [One sentence explaining why this template fits]
   [Note any template considerations]

📊 **Proposed Structure:** [X slides total]
   • [List proposed slide types and purposes]
   • [Note any special layout requirements]

📝 **Content Assessment:**
   • **Available:** [What we have from the transcript]
   • **Needs clarification:** [What gaps need filling]

**Confidence Level:** [High/Medium/Low] - [Brief reasoning]

Does this structure look right?
Reply "yes" to continue, or tell me what needs adjusting.
---

4. Wait for the user to confirm the structure and template
   before moving to Stage 3.

---

## Stage 3 — Targeted Clarify and Enrich Presentation Details

### Instructions
1. Load the JSON from: working/analyse-output.json

2. Run the clarify-presentation skill:
   Follow all instructions in: skills/clarify-presentation/SKILL.md

   The skill will ask targeted questions to fill gaps in:
   - Slide content and messaging
   - Visual requirements and image needs
   - Audience considerations
   - Key data points or metrics
   - Call-to-action elements

3. Save the enriched JSON output to:
   working/clarify-output.json

4. Move to Stage 4.

---

## Stage 4 — Generate Presentation

### Instructions
1. Load the JSON from: working/clarify-output.json

2. Create an agent using the Agent tool:
   ```
   Agent tool with:
   - description: "Generate PowerPoint presentation"
   - prompt: "Load working/clarify-output.json and follow all instructions in skills/generate-presentation/SKILL.md. Create the presentation using the specified template and save to output/. Include detailed slide content, proper layouts, and image placeholders where specified."
   - run_in_background: true
   ```

3. You will be automatically notified when the agent completes.

4. Once the agent completes, verify the output exists in output/ folder.

5. Display this summary to the user:

---
✅ Presentation generation complete!

**Created:** [Presentation filename in output/ folder]
**Template:** [Template used]
**Slides:** [Number of slides created]
**Special features:** [Any image placeholders, special layouts, etc.]

**Next Steps:**
- Review the presentation in the output/ folder
- Replace image placeholders with actual images
- Make any final adjustments needed

The workflow is now complete!
---

### Error Handling
If the agent fails:
- Report what went wrong
- Suggest manual execution of generate-presentation skill
- Offer to retry with different parameters


## File Structure Reference
transcripts/    — input files go here: meeting transcripts, matrices, quotes, reference materials (read-only)
working/        — intermediate JSON files (managed automatically)
output/         — final generated presentations
skills/         — skill files for each stage
templates/      — presentation template specifications

## Notes
- Do not skip stages — each stage feeds the next
- The working/ folder is managed automatically by the workflow
- Stage 4 generates the final presentation using existing presentation-tools.py
- Files in the transcripts/ folder are read-only inputs
- Generated presentations will include image placeholders where the transcript mentions visual needs
- The workflow adapts to any available presentation template
- After generation, users manually review and refine the presentation as needed