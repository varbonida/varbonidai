# Log

Append-only operational history, most recent last. One line per meaningful
operation. Format: `## [YYYY-MM-DD] type | subject`

Types: `ingest`, `update`, `query`, `decision`, `client-log`, `lint`, `major-change`

Last five operations: `grep "^## \[" log.md | tail -5`

---

## [2026-08-27] ingest | Bootstrapped vault structure and git repo
## [2026-08-27] ingest | Created people/me.md from onboarding interview
## [2026-08-27] ingest | Created clients/kelly/overview.md
## [2026-08-27] ingest | Created clients/kelly/invoices.md
## [2026-08-27] ingest | Created clients/kelly/dictation-app/overview.md
## [2026-08-27] ingest | Created clients/kelly/dictation-app/decisions.md
## [2026-08-27] ingest | Ported dictation app changelogs, audits, and branding notes from the old vault
## [2026-08-27] ingest | Created clients/kelly/schengen-calculator/overview.md
## [2026-08-27] ingest | Created research stubs: n8n-automation, affiliate-marketing, ai-dropshipping, trading
## [2026-08-27] ingest | Created personal/job-search/overview.md
## [2026-08-27] ingest | Created questions/ios-build-without-mac.md
## [2026-08-27] decision | Created decisions/vault-as-single-source-of-truth.md
## [2026-08-27] update | Corrected dictation app workflow checkboxes against the real changelog state
## [2026-08-27] update | Recorded the VoiceInk to Handy desktop selection change as a contradiction
## [2026-08-27] ingest | Created index.md, log.md, changelog.md
## [2026-08-27] ingest | Created 12 planned project folders for Kelly's backlog
## [2026-08-27] update | Replaced Kelly's backlog table with links to the new project pages
## [2026-08-27] update | Added `planned` to the project status enum in CLAUDE.md
## [2026-08-27] decision | Every named client project now gets a folder at status: planned
## [2026-08-27] major-change | Archived SETUP.md to raw/_setup-archive; onboarding complete
