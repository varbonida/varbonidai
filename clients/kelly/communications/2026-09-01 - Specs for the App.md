---
kind: communications-entry
client: kelly
tags: [kelly, communications]
created: 2026-09-01
updated: 2026-09-02
---

# 2026-09-01 - Specs for the App

Written by Kelly, her title suggestion. See
[[clients/kelly/communications/index|Communications]] for the full list.

**Workflow question, asked first:** whether she should be creating a new
file/folder per communication rather than writing into a shared file, how
she's notified of a communication, and a stated preference for one file per
day under communications, each labeled with a date and a descriptive title
(e.g. "Specs for the app") rather than the single accumulating file this
started as. **Answered 2026-09-01** - this folder structure is that answer.

**Then, a full requirements document for the Android app - copied verbatim:**

> I really need you to do a note every single day. It's for me more than you,
> but I do think it will help get us on the same page.
>
> On the apps. First, something you need to know before we submit anything.
> The App Store will reject an app that is just a rebrand of a known app. So
> will Google, though they're softer about it. We have to add real value, and
> it has to show both in the app and in the store description. That's not a
> criticism of where we are. The fork was my decision and it was the right
> one. It just means the next stretch of work is the part that makes it ours.
>
> So here's what I want the Android app to become.
>
> **The people we're building for**
>
> This matters more than any feature, so let me set it up.
>
> A chronic patient lives with something for months or years. Then they get a
> twelve minute appointment, and they're supposed to remember what happened
> across all those weeks. Nobody can, so they say "it's been about the same,"
> and the doctor gets nothing useful out of them. Then they walk out and
> forget half of what was just said before they reach the car.
>
> That's the problem. We will partially solve the problem with a dictation
> app that has additional features and big buttons, etc.
>
> These people also often can't type well. Dry mouth from medication,
> breathlessness, tremor, fatigue, brain fog. They lose the thread
> mid-sentence. Every general dictation app punishes all of that.
>
> **1. Medical words, loaded in advance**
>
> Right now the recognizer mangles medical terms, and that alone would make
> people quit. The fix for that is to insert 2 free lists of medically
> related words. Let me know if there is any issue with this. The two lists
> are:
>
> RxNorm, from the US National Library of Medicine. Free, immediate download.
> Drug names, brand and generic, with the mapping between them, so Plaquenil
> and hydroxychloroquine both come out right.
>
> SNOMED CT, for diagnoses, symptoms and procedures. Free in Germany and the
> US, but it needs a license registration first and the account can take a
> day or two to come through. Start that registration today so it isn't
> holding anything up later.
>
> Past those two, let the users build their own list of frequently misspelled
> words. Dictus already has a personal dictionary, so make it easy to find
> and easy to add to (we will add a description in the instructions/app
> description). When somebody's medication comes out wrong, they fix it once
> and it sticks. They know what they say better than I could guess.
>
> **2. Two places to talk**
>
> We will have 2 big buttons for 2 logs that will make this app super
> helpful. Not forms, fields, typing, and no decisions to make. Two buttons
> that each open a page that they speak into and the app labels the dictation
> with the date and files it on their phone.
>
> _Symptom log._ For whenever something happens. A bad night, a new pain, a
> medication that made them feel strange. Open the app, one button, talk.
> They can ramble. When they stop, the app dates it, titles it, files it.
> That's the entire interaction, because on a bad day anything more is the
> reason somebody closes the app and doesn't come back.
>
> _Post-visit capture._ For the five minutes after an appointment, sitting in
> the car, while it's still fresh. What was said, what got prescribed, what
> to do next, what they forgot to ask. Same thing: one button, talk, done.
>
> Both save on the phone. Add an export button so someone can send themselves
> a copy if they want it, but that's their choice, never automatic.
>
> They need to be able to browse past entries by date and search them.
>
> **3. Speech that forgives**
>
> No timeouts anywhere. Not on recording or on the app. Somebody pauses for
> thirty seconds because they lost the thread, and they must not lose what
> they already said. This is the single thing that will make people choose
> us over a free keyboard.
>
> **4. Built for bad hands and no energy**
>
> Every control large. Usable one-handed. Usable lying down. This is an
> assistive app and it should be designed that way from the start, not
> adjusted afterward.
>
> **5. Nothing leaves the phone**
>
> No cloud, no server, no account, ever. Don't add anything that sends audio
> or text off the device.
>
> We discussed this before: this is not a HIPAA compliant app and we're not
> claiming it is. But I want HIPAA on your mind the whole time you build,
> because our users are handling exactly the kind of information HIPAA exists
> to protect, and they'll expect us to treat it that way whether the law
> requires it or not. Further, when problems happen, the bureaucrats will
> always default to investigation.
>
> Everything staying local means there's nothing to breach and nothing to
> explain. It's also what we're selling: your symptoms never leave your hand.
> I don't want to trade that away later for a convenient feature.
>
> **What I need back from you**
>
> Two things, before you start building.
>
> First, a date. Not a range, not "about two weeks," not "should be." One
> date, from you, on which this app is finished, tested, and ready to upload
> to Google Play. Pick it yourself, and pick one you can hit, because once
> you give it to me I'm going to hold you to it. If something goes wrong
> along the way, tell me the day it goes wrong, not the day before the
> deadline.
>
> Second, go through the five numbered sections and tell me roughly how many
> days each will take, and which is hardest and why.
>
> If anything in here is unclear, or you think I've asked for the wrong
> thing, say so now rather than building it anyway. I would much rather be
> argued with than quietly disagreed with.
>
> Then, as we get closer, I'll want three things written up: a technical
> description of the app (what it is, how it's built, every tool used in the
> build); a user description, detailed and genuinely inviting for a chronic
> patient, written for someone tired and unwell who's deciding whether this
> is worth their energy; and a step by step plan for getting it onto Google
> Play.
>
> One last thing. I know I haven't been clear enough with you up to now about
> what I actually want, and that's on me, not you. This document is my
> attempt to fix that. Tell me if it works better.
>
> Kelly
>
> **PS.** Separate job, next week, not part of the above. The dictation app I
> use on my Mac, Handy, has a pre-roll buffer problem: it grabs audio from
> before I press the button and carries fragments between sessions. I've had
> words from a video playing in the background land inside my transcript.
> For a normal keyboard that's annoying. For an app holding somebody's
> medical notes it would be a privacy defect, so I want to understand it
> before it turns up in ours. Other people are working on this same bug
> publicly, so if you find a solution out there, use it. I don't need you to
> invent one. I need you to understand it well enough to explain to me in
> plain English what it does.

**Extracted to canonical pages:** the Android requirements above are now in
[[clients/kelly/dictation-app/overview|the dictation app's requirements]]; the
Handy bug investigation has its own page at
[[clients/kelly/handy-preroll-bug/overview|Handy Pre-Roll Buffer Bug]].

---

# Reply - 2026-09-02

Wed, Sept 2, 2026
Vergel

Hello Kelly.

Yes, Obsidian is good. I've moved communications into its own folder, so from
there you can add a new note per day or per title. Daily updates got the same
treatment, one note per week.

I'll keep updating the vault. Tell me if there's anything you want added to
it.

## The date

**Friday, 23 October 2026.** Finished, tested, and ready to upload to Google
Play. That excludes Google's own review queue.

There are 37 working days between tomorrow and the 23rd. The five sections
add up to 31 to 39 days. The date sits in the middle of that, so it isn't
padded.

I'll tell you the day something slips.

## How the time breaks down

| Section                                         | Days     |
| ----------------------------------------------- | -------- |
| 1. Medical words                                | 10 to 14 |
| 2. Two places to talk                           | 6 to 8   |
| 3. Speech that forgives                         | 3 to 4   |
| 4. Bad hands and no energy                      | 4 to 5   |
| 5. Nothing leaves the phone                     | 1        |
| Putting it together and testing on real phones  | 4        |
| Google Play preparation and the three write-ups | 3        |

Section 1 is the hardest and holds roughly two thirds of the risk. If I bring
you bad news it will be about that section, in the first three weeks rather
than the last.

## Section 1: medical words

**10 to 14 days. The hardest of the five.** Three things here - the two
lists, the licence, and the personal dictionary.

### The lists work, "loaded in advance" doesn't

Both lists are free and we can use them. But offline speech recognition has
nowhere to put a word list. Handing the engine a vocabulary before you talk
is a cloud feature. Google and Amazon offer it, the offline engines don't.
The closest one of ours gets holds a few hundred words. RxNorm has over a
hundred thousand.

So the words go in after. The person talks, the engine makes its best guess,
then the app checks that guess against the medical lists and repairs anything
close but wrong. "plaquinil" becomes "Plaquenil". "hydroxy chloroquine"
becomes "hydroxychloroquine". RxNorm carries the brand and generic mapping,
so we get that for free. Same result for the person, and I can tune how
aggressive the repair is.

It's the hardest section because checking every word against a hundred
thousand medical terms, fast enough that nobody notices, on a cheap phone, is
the one piece here I haven't built before. Either it works in three days or
it eats a week.

### The personal dictionary is the wrong one

The one in the app belongs to the keyboard, not the dictation. It watches
what you type and pushes your common words up the suggestion strip. No
connection to speech, and it can't be pointed at one.

What you described - medication comes out wrong, they fix it once, it sticks
- is new. A list where you tap the wrong word in a transcript and say what it
should have been. Cheap once the repair step above exists, since it's the
same machinery with their own words in it. Costed as new, not as switching
something on.

### SNOMED's licence

The account delay is the small problem. I'll start both registrations this
week.

The bigger one: permission to download and use SNOMED isn't the same as
permission to ship parts of it inside an app on Google Play, to people in
countries the licence doesn't cover. Separate clauses, and I won't guess at
them. Send me the licence text when it arrives, not just confirmation that
the account is open.

I also suspect RxNorm needs a free account rather than an instant download.
Your note says immediate. I'll verify.

If SNOMED hasn't cleared by **20 September**, we ship on the 23rd with RxNorm
and the personal corrections, and SNOMED follows. Adding it later will mean
swapping in a file. That protects the date.

## Section 2: two places to talk

**6 to 8 days.** Two buttons, talk, done. No disagreement.

It's that long because the app can't store anything today. No list of past
entries, no search, no export - it types into other apps and forgets. All of
that is new.

One caveat on "dates it, titles it, files it." Dating and filing are simple.
Titling isn't. Summarising an entry needs the kind of language model that
runs in a data centre, and putting one on the phone breaks rule 5. So the
title is the opening line of what they said, trimmed, with the date beside
it. Not a summary.

## Section 3: speech that forgives

**3 to 4 days.** Most of this is already done. Recording has no time limit
and no cutoff for silence. A thirty second pause loses nothing. Android won't
shut it down when the screen goes dark. I checked that in the code today.

Two things to fix.

A two minute cap on turning audio into text after they stop talking. An older
phone with a long recording will hit it. Easy to remove.

The app holds the whole recording in the phone's working memory. Half an hour
of audio is about 115 megabytes. Much past that and Android shuts the app
down and the person loses everything they said. Not in your list, but it's
the exact failure this section is meant to prevent. The fix is writing audio
to storage as it arrives, and it's most of the three to four days.

## Section 4: bad hands and no energy

**4 to 5 days**, most of it on the screens that already exist rather than the
new ones. Agreed, and cheaper this way than retrofitting.

Taking "usable lying down" as part of the same idea as the other two lines:
no standing, no sitting up, no second hand. Large controls, everything in
reach of one thumb, nothing needing a steady grip or a precise tap.

## Section 5: nothing leaves the phone

**1 day.** The app already works this way - no server, no account, nothing
that sends audio or text anywhere. The day is auditing that rather than
assuming it, and writing the privacy claim so it's both true and defensible.

I'll treat it as a rule that can't be traded, including when a later feature
would be easier with a server behind it. If that comes up you'll hear it as a
question, not as something I already did.

## What I need from you

1. **The RxNorm and SNOMED registrations.** It's the only item on this
   list that can move the date.

Vergel

**Extracted to canonical pages:** the ship date, per-section estimates, and
the technical caveats above (offline correction instead of pre-loading, the
personal dictionary being new work, the SNOMED redistribution-licence risk,
the two bugs found in section 3) are now recorded on
[[clients/kelly/dictation-app/overview|the dictation app page]].
