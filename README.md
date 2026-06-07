# medical-school-notes

Oxford Medicine Year 4 OSCE revision. Built from the actual Y4 source docs (MedEd Booklet 2025 + Clinical Syllabus 2025-26) — but it's not a substitute for reading the real thing.

Live at: **[msn.arshpatankar.com](https://msn.arshpatankar.com)**

---

## What's in it

A single interactive HTML file covering every examination in OSCE order:

**CVS → Resp → Abdo → Neuro limbs → Upper/lower limb → Cranial → Lump/breast → Neck/thyroid → Vascular**

Three tabs:

- **Signs Bank** — examiner states a finding, you work out the differential and investigations. Has a quiz mode that hides answers until you tap.
- **Investigation Map** — every test grouped by how many exams share it, so you can see what's universal vs what's specific. Each test expands to show how to use it and when to think of it.
- **Differential Atlas** — all differentials tiled by examination, colour-coded. Click a tile for the sign that points to it.

Key thing to know for Y4: patients are healthy volunteers. Examiners give you the finding verbally. The whole point of this is to build the reflex of "examiner says X → I know the differential and investigations."

---

## Running it locally

Just open `y4/osce_atlas.html` in a browser. No build step, no dependencies.

---

## Sources

`y4/sources/` — the two PDFs everything is grounded in. If something in the app contradicts these, the PDFs win.

---

## Contributing

If I've missed something or got something wrong, open a PR. The data all lives in the JS at the top of `y4/osce_atlas.html` — `SECTIONS` for the signs bank, `POOLS` + `TEST_INFO` for the investigation map. Shouldn't be hard to find where to add things.
