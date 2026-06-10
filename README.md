# medical-school-notes

Oxford Medicine Year 4 OSCE revision. Built from the actual Y4 source docs (MedEd Booklet 2025 + Clinical Syllabus 2025-26) — but it's not a substitute for reading the real thing.

Live at: **[msn.arshpatankar.com](https://msn.arshpatankar.com)**

---

## What's in it

Five self-contained HTML pages covering every examination in OSCE order:

**CVS → Resp → Abdo → Neuro limbs → Upper/lower limb → Cranial → Lump/breast → Neck/thyroid → Vascular**

- **Signs Bank** (`osce_atlas.html`) — examiner states a finding, work out the differential and investigations. Colour-coded by exam.
- **Investigation Map** (`osce_atlas.html`) — every test grouped by how many exams share it. Expands to show how to deploy it and when to think of it.
- **Differential Atlas** (`osce_atlas.html`) — all differentials tiled by examination. Click a tile for the sign that points to it, plus management principles.
- **Quiz** (`quiz.html`) — Anki-style spaced-repetition flip cards on signs. Missed / Hard / Got it rating stored in localStorage.
- **Examination Technique** (`technique.html`) — click through each exam step in MedEd booklet order. Sub-types for Neuro, Vascular, and Neck. Final step has a fill-in-blank "present your findings" template.
- **Data Interpretation** (`data.html`) — two tabs: systematic approach for ECG/CXR/AXR/ABG/Bloods, and a 56-card SRS quiz.

Key thing to know for Y4: patients are healthy volunteers. Examiners give you the finding verbally. The whole point of this is to build the reflex of "examiner says X → differential → investigations → simple management."

---

## Running it locally

Open any of the files in `y4/` directly in a browser. No build step, no dependencies.

---

## Sources

`y4/sources/` — the two PDFs everything is grounded in. If something in the app contradicts these, the PDFs win.

---

## Contributing

If something's missing or wrong, open a PR. The canonical data source is `y4/data/database.example.json` — edit there first, then mirror into the relevant JS constants in the HTML files (see `CLAUDE.md` for the full data flow).
