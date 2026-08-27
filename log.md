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
## [2026-08-27] ingest | Ported the Prompt Library from the old vault into prompts/ (4 prompts + index)
## [2026-08-27] update | Parameterized the hardcoded old-vault output path in prompts/audit-check.md
## [2026-08-27] ingest | Ported 04 Notes into research/: affiliate-marketing (replaced stub), ai-automation-agency
## [2026-08-27] ingest | Created concepts/project-notes-symlink.md from the old Inbox scratch
## [2026-08-27] update | Added the prompts/ folder and its rules to CLAUDE.md; updated index.md
## [2026-08-27] update | Fixed a stale old-vault path in the ported iOS audit
## [2026-08-27] update | Added .gitignore (Obsidian workspace files, .trash)
## [2026-08-27] update | Recorded the completed port on the vault migration decision page
## [2026-08-27] decision | Added raw/inbox/ drop zone; resolved the contradictory raw/ move rules in CLAUDE.md
## [2026-08-27] update | Added a session-start workflow to CLAUDE.md (read index.md and log.md before working)
## [2026-08-27] ingest | Created projects/portfolio/ (overview + updates) from the repo's PRODUCT.md and package.json
## [2026-08-27] update | Added projects/ to CLAUDE.md for own (non-client) work
## [2026-08-27] update | Added a "working from a code repo" section to CLAUDE.md (PROJECT_NOTES.md hard link, read one file not the vault)
## [2026-08-27] update | Added a "What does not belong in this vault" section to CLAUDE.md's Don't over-file rules
## [2026-08-27] update | Removed ClickUp from Kelly's contacts; recorded in her Revision History
## [2026-08-27] ingest | Indexed the Claude.ai export (33 conversations) and triaged it; conversations not filed, only extracted
## [2026-08-27] ingest | Created projects/redflagger/overview.md from the 2026-04-22 conversation
## [2026-08-27] ingest | Created projects/mycentimo/overview.md from the 2026-06-30 conversation
## [2026-08-27] update | Corrected research/affiliate-marketing.md: a live affiliate site already exists
## [2026-08-27] update | Corrected projects/portfolio/overview.md: two usable case studies now exist
## [2026-08-27] ingest | Filled personal/job-search/overview.md from the export's Apr-May 2026 job search (targets, channels, comp, drafting rules)
## [2026-08-27] update | Rewrote research/n8n-automation.md: status planned to active, added patterns and five production gotchas
## [2026-08-27] update | Added the productised-product alternative to research/ai-automation-agency.md
## [2026-08-27] ingest | Ingested raw/inbox/Trading/The pre LIT Basic Master Map.pdf into research/trading.md; filed to raw/research/trading/
## [2026-08-27] query | WALANG TITULO BY MB.pdf (88MB, scanned, no OCR tool available) left unprocessed in raw/inbox/Trading/
## [2026-08-27] update | WALANG TITULO BY MB.pdf deleted unread by the human; noted on research/trading.md, inbox now empty
## [2026-08-27] update | Aligned tags between research/n8n-automation.md and research/ai-automation-agency.md (ai-automation -> automation) so both surface under one tag
