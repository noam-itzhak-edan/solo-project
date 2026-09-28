# Decisions

Format: decision · reason · rejected alternative.

| # | Date | Decision | Reason | Rejected alternative |
|---|---|---|---|---|
| 1 | 2026-09-28 | Brief hex values are canonical; mockup samples are recorded beside them only for reference | The mockup's colors are graded and compressed (amber samples at `#AA805A`, not `#C79A5B`) | Re-deriving the palette from the mockup pixels |
| 2 | 2026-09-28 | Add `--c-recess #1E1E1F` | Recessed tracks sample at `#262626`; no brief token is dark enough | Using charcoal for tracks (1.2:1 against charcoal plates, so the recess would disappear) |
| 3 | 2026-09-28 | Text-bearing plates use dark concrete `#5E5D5B` or a charcoal inset, never raw steel | Off-white on steel is 3.5:1 and fails AA for normal text | Matching the mockup's mid-steel top bar exactly |
| 4 | 2026-09-28 | Research sites (21st.dev, awwwards.com, clapat-templates.com) are unreachable from this container, so reference work falls back to the brief's descriptions until they're allowlisted | The egress proxy blocks them for both shell and web fetch | Scraping mirrors or caches |
| 5 | 2026-09-28 | Keep the mockup at `docs/reference/mockup-portrait.webp` in the repo | Phase 5 side-by-side screenshots need a stable path | Referencing a temp path that disappears with the container |
