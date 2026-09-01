---
kind: meeting-notes
client: kelly
project: avelisse-dictation-app
tags: [kelly, dictation-app, meeting-notes, presentation]
created: 2026-08-31
updated: 2026-08-31
---

# Avelisse Dictation App - Meeting Notes

Call prep and outcomes for [[clients/kelly/dictation-app/overview|Avelisse
Dictation App]]. Newest entry at the bottom.

---

## 2026-09-01, 10:00 GMT - Presentation: last two weeks, Android + iOS only

A walkthrough of the last two weeks of work, what's been seen,
and what I thinks. Scoped to the dictation app only - Android and iOS.

### Open with this question

- "Did you get a chance to try the Android version? What did you think?"

### 1. Android - what I got done

- Every screen now matches the final look you approved - colors, layout, the
  whole visual identity.
- Found and fixed a crash that happened on certain phones. The app was trying
  to use a shortcut some phone chips don't support - traced it to the exact
  phone model and fixed it properly.
- Found and fixed a bug where tapping stop quickly, or twice in a row, could
  get the app stuck instead of finishing the transcription. Can't happen
  anymore.
- Found and fixed a real privacy issue before it ever reached you: the
  released version was quietly saving a copy of everything dictated to a file
  on the phone. That directly contradicted the "private, nothing leaves the
  device" promise from day one. Caught it, fixed it, verified it's gone from
  the version people actually use.
- Fixed the keyboard defaulting to a French layout instead of the standard
  one.
- Went through the entire app and stripped out every trace of the original
  open-source project it was built on - name, look, internal references, all
  of it. It's fully yours now, not a reskin.
- Checked every piece of code and every third-party component this is built on
  for legal safety, so it's clear to sell and distribute under your name.
  Everything checked out clean.
- First testable version went out to you on August 25th.

### 2. iOS - what I got done, and the one real blocker

- Same legal and safety check done there too. One small loose end I'm still
  confirming: the rights on a couple of sound effect files used in the app.
- All the internal documentation rewritten to describe your app, not the
  original project.
- Your final color scheme is fully applied on iOS as well.
- As of this morning, finished switching the app's internal identity over to
  yours too - the same kind of cleanup already done on Android.
- **The blocker:** none of that has actually been turned on yet, because the
  tools that build and finalize an iPhone app only run on Apple's own
  computers, and I don't have one. Everything above is ready and waiting - the
  moment that's solved, iOS can move fast, since the groundwork is already in
  place. Not new - it's the reason Android went first - but it's the one thing
  standing in the way now.

### 3. What's left before each is truly finished

- **Android:** the technical paperwork Google requires to publish under your
  name, then a short test pass, then it's ready for the Play Store.
- **iOS:** just the no-Mac problem. Nothing else moves until that's solved.

### 4. What I need from you

- Your test results on the Android version.
- Final brand name and logo sign-off - still sitting on a placeholder name.
- Confirmation that I actually have access to your Google Play Developer and
  Apple Developer accounts.
- A decision on the iOS building problem: rent access to a Mac in the cloud,
  use an automated cloud build service, use your own Mac when you're settled
  somewhere with power and internet, or buy a low-cost one outright. Your
  call.

### Outcome

*Not yet held - fill in after the call: what she said about the Android alpha,
which iOS option she picked, and anything that changes
[[clients/kelly/dictation-app/overview|the project's status]] or
[[clients/kelly/dictation-app/decisions|its decisions]].*
