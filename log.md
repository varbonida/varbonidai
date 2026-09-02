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
## [2026-08-31] update | Rewrote meeting-notes.md presentation content in first person, as Vergel speaking directly to Kelly
## [2026-08-31] query | Verified the iOS Mediterranean Coastal color claim against the actual git diff (DictusColors.swift, 2026-08-25) - real, hex values match DESIGN.md exactly
## [2026-08-31] update | Reverted meeting-notes.md to bulleted format, kept first-person voice
## [2026-08-31] update | Optimized prompts/pinterest-pin-package.md for buyer keywords (purchase-intent phrases) across title, description, board name, and hashtags; added optional star rating / Amazon's Choice inputs that surface as trust-signal badges in the image prompt when supplied
## [2026-08-31] update | Fixed a content-policy trigger in prompts/pinterest-pin-package.md: the Amazon's Choice badge instruction asked image generators to reproduce a real trademark; redirected to an original generic badge design
## [2026-08-31] ingest | Created concepts/client-safe-copy.md documenting the redaction rules and on-request sync workflow for kelly/
## [2026-08-31] update | Linked the client-safe copy from clients/kelly/overview.md
## [2026-08-31] decision | Client-safe copies sync on request only, never automatically - redaction requires judgment a script can't safely replicate
## [2026-09-01] ingest | Created clients/kelly/daily-updates.md - client-facing, plain-English daily log, no redaction needed
## [2026-09-01] ingest | Created clients/kelly/communications.md - internal log of what Kelly herself says, never shared with her
## [2026-09-01] update | Linked both from clients/kelly/overview.md's new Supporting Files section
## [2026-09-01] update | Documented both file patterns in concepts/client-safe-copy.md - one syncs as-is, one must never sync
## [2026-09-01] update | Set daily-updates.md's format: What I did today / What I'll work on next / Blockers, per-day
## [2026-09-01] ingest | Backfilled daily-updates.md with 2026-08-25 and 2026-08-31 (only two days with real dictation-app work in the last week); 2026-08-26 to 2026-08-30 skipped per the file's own no-padding rule
## [2026-09-01] update | Synced kelly/: added daily-updates.md (stripped internal sync-workflow references) and a new overview.md Updates link; communications.md deliberately excluded, confirmed zero footprint in the copy
## [2026-09-01] decision | Communications Log made client-facing at explicit request; reworded away from "internal, she'll never see this" framing before syncing
## [2026-09-01] update | Corrected concepts/client-safe-copy.md: visibility of a communications-style log is a per-file, per-client decision, not a fixed rule
## [2026-09-01] update | Synced kelly/communications.md and linked it from kelly/overview.md
## [2026-09-01] decision | Communications Log is now genuinely two-way - Kelly can write directly into her copy on GitHub, not just Vergel logging what she says
## [2026-09-01] update | Added step-by-step GitHub edit instructions to kelly/communications.md for a non-technical writer
## [2026-09-01] update | Added a mandatory pull-before-sync step to concepts/client-safe-copy.md now that a file in the copy can be edited from the client's side
## [2026-09-01] update | Removed "Vergel writes summaries here" framing from communications.md (both copies) - it's Kelly's space only, not a shared/mixed log
## [2026-09-01] update | Corrected communications.md framing again: it's a shared space either side writes into, not Kelly-exclusive - "own space" was an overcorrection
## [2026-09-01] update | Synced kelly/: confirmed no remote changes to pull, verified communications.md/daily-updates.md/overview.md already match the vault's latest wording, fixed a stale frontmatter date
## [2026-09-02] update | Added 2026-09-02 entry to daily-updates.md: Live Activity re-theme and the iOS source-level rename, translated to plain English
## [2026-09-02] update | Updated dictation-app/overview.md's iOS checklist: Live Activity re-theme and app-name/reference replacement both marked done, with the three deliberate exceptions noted
## [2026-09-01] ingest | Pulled Kelly's first direct write into communications.md: a full chronic-patient requirements document for the Android app, a workflow/UX question, and a separate Handy bug investigation request
## [2026-09-01] major-change | Dictation app scope expanded from "Kelly's private tool" to an explicit chronic-illness-patient product - added full "Chronic Patient Requirements (Android)" section to dictation-app/overview.md
## [2026-09-01] ingest | Created clients/kelly/handy-preroll-bug/overview.md (new planned project) from Kelly's own request
## [2026-09-01] update | Connected chronic-patient-audience/overview.md to the dictation app - the product now exists that the audience research was missing
## [2026-09-01] query | Three items now await Vergel's direct response: a firm ship date, per-section time estimates, and Kelly's own question about restructuring the communications log to one file per day
## [2026-09-02] update | Synced kelly/: pushed dictation-app/overview.md, chronic-patient-audience/overview.md, handy-preroll-bug/overview.md, and the overview.md backlog entry; re-applied the "Compliance and reputational considerations" redaction that a raw push had reverted; left her own communications.md entry untouched, not overwritten with the vault's annotated version
## [2026-09-01] decision | Restructured communications from a single accumulating file into a folder of dated, titled notes (YYYY-MM-DD - Title.md), directly answering Kelly's own request
## [2026-09-01] update | Migrated communications.md content into clients/kelly/communications/2026-09-01 - Specs for the App.md and created communications/index.md; old file removed
## [2026-09-01] update | Rewrote all cross-references (dictation-app, handy-preroll-bug, client overview, concepts/client-safe-copy) to point at the new folder structure
## [2026-09-01] update | Applied the same restructuring to kelly/: her raw entry preserved verbatim in the new location, old communications.md turned into a redirect stub rather than deleted
## [2026-09-01] query | Realized from Kelly's own message ("I LOVE this Obsidian") that she's using the Obsidian app directly, not GitHub's web editor - rewrote the "how to add a note" instructions in her copy to match, dropping the GitHub-pencil-icon steps
## [2026-09-02] decision | Restructured daily-updates from a single accumulating file into one note per week, Wednesday through Tuesday
## [2026-09-02] update | Split existing entries into three weekly files (2026-08-19 to 25, 2026-08-26 to 09-01, 2026-09-02 to 09-08) plus an index; old daily-updates.md removed
## [2026-09-02] update | Applied the same restructuring to kelly/; left a redirect stub in place of the old file since Kelly specifically praised "the daily notes" in her message
## [2026-09-02] update | Logged the Obsidian communications/daily-updates restructure itself in this week's daily-updates entry, plain English, both vault and kelly/ copy
## [2026-09-02] update | Found additional real iOS work in updates-ios.md not yet synced: swipe-back overlay re-themed (last flagged screen), old Dictus palette fully retired, two dead links killed
## [2026-09-02] update | Updated dictation-app/overview.md checklist and daily-updates entry to reflect the swipe-back overlay completion; app icon flagged as the one remaining holdout, needing a design decision not a code fix
## [2026-09-02] update | Synced updates-ios.md, dictation-app/overview.md, and this week's daily-updates entry to kelly/; verified no redaction reversion and all links resolve
## [2026-09-02] update | Pulled Vergel's reply to Kelly's spec doc (written directly in kelly/communications) into the vault's copy of the same file
## [2026-09-02] update | Extracted the reply's durable answers into dictation-app/overview.md: firm ship date (2026-10-23), per-section estimates, and four scope clarifications found while estimating (offline correction instead of pre-loading, personal dictionary is new work, SNOMED redistribution risk, auto-title means trimmed opening line not a summary) plus two bugs found in section 3 (2-minute transcription cap, audio held in memory instead of storage)
## [2026-09-02] update | Pushed the same dictation-app/overview.md changes to kelly/ - all client-facing, no redaction needed
