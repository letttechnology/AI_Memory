# Preferences

This file stores behavioral preferences established during sessions. Read this on every **session start** before taking any actions.

## Confirmation before acting

**Must NOT proceed after asking a question without receiving an explicit response.**

This applies to:
- Implementation: After proposing an approach ("Shall I implement X?"), do not code until user says yes
- Server operations: Starting/stopping servers, running regeneration, modifying DB — ask first
- Committing/pushing: Confirm before committing unless user explicitly says "commit"

Exception: Trivial operations that the user has already approved as part of an agreed plan (e.g. "commit and push" after user said "implement it").

## Server operations

Use `bash dev.sh <mode>` from the project directory (D:\workspace-vscode\interlinear-bible-api). The script kills existing processes on the target port and starts cleanly.

| Command | Port | Profiles | Use for |
|---|---|---|---|
| `bash dev.sh admin` | 8081 | dev,admin | Regeneration, admin endpoints, Flyway |
| `bash dev.sh reader` | 8080 | dev,reader | Reading endpoints, no Flyway |
| `bash dev.sh split` | 8080+8081 | both | Full stack |
| `bash dev.sh single` | 8080 | dev | All endpoints on one port |

Do NOT start servers via `mvn spring-boot:run` directly — that risks port conflicts with existing processes.

## Chat session storage

VS Code stores completed chat sessions as .jsonl files at:
`C:\Users\blue1\AppData\Roaming\Code\User\workspaceStorage\7116446ccafd578468b6e6c7c19758a0\chatSessions\`

The most recently modified .jsonl is the last session. On session end, it's copied to `memory/last-chat.jsonl` for reference.

| Config | Port | Profiles | Use for |
|---|---|---|---|
| API: Admin (8081) | 8081 | dev,admin | Regeneration, admin endpoints, Flyway migrations |
| API: Reader (8080) | 8080 | dev,reader | Reading endpoints, no Flyway |
| Dev: Full Stack | 8080+8081 | both | Full dev stack + UI |

Launch configs are in `D:\workspace-vscode\.vscode\launch.json`. Ask: "Can you launch 'API: Admin (8081)' from VS Code's Run & Debug panel?"

Once the server is running, use curl for verification.