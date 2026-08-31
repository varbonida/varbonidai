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
## [2026-08-28] ingest | Created projects/homemadeeasier/ (overview + updates) from the repo's README, package.json, and its one live post
## [2026-08-28] update | Corrected research/affiliate-marketing.md: status planned to active, added Home Made Easier as the second live implementation
## [2026-08-28] update | Added a vault pointer to homemadeeasier/CLAUDE.md (PROJECT_NOTES.md not yet linked)
## [2026-08-28] ingest | Ingested raw/inbox/08-28-2026.md (Claude.ai conversation, Home Made Easier planning) into projects/homemadeeasier/; filed to raw/projects/homemadeeasier/
## [2026-08-28] update | Rewrote projects/homemadeeasier/overview.md with growth strategy, content pillars, architecture, and design direction
## [2026-08-28] ingest | Created projects/homemadeeasier/decisions.md (7 decisions: distribution channel, linking rule, niche/audience, naming, stack choice, feature scope, design mode)
## [2026-08-29] ingest | Added prompts/pinterest-pin-package.md, first entry in a new Marketing category
## [2026-08-29] ingest | Added prompts/tiktok-affiliate-storyboard.md to the Marketing category
## [2026-08-29] ingest | Added prompts/tiktok-affiliate-video-generation.md; cross-linked as stage 2 of the storyboard prompt's pipeline
## [2026-08-29] update | Rewrote prompts/tiktok-affiliate-storyboard.md: single consolidated image instead of two separate outputs, now matching what the video-generation prompt already expected
## [2026-08-31] ingest | Created clients/kelly/dictation-app/meeting-notes.md - presentation prep for the 2026-09-01 call with Kelly, scoped to Android/iOS, plain-language
## [2026-08-31] update | Linked meeting-notes.md from clients/kelly/dictation-app/overview.md's Supporting Files
## [2026-08-31] query | Audited all four PROJECT_NOTES.md hard links: only portfolio/varbonida was real; homemadeeasier, avelisse-android, avelisse-ios were all unlinked plain files
## [2026-08-31] update | Merged homemadeeasier's real drift (GitLab merge conflict fix, "The Exposed Binding" design pass, a sidebar layout bug) into projects/homemadeeasier/updates.md
## [2026-08-31] update | Corrected projects/homemadeeasier/overview.md and decisions.md: design direction is "The Exposed Binding", not the sage/warm-neutral palette named in planning, which was never built
## [2026-08-31] update | Added a caveat to concepts/project-notes-symlink.md: a coding agent falsely claimed to have fixed a broken link; verify with inode comparison, never trust the claim
## [2026-08-31] update | Removed the three fake PROJECT_NOTES.md files so real hard links can be created; mklink needs an elevated prompt, which this session does not have - commands handed to the human
## [2026-08-31] query | Checked avelisse-android/ios repos via git log for undocumented work; found the iOS repo has real work today (2026-08-31) not yet in the vault
## [2026-08-31] update | Recorded the iOS technical identity rebrand (bundle ID, App Group) completed 2026-08-31 in updates-ios.md, overview.md, and meeting-notes.md
## [2026-08-31] query | Confirmed the new mklink attempt on avelisse-android/ios still did not create real hard links (Links: 1 on both sides, not 2); commands handed back to the human
## [2026-08-31] update | Found and merged a duplicate 2026-08-31 heading in updates-ios.md - two separate untracked edits landed once the real hard link was created; kept the more complete/accurate version
## [2026-08-31] update | Added URL scheme, Xcode project rename, and the "Dictus" file/display names still untouched to overview.md's iOS checklist
## [2026-08-31] query | Confirmed avelisse-android and avelisse-ios PROJECT_NOTES.md are now genuine hard links (matching inode, link count 2 on both sides)
