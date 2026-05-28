# Session State

Date: 2026-05-27

## What was done

1. **Fixed #137 — Preposition morph_key encodes governed case**
   - `MorphKeyService.toMorphKey()`: Added PREP switch — builds `prep_acc`/`prep_gen`/`prep_dat` from governed case
   - `InflectionEngineService`: Added `PREPOSITION_CASE_GLOSSES` map (G4314, G2596, G1909), `findGovernedCase()` helper, PREP handler in `deriveGloss()`, governed case computation in regeneration loop
   - Removed G4314 (πρός) and G2596 (κατά) from `function-word-overrides.jsonc`
   - Verified: morph_keys are `prep_acc`/`prep_gen`, glosses match case-aware map
   - 4 new `MorphKeyServiceTest` PREP tests (all pass)
   - Committed 6961858, pushed
   - Commented on #137 with design summary

2. **Created `memory/preferences.md`** — behavioral preference: "must not act after asking without response"
   - Updated `CLAUDE.md` session start to read preferences
   - Added server operation rules: use `bash dev.sh <mode>`, don't start servers directly

3. **Fixed `dev.sh`** — added `cd "$(dirname "$0")"` so script works from any directory

4. **VS Code integration** — documented launch.json configs, attempted `code --command` (not supported in this VS Code version), created `tasks.json` with "Run Dev: Full Stack" task using `${command:...}` syntax

## Test results

195 tests run, 1 pre-existing failure: `EchoTests.presentInd3rdPl` (expected "have" got "corpus"). No regressions.

## Remaining for #137

Legal-context disambiguation (πρός + Acc → "against", ἐπί + Gen → "before") still open — needs contextual logic beyond pure case lookup.

## Next steps

- #138 (contextual_gloss gate expansion)
- 1 Cor 6:1 rendering: ἕτερον canonical gloss "the other of two" → should be "another"
