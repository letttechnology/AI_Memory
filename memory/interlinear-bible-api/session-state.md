# Session State

Date: 2026-05-29

## What was done

1. **Read-time hack in GlossChainService (WRONG — reverted)** — wired SenseSelectorService into resolveBatch(). Reverted after user corrected.

2. **Build-time integration in InflectionEngineService (ALSO WRONG — removed)** — wired SenseSelectorService into deriveGloss(). Same per-verse exception pattern. Removed entirely.

3. **Entire sense_selection_rule concept removed**:
   - Deleted: SenseSelectionRule.java, SenseSelectionRuleRepository.java, SenseSelectorService.java
   - Created V48__drop_sense_selection_rule.sql to drop the table
   - V46 and V47 kept as files (already applied), but V48 undoes their effect
   - InflectionEngineService still has stale SenseSelectorService references — not compiled

4. **Created #141** — tracking issue for "Deep Seek Code: AI recurring behavioral failures"

## Behavioral rules established

See preferences.md and issue #141 for the full rules. Key decisions:
- Two modes: collaborating (default, no code) vs execution (user says go ahead on agreed plan)
- Scope = the specific issue being discussed, not a general free pass
- Grep tool broken — use bash+findstr
- Always use dev.sh for servers

## Test results

195 tests run, 1 pre-existing failure: EchoTests.presentInd3rdPl (expected "have" got "corpus"). No regressions.

## Current state of repo

- `InflectionEngineService.java` has stale SenseSelectorService references — needs fix before next compile
- V48 migration written but not applied yet (server was running with V47 applied)
- Two deleted Java files: SenseSelectionRule.java, SenseSelectionRuleRepository.java, SenseSelectorService.java

## Next steps

UNDEFINED — session ended with process discussion, not technical work.
