# DEFRA Template Specification

## Identity

- **Slide dimensions:** 25.4 cm × 14.29 cm (widescreen 16:9)

## Assets

Always use these files — never substitute text placeholders.

| File | Use |
|------|-----|
| `assets/defra/cover_bg.png` | Full-bleed cover background with comprehensive DEFRA branding |
| `assets/defra/logo_wide.png` | Defra logo — cover slide top-right |
| `assets/defra/logo_tall.png` | Defra logo — section divider right panel |

## Colours

| Name | Hex | Usage |
|------|-----|-------|
| Defra Green | `#00AF41` | Header bars, section divider background, separator lines, placeholder border |
| Green (page number) | `#00B050` | Page number box fill |
| White | `#FFFFFF` | Slide backgrounds, text on dark fills, panels |
| Black | `#000000` | Body text, footer text |
| Placeholder grey | `#EBEBEB` | Placeholder box fill |
| Placeholder text | `#666666` | Label inside placeholder box |

## Fonts

| Role | Typeface | Size | Style |
|------|----------|------|-------|
| Cover title | Arial | 28 pt | Bold, white |
| Cover supplier | Arial | 24 pt | Regular, white |
| Cover info | Arial | 18 pt | Regular, white |
| Section header | Arial | 22 pt | Bold, white |
| Content header | Arial | 18 pt | Regular, white |
| Slide title | Arial | 18 pt | Bold, black |
| Body text | Calibri | 14 pt | Regular, black |
| Footer | Arial | 10 pt | Regular |
| Page number | Arial | 10 pt | Regular, white |
| Placeholder label | Arial | 14 pt | Regular, `#666666` |

## Slide Types

All dimensions in cm.

### 1. Cover Slide

| Element | x | y | w | h | Notes |
|---------|---|---|---|---|-------|
| Background image | 0.0 | 0.0 | 25.4 | 14.29 | `assets/cover_bg.png` |
| Defra logo (wide) | 19.29 | 0.38 | 5.65 | 1.50 | `assets/logo_wide.png` |
| Title text box | 1.20 | 4.52 | 16.89 | 2.65 | 28 pt Arial Bold, white, no fill |
| Supplier text box | 1.20 | 7.20 | 19.98 | 1.03 | 24 pt Arial, white, no fill |
| Info table | 1.20 | 8.83 | 19.98 | 1.50 | Date/version info table |

Title: `[Subject]`
Supplier: `Equal Experts`
Info table: Date and version information in tabular format

### 2. Section Divider Slide

| Element | x | y | w | h | Notes |
|---------|---|---|---|---|-------|
| Green background | 0.0 | 0.0 | 25.4 | 14.29 | fill `#00AF41` |
| White bottom panel | 0.0 | 11.27 | 20.39 | 3.08 | fill `#FFFFFF` |
| White right sidebar | 20.39 | 0.0 | 5.01 | 14.34 | fill `#FFFFFF` |
| Defra logo (tall) | 21.61 | 7.34 | 2.29 | 3.92 | `assets/logo_tall.png` |
| Section header text | 1.15 | 3.01 | 17.75 | 1.20 | 22 pt Arial Bold, white |
| Footer | 1.27 | 13.21 | 15.76 | 0.76 | 10 pt Arial, black, no fill — `Official` |
| Page number box | 23.31 | 13.24 | 1.14 | 0.76 | fill `#00B050`, 10 pt Arial, white |

### 3. Content Slide

| Element | x | y | w | h | Notes |
|---------|---|---|---|---|-------|
| White background | 0.0 | 0.0 | 25.4 | 14.29 | fill `#FFFFFF` |
| Green header bar | 0.0 | 0.0 | 24.7 | 1.05 | fill `#00AF41` |
| Header text | 0.18 | 0.05 | 9.5 | 1.03 | 18 pt Calibri, white |
| Separator line | 0.7 | 1.10 | 24.0 | 0.03 | fill `#00AF41` |
| Slide title | 0.70 | 1.20 | 23.00 | 1.30 | 18 pt Arial Bold, black, no fill |
| Body text | 0.70 | 2.60 | 23.00 | 10.61 | 14 pt Calibri, black, no fill |
| Footer | 1.27 | 13.21 | 15.76 | 0.76 | 10 pt Arial, black, no fill — `Official` |
| Page number box | 23.31 | 13.24 | 1.14 | 0.76 | fill `#00B050`, 10 pt Arial, white |

Content area: y=1.10 to y=13.21 cm.
Header text format: `[Project Name] - [Report Type] : [Period]`

### 4. Content Slide — Image Left

Content chrome identical to slide 3. Left column: placeholder. Right column: title + body text.

| Element | x | y | w | h | Notes |
|---------|---|---|---|---|-------|
| **Placeholder (left)** | **0.70** | **1.15** | **11.80** | **12.06** | fill `#EBEBEB`, border `#00AF41` 1.5 pt, label centred |
| Slide title (right) | 12.90 | 1.20 | 11.80 | 1.30 | 18 pt Arial Bold, black, no fill |
| Body text (right) | 12.90 | 2.60 | 11.80 | 10.61 | 14 pt Calibri, black, no fill |

### 5. Content Slide — Image Right

Content chrome identical to slide 3. Left column: title + body text. Right column: placeholder.

| Element | x | y | w | h | Notes |
|---------|---|---|---|---|-------|
| Slide title (left) | 0.70 | 1.20 | 11.80 | 1.30 | 18 pt Arial Bold, black, no fill |
| Body text (left) | 0.70 | 2.60 | 11.80 | 10.61 | 14 pt Calibri, black, no fill |
| **Placeholder (right)** | **12.90** | **1.15** | **11.80** | **12.06** | fill `#EBEBEB`, border `#00AF41` 1.5 pt, label centred |

### 6. Content Slide — Two Column Text

Content chrome identical to slide 3. Two columns of text side by side with equal spacing.

| Element | x | y | w | h | Notes |
|---------|---|---|---|---|-------|
| Slide title (full width) | 0.70 | 1.20 | 23.00 | 1.30 | 18 pt Arial Bold, black, no fill |
| Left column text | 0.70 | 2.60 | 11.30 | 10.61 | 14 pt Calibri, black, no fill |
| Right column text | 12.40 | 2.60 | 11.30 | 10.61 | 14 pt Calibri, black, no fill |

## Placeholder Box Specification

| Property | Value |
|----------|-------|
| Position & size | Exactly fills the image cell: x, y, w, h as defined for that slide type |
| Fill | `#EBEBEB` |
| Border | `#00AF41`, 1.5 pt solid |
| Label | `[ Insert image — slide N ]` (1-based), Arial 14 pt `#666666`, centred |

## Infographic Specifications

### Infographic Types Supported

| Type | Usage | DEFRA Styling |
|------|-------|---------------|
| **Data Visualisation** | Charts, graphs, statistics | DEFRA green primary, white backgrounds |
| **Process Flow** | Step-by-step processes, workflows | Green arrows, numbered steps |
| **Timeline** | Project timelines, milestones | Horizontal green timeline with white milestone boxes |
| **Comparison** | Before/after, vs. scenarios | Side-by-side layout with green divider |
| **Hierarchy** | Organisational charts, structures | Green boxes with white text, connecting lines |
| **Geographic** | Maps, location data | Green markers on neutral background |
| **Icon Arrays** | Feature lists, benefits | Green icons with black descriptive text |

### Infographic Placeholder Specification

| Property | Value |
|----------|-------|
| Fill | `#F0F8F0` (light green tint) |
| Border | `#00AF41`, 2 pt solid |
| Title | `[ INFOGRAPHIC: [Type] ]`, Arial 16 pt Bold `#00AF41` |
| Specification | Detailed requirements below title, Arial 12 pt `#666666` |
| Dimensions | Full content area or specified infographic zone |

### Infographic Content Requirements

**Data Visualisation:**
- Data source and values
- Chart type preference (bar, line, pie, etc.)
- Key message to highlight
- Colour coding requirements

**Process Flow:**
- Number of steps (max 7 for readability)
- Step descriptions and order
- Decision points or branches
- Start/end indicators

**Timeline:**
- Time period and scale
- Key milestones and dates
- Priority levels of events
- Direction (horizontal/vertical)

**Comparison:**
- Items being compared
- Comparison criteria
- Visual metaphor preference
- Emphasis areas

### Infographic Slide Layout

**Full-Slide Infographic:**
- Uses entire content area (0.70 cm margin from edges)
- Header with infographic title
- Main infographic area with specifications
- Small legend/key area if needed

**Half-Slide Infographic:**
- Compatible with existing Image Left/Right layouts
- Infographic occupies image area
- Text content in opposite column
- Clear visual hierarchy

### DEFRA Infographic Style Guidelines

**Colours:**
- Primary: DEFRA Green (`#00AF41`)
- Secondary: Light Green (`#7CC142`)
- Accent: Page Number Green (`#00B050`)
- Neutral: White (`#FFFFFF`), Light Grey (`#F5F5F5`)
- Text: Black (`#000000`), Dark Grey (`#666666`)

**Typography:**
- Titles: Arial Bold 18-24 pt
- Labels: Arial Regular 12-14 pt
- Data points: Arial Bold 14-16 pt
- Captions: Arial Regular 10 pt

**Visual Elements:**
- Clean, government-appropriate styling
- High contrast for accessibility
- Consistent spacing and alignment
- Professional iconography