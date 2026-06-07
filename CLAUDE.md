# CLAUDE.md — medical-school-notes

Oxford Medicine Year 4 OSCE revision resource. AI-generated, grounded in the actual Y4 source documents.

## Project Structure

```
y4/
  osce_atlas.html          — single self-contained app (signs bank, investigation map, differential atlas)
  sources/
    MedEd Booklet 2025.pdf              — Oxford Y4 examination technique + sign-interpretation tables
    Year 4 Clinical Syllabus 2025-26.pdf — official differential/investigation/management expectations
```

## What this is

A single-file interactive HTML reference built for photographic memory + active recall:

- **Signs Bank** — examiner-states-finding → differential → bedside-first investigations (quiz mode available)
- **Investigation Map** — tests pooled by how many exams share them (Venn-style); each test tile expands to show deployment specifics + trigger logic
- **Differential Atlas** — tile wall of all differentials, grouped by exam, colour-coded

## Key Y4 OSCE facts that shape content decisions

- Patients are **healthy volunteers** — real positive signs rarely found on the body
- Examiner supplies findings verbally ("you hear a pansystolic murmur...") or via data card
- Test is: (1) slick safe examination technique, (2) sign → reasoning → differential → investigation → simple management
- Examinations in OSCE order: CVS → Resp → Abdo → Neuro limbs → Upper/lower limb neuro → Cranial → Lump/breast → Neck/thyroid → Vascular
- **Signature colour per exam** carried across all tabs: CVS red, Resp blue, Abdo amber, Neuro purple, Lump teal, Breast pink, Neck green, Vascular indigo

## Source authority

When updating content, always ground it in the two PDFs in `y4/sources/`. Do not add differentials or investigations that aren't supported by the MedEd booklet or the clinical syllabus.

## HTML architecture

The entire app lives in `y4/osce_atlas.html` — one file, no build step, no dependencies. All data is inline JS objects. CSS uses Apple design language (SF Pro stack, `--bg:#f5f5f7`, generous whitespace, `backdrop-filter` header).

When editing:
- Data lives in `const SECTIONS`, `const POOLS`, `const TEST_INFO` at the top of the `<script>` block
- Rendering is JS-driven — cards, tiles, and test pills are all generated from data; edit the data, not the DOM string templates, unless adding a new visual feature
- Colour system: `--c-cvs`, `--c-resp`, `--c-abdo`, `--c-neuro`, `--c-lump`, `--c-breast`, `--c-neck`, `--c-vasc` — use these, never hardcode hex for an exam

## Working rules

- **One file** — keep everything in `osce_atlas.html`. No split files, no npm, no build step.
- **Data-first edits** — add/correct a sign or investigation by editing the JS data objects, not by touching the render logic
- **Bedside → bloods → imaging** — investigation order must always follow this sequence
- **No waffle** — this is a memory aid, not a textbook. Entries are dense and scannable.
- **Quiz mode must still work** after any edit — it hides `.body` on `.card` elements; don't restructure that
- **Mobile-friendly** — the existing responsive layout uses `max-width:1040px` with `padding:0 22px`; preserve this

## Deployment

Hosted on Vercel as a static site. The `y4/` directory is the publish root.
Custom domain configured in Vercel dashboard.
Push to `main` → auto-deploy.
