# Session State — 2026-05-30

## Done
- Named new pipeline component: Token Sense Resolution (TSR)
- Fixed grep/glob tool Expand-Archive module loading (PSModulePath registry fix + PSGallery install; tool restart may be needed)
- Clarified architecture: TSR (build-time sense index selection) vs ContextualGloss (read-time overlay for 13 words) vs LITE pipeline (gloss_set_entry)
- Read and analyzed legacy Handler C (run_handler_c.py) — confirmed no admin endpoint, direct DB write (known violation)
- Confirmed architecture: TSR → token_sense_override → feeds into InflectionEngineService COALESCE → gloss_set_entry

## Next Steps
1. Build Java POST /admin/import-sense-selections endpoint for TSR JSONL import
2. Write tests for existing sense override controllers
3. Update DESIGN.md with TSR pipeline
4. Run full NT batch and review quality
5. Fix G3588 duplicate senses
