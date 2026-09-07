# Telugu Document Annotation Workflow

## Overview
This document describes the systematic workflow for annotating and transcribing Telugu PDF documents for AI training data.

## Workflow Steps

### Step 1: Document Sourcing
- Source publicly accessible Telugu PDFs from:
  - Government educational portals (AP SCERT, Telangana SCERT)
  - Public domain book archives (archive.org, TTD ebooks)
  - Newspaper digital editions (Eenadu, Sakshi, Andhra Jyothi)
- Record source URL, document type, and access date
- Verify document contains multimodal elements (images, tables, diagrams, or handwriting)

### Step 2: Page Analysis
- Identify all meaningful regions on the page:
  - Document title
  - Section headings
  - Paragraphs
  - Lists (bulleted or numbered)
  - Tables
  - Figures/diagrams
  - Captions
  - Formulas
  - Question/answer fields
  - Handwritten text
- Note page dimensions and orientation

### Step 3: Region Bounding
- Draw precise bounding boxes around each identified region
- Ensure boxes tightly fit content without cutting off text
- Handle overlapping regions by creating separate annotations
- For multi-column layouts, annotate column by column following reading order

### Step 4: Component Typing
- Assign each region a component type from the taxonomy:
  - `title` - Main document title
  - `heading` - Section/subsection headings
  - `paragraph` - Body text
  - `table` - Tabular data
  - `figure` - Images, diagrams, charts
  - `caption` - Text describing figures
  - `list` - Bulleted/numbered lists
  - `formula` - Mathematical expressions
  - `handwritten` - Handwritten content
  - `mixed_script` - Pages with multiple scripts

### Step 5: Reading Order Assignment
- Assign sequential reading-order indices (1, 2, 3...)
- Follow natural reading flow:
  - Left-to-right, top-to-bottom for single-column
  - Column-by-column for multi-column layouts
  - Header to footer flow
- Cross-reference with visual layout to ensure logical reading sequence

### Step 6: Relationship Mapping
- Link each region to its parent component:
  - Paragraph → section heading it belongs to
  - Caption → figure it describes
  - List item → parent list
  - Table cell → parent table
- Use consistent parent IDs (e.g., region_001, region_002)

### Step 7: Transcription
- Transcribe all text exactly as it appears in Telugu script
- Preserve:
  - Diacritics and conjunct forms
  - Numeral forms (Telugu or Arabic as in source)
  - Punctuation and spacing
  - Line breaks within paragraphs
- Flag any illegible regions with quality markers
- Do NOT transliterate or translate in the transcription field

### Step 8: Metadata Capture
- Record for each page:
  - Language: Telugu
  - Document type: textbook/newspaper/form/etc.
  - Source URL and access date
  - Page dimensions
  - Content flags: has_tables, has_formulas, has_handwriting
  - Script type: Telugu only / Mixed script

### Step 9: Quality Review
- Self-review checklist:
  - [ ] All meaningful regions identified
  - [ ] Bounding boxes accurately placed
  - [ ] Component types correctly assigned
  - [ ] Reading order reflects actual page flow
  - [ ] Transcriptions match source character-for-character
  - [ ] Parent-child relationships mapped
  - [ ] Metadata complete and accurate
- Flag any issues for second-expert review

### Step 10: Export and Delivery
- Export annotations in JSON format
- Include all metadata fields
- Package with source document references
- Document any issues or flags found during review

## Taxonomy Reference

| Component Type | Description | Example |
|----------------|-------------|---------|
| title | Main document title | "గణితశాస్త్రం - పదవ తరగతి" |
| heading | Section/subsection heading | "1.1 వర్గసమీకరణాలు" |
| paragraph | Body text content | Explanatory text |
| table | Tabular data structure | Data tables |
| figure | Images, diagrams, charts | Graphs, illustrations |
| caption | Text describing a figure | "చిత్రం 1.1: ..." |
| list | Bulleted/numbered items | Itemized lists |
| formula | Mathematical expressions | ax² + bx + c = 0 |
| handwritten | Handwritten content | Form entries |
| mixed_script | Multi-script pages | Telugu + English |

## Quality Standards

- **Character-level accuracy**: Zero tolerance for diacritic errors
- **Reading order**: Must match how a native Telugu reader would read the page
- **Completeness**: Every meaningful region must be captured
- **Consistency**: Same taxonomy applied across all documents
- **Traceability**: All annotations linked to source documents
