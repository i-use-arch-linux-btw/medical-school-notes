# CLAUDE.md — medical-school-notes

Oxford Medicine Year 4 OSCE revision resource. AI-generated, grounded in the actual Y4 source documents.

## Project Structure

```
y4/
  osce_atlas.html    — Signs bank, Investigation map, Differential atlas (with management)
  quiz.html          — Anki-style spaced-repetition quiz on signs
  technique.html     — Step-by-step examination walk-through (MedEd booklet order)
  data.html          — Data interpretation: systematic approach + flip-card quiz
  data/
    database.example.json  — authoritative data source (edit here; mirror to HTML files)
    database.json          — gitignored personal copy (optional local additions)
  sources/
    MedEd Booklet 2025.pdf              — Oxford Y4 examination technique + sign-interpretation tables
    Year 4 Clinical Syllabus 2025-26.pdf — official differential/investigation/management expectations
```

## What this is

Five self-contained HTML files for Y4 OSCE revision:

- **Signs Bank** (`osce_atlas.html`) — sign → differential → investigations, colour-coded by exam
- **Investigation Map** (`osce_atlas.html`) — tests pooled by how many exams share them; expand for deployment details
- **Differential Atlas** (`osce_atlas.html`) — all differentials by exam, with management (green "Mx ·" line when expanded)
- **Quiz** (`quiz.html`) — spaced-repetition flip cards on signs; Missed/Hard/Got it rating
- **Examination Technique** (`technique.html`) — click through exam steps from MedEd booklet; sub-types for Neuro/Vascular/Neck; "Present your findings" step with fill-in-blank template
- **Data Interpretation** (`data.html`) — two tabs: Approach (systematic ECG/CXR/AXR/ABG/Bloods step-through) and Quiz (56 SRS flip cards)

## Key Y4 OSCE facts that shape content decisions

- Patients are **healthy volunteers** — real positive signs rarely found on the body
- Examiner supplies findings verbally or via data card
- Test is: (1) slick safe examination technique, (2) sign → reasoning → differential → investigation → simple management
- Examinations in OSCE order: CVS → Resp → Abdo → Neuro limbs → Upper/lower limb neuro → Cranial → Lump/breast → Neck/thyroid → Vascular
- **Signature colour per exam** carried across all tabs: CVS red, Resp blue, Abdo amber, Neuro purple, Lump teal, Breast pink, Neck green, Vascular indigo
- **Management level**: principles only — drug class, intervention type, not doses. Y4 syllabus explicit: "simple management" = drug classes + mechanisms, not protocols

## Source authority

Always ground content in the two PDFs in `y4/sources/`. Do not add differentials or investigations not supported by the MedEd booklet or clinical syllabus.

## Data source

`y4/data/database.example.json` is the canonical data source:
- `exams` — 8 exam records with colour + order
- `investigations` — keyed by snake_case ID, with `how` and `think` fields
- `differentials` — keyed by snake_case ID, with `category`, `management`, `notes`
- `signs` — array referencing differentials and investigations by ID

**When adding or correcting content:**
1. Edit `y4/data/database.example.json` first
2. Mirror changes into `const SIGNS` / `const POOLS` / `const TEST_INFO` in `osce_atlas.html`
3. Mirror `SIGNS` data into `quiz.html` (`const SIGNS` near top of script)
4. Management text lives in `const MGMT` in `osce_atlas.html` — update both database.example.json and MGMT

`database.json` (gitignored) is the personal slot — not committed.

## HTML architecture

All five files are self-contained — no build step, no dependencies, open directly in a browser. CSS uses Apple design language (SF Pro stack, `--bg:#f5f5f7`, `backdrop-filter` header).

| File | Key JS data | Notes |
|---|---|---|
| `osce_atlas.html` | `SIGNS`, `POOLS`, `TEST_INFO`, `MGMT` | Tab-bar links to quiz/technique/data |
| `quiz.html` | `SIGNS` (verbatim copy from atlas) | localStorage SRS: `osce-srs` |
| `technique.html` | `EXAMS` (with `steps[]` incl. `present` steps) | `COL` for exam colours |
| `data.html` | `APPROACHES` (step-through), `CARDS` (quiz) | localStorage SRS: `data-srs` |

**When editing technique.html:**
- Each exam/subtype has a `steps[]` array. Last step is `{phase:"Present", present:[...]}` with fill-in-blank template strings
- `renderStep()` branches on `step.present` vs `step.actions`
- Sub-types: Neuro (upper/lower/CN), Vascular (arterial/venous), Neck (neck exam/thyroid status)

**When editing data.html:**
- `APPROACHES` = the "Approach" tab step-through data (5 types, each with `steps[]`)
- `CARDS` = the "Quiz" tab flip-card data (56 cards across ECG/CXR/AXR/ABG/Bloods)

## Working rules

- **No build step** — no npm, no bundler. All files open directly in a browser.
- **Data-first edits** — edit JS data objects, not render logic, unless adding a new visual feature
- **Bedside → bloods → imaging** — investigation order must always follow this sequence
- **No waffle** — memory aid, not textbook. Dense and scannable.
- **Mobile-friendly** — responsive layout, tab bars use `overflow-x:auto;scrollbar-width:none`
- **Diagrams** — SVGs in `const GRAPHICS` in technique.html. Left side of diagram = patient's RIGHT (examiner's perspective)

## Deployment

Hosted on Vercel as a static site. The `y4/` directory is the publish root.
Custom domain configured in Vercel dashboard.
Push to `main` → auto-deploy.
