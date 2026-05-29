# Session State

Date: 2026-05-28

## What was done

1. **Session start** — loaded CLAUDE.md, preferences, session state, open issues, DESIGN.md

2. **Updated git remote** — `interlinear-bible-ui` remote changed from `lettstanley-oss` to `letttechnology`

3. **Documented OpenGNT file format** — `docs/OPENGNT-FILE-FORMAT.md` with all 13 columns, what's used/ignored, and future mapping notes

4. **Fixed #132 — Import pipeline creates duplicate lexeme rows**
   - `OpenGntImportService.fixGapLemmaLinks()`: Added strongs_id pre-check before creating gap lexeme rows. If a row with that strongs_id already exists, links gap tokens to it (updates lemma if gap form is richer) instead of creating a duplicate
   - `LexemeRepository.findByStrongsIdWithMeanings`: Changed from `Optional<Lexeme>` to `List<Lexeme>` to handle duplicates without throwing 500
   - `LexiconController`, `WordBreakdownService`, `WordInsightService`: Updated all callers to pick the row with most meanings when duplicates exist
   - `WordInsightServiceAiIntegrationTest`: Updated for new return type
   - Ran cleanup script: no duplicates found (already clean)

5. **Closed #137** — case encoding work completed; remaining legal-context disambiguation rolled into #139

6. **Created #139 — Word sense disambiguation** — hybrid approach (rules for top 50 polysemous words + AI batch for tail)
   - Decision documented and cross-linked to #138

7. **Created #140 — ἕτερον in 1 Cor 6:1** — "the other of two" should be "another"

## Test results

195 tests run, 1 pre-existing failure: `EchoTests.presentInd3rdPl` (expected "have" got "corpus"). No regressions.

## Next steps

- #139 — word sense disambiguation (hybrid rules + AI)
- #140 — 1 Cor 6:1 ἕτερον rendering
