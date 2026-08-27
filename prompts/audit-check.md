---
kind: prompt
category: coding
tags: [audit, licensing, open-source, rebrand, compliance]
created: 2026-08-22
updated: 2026-08-27
---

# Audit Check

Audits a repository before rebranding it and shipping it commercially. Covers
project license, dependency licenses, AI model licenses, privacy and telemetry,
hardcoded secrets, and leftover upstream branding. Read-only: it is told not to
modify anything except the audit file it writes.

Used for both the Android and iOS passes on
[[clients/kelly/dictation-app/overview|Avelisse Dictation App]]. Set
`<AUDIT_OUTPUT_PATH>` before running it.

```You are auditing this repository before I rebrand and commercially distribute it.

This is an AUDIT ONLY.

**Do not modify any existing project files, install/update dependencies, rename anything, or make commits.**

Analyze the repository and save the complete audit report to:

`<AUDIT_OUTPUT_PATH>`

(Fill in per use. For Kelly, that is `clients/kelly/dictation-app/audits/<platform>-audit.md` inside this vault.)

The only file you may create/modify is that audit file.

Check:

1. **Project license**
    
    - Main license and copyright holder.
        
    - Whether commercial use, modification, and redistribution are allowed.
        
    - Required copyright/license notices.
        
2. **Dependencies**
    
    - Inspect Gradle/version catalogs.
        
    - Identify important dependencies and their licenses.
        
    - Commercial-use/redistribution restrictions.
        
    - Attribution/NOTICE requirements.
        
    - Flag unknown or risky licenses.
        
    - Pay special attention to native and AI/speech components.
        
3. **AI models**
    
    - Identify all bundled/downloaded models and model files.
        
    - Check model licenses separately from library licenses.
        
    - Flag restrictions on commercial use or redistribution.
        
4. **Third-party code/assets**
    
    - Find vendored/copied code, fonts, icons, images, or other assets with separate licenses.
        
    - Flag attribution or commercial restrictions.
        
5. **Privacy/security**
    
    - Check permissions, network access, analytics, telemetry, crash reporting, APIs, model downloads, and logging.
        
    - Pay special attention because this is an Android keyboard handling potentially sensitive text/audio.
        
    - Verify whether privacy claims such as "no telemetry" and "on-device processing" are supported by the code.
        
6. **Branding**
    
    - Find Dictus/PIVI references, package/application IDs, domains, URLs, logos, and other branding.
        
    - Distinguish branding that should be replaced from legally required attribution/license notices that must remain.
        
7. **Commercial/Google Play concerns**
    
    - Identify anything I should resolve before publishing a paid/rebranded version.
        
    - Flag issues to verify rather than claiming legal or Google Play compliance.
        
8. **Final action list**
    

Keep the report concise and repository-specific.

Use these sections:

### 🟢 Safe

Things that appear safe to do.

### 🟡 Check

Things requiring further investigation.

### 🔴 Blockers

Potential commercial-distribution blockers.

### Before Rebranding

Prioritized actions I should resolve first.

### Files to Preserve

License, NOTICE, attribution, or other files I should retain.

### Dependency Summary

Concise table of important dependencies and licenses.

### AI/Model Summary

Concise table of AI libraries/models and their licensing status.

Do not explain obvious Android concepts.

Do not modify source/configuration files.

At the end of the audit file state:

`Source files modified: 0`  
`Audit saved: Android Audit.md`

After saving the audit, give me only a short summary of the most important findings.
```
