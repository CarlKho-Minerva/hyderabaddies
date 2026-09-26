# Packet verification — run ~23:20–23:50 PDT, Sep 25 2026

Run by a follow-on agent (pi/Claude) after the Codex thread died at the usage limit with "I'm checking the final packet now." This is that check. Nothing below is claimed that was not actually run; commands and sources are named.

## Summary

| Check | Result |
|---|---|
| Internal links / file paths in `00` and `03` | **14 local links, 14 resolve. 0 broken.** (`01` and `02` also scanned: 0 local links, 23 external URLs, not fetched.) |
| Logistics claims in `00` §3 vs `work/event.txt` | **All 7 load-bearing claims grounded** in the Day 1 deck text. 0 rest on a screenshot alone. |
| Ten council rounds present and complete in `04` | **10/10 present, each byte-identical to its `council/round-NN.md`, none truncated, all required sections present.** |
| Fictional-critique labelling | Every round labels itself fictional (14–31 "fiction*" mentions per file); no real judge name is ever used as a speaker. |
| Work-authorization / employment language | 0 hits for work-authoriz*, EAD, OPT, I-765, "employed" across `outputs/`. |
| Messages to humans | One Slack DM was **already sent by Codex at 22:49:33 PDT** (verified from the permalink timestamp), disclosed in `00` §1 and `01`. No other message was sent, drafted-and-sent, or scheduled. Nothing was sent by this pass. |
| Fixes made | 3 (listed below). |
| Unverified / open | 6 items (listed below). |
| Wrong (found and corrected) | 1 factual error: teammate name. |

## 1. Link integrity — what was run

`grep -oE '\]\([^)]+\)'` over `00`, `01`, `02`, `03`; each non-http path tested with `[ -e ]`.

- `00-start-here.md`: 3 local links (`01`, `02`, `03`) — all exist. 1 external (Slack permalink) — not fetched.
- `03-council-index.md`: 11 local links (`council/round-01..10.md`, `04-full-council-transcripts.md`) — all exist.
- `04` header links back to `03` — exists.
- Bare-path mentions (`work/`, `outputs/council/round-10.md`, `outputs/02-research-and-demo-options.md` inside transcripts) all correspond to real files.
- Source PDF path quoted in `02` (`/private/tmp/hyderabaddies/attachments/InnovationCup2026_Day1_Slide.pdf`) — exists (4.6 MB, Sep 25 19:51), alongside `PreEvent_Material_JP.pdf`, `hackathon_template.pptx`, `team_gcp_assignments.tsv`. Note `/private/tmp` does not survive a reboot.

**Count: 14 local links checked, 0 fixed.**

## 2. Logistics fact-check — `00` §3 against `work/event.txt`

`work/event.txt` is the text extraction of the Day 1 deck. The PNGs in `work/` were **not** read (no image lane used); nothing below relies on them.

| Claim in `00` | Source | Status |
|---|---|---|
| Sunday submission 11:00 AM | event.txt p17 "Deadline: 11:00 AM PDT, Sunday, September 27" | Verified |
| Public repo + PDF deck + demo/video ≤ 90 s | p17 items 1–3: public GitHub repo; "demo or a video of the prototype (Up to 1.5 minutes)"; deck ".pdf" | Verified. Note it is "demo **or** video" — a live demo link satisfies item 2. |
| Prelim 3 min + 90 s Q&A | p18 "3 minutes presentation + 1.5 minutes Q&A" | Verified |
| Final 6 + 6 | p19 "6 minutes presentation + 6 minutes Q&A" | Verified |
| Saturday lunch/mentoring 12:30–2:30 PM | p7/p8 "12:30 - 2:30 PM Lunch / Mentoring Session" | Verified |
| Saturday evening session 5–6 PM | p7/p8 "5:00 - 6:00 PM Mentoring Session" | Verified |
| "Not a documented rotation through industries" | p7–9 list only gather / lunch-mentoring / work / mentoring / announcements | Verified (absence of any such item) |
| 40/30/30 rubric | p14 | Verified |
| "Prepare both before submission" | Inference from p19 "No setup time after the prelim results" | Reasonable inference, labelled as such in `05` |
| "Don't reuse AI ideas as-is" | p27 | Verified |
| Slack request "at 10:49 PM" | Permalink `p1790401773440139` → epoch 1790401773 → 2026-09-25 22:49:33 PDT | Verified (timestamp only; message content not re-read) |

Additional facts in `02` cross-checked: prelim order announced 6:30 PM Day 2 (p18) ✓; tech support 10–11 AM and 8–9 PM (p9) ✓; Hiro reservation thread Friday 7 PM, Golden Gates 1F; walk-in at Amazing Grace 1F (p8) ✓; midnight–6 AM hotel-only (p7, p29) ✓; prizes $20k + conditional $30k, two $10k special awards (pp21–22) ✓; submission channel `#announcements-all` (p17) ✓.

**Discrepancy worth knowing:** `work/preevent-jp.txt` (pre-event Japanese PDF) has a *different* Saturday: lunch 12:30–13:30, optional mentoring 13:30–14:30, work 14:30–18:30, announcements 18:30–18:40; and lists the submission as a "working demo" (動作するデモ) rather than "demo or video". The Day 1 deck is the newer document and the packet follows it. Flagged in `05`; a Slack announcement would override both.

## 3. Council transcript completeness

Method: (a) `grep '^# '` on `04` → 10 round headings, ROUND 01…ROUND 10, plus the file header. (b) Python substring test: each `council/round-NN.md` (stripped) appears verbatim inside `04` — **10/10 True**. (c) Sizes: concatenated rounds 334,958 bytes vs `04` 335,521 bytes; the 563-byte difference is `04`'s header + link back to `03`. (d) Each round's last H2 is a closing section (revision/reversal, rehearsal check, or saved-file check), not a mid-body section. (e) One `vertex.py` call (gemini-3.8-flash, tag `recruit-packet`, 69,094 tokens in, $0.024, logged in `~/.local/state/lifeos/vertex_ledger.jsonl` at 23:38:12) audited every round for nine required sections — prelim script, prelim Q&A, final script, final Q&A, 90 s storyboard, four-lens deliberation, score table, truth table, reversal conditions — and returned Y on all 90 cells and "ends cleanly: Y" on all ten. Vertex's negative findings (no real judge as speaker, no employment language) were independently re-checked with grep, below.

The ten rounds, by title and stated direction:

| # | Title | Direction the round itself states |
|---|---|---|
| 01 | baseline comparative council | C, narrowed to one incident |
| 02 | Buyer skepticism, revision 2.0 | C for exploration; A for discovery |
| 03 | Incumbents and disconfirmation | A rehearsed; C concept lead |
| 04 | worker agency, consent and bias | C conditional, learner-owned |
| 05 | No enterprise data, no mentor author, one build day | C as fictional mechanism only |
| 06 | Can the judge actually change the experiment? | B |
| 07 | the magic must survive the missing model | C conditional |
| 08 | Two people, one day | C narrowly, one scene |
| 09 | Who benefits when this crosses an industry boundary? | C-onboarding narrowly; B if no approved case |
| 10 | final head-to-head rehearsal | C, careers-program buyer, exploratory artifact |

This matches the table in `03`. **None truncated.**

Labelling: `grep` for the four real judge names used as a dialogue speaker (`^Name:` / `**Name**`) → 0 hits in `04` and `council/`. The names appear only in evidence-boundary lines citing public backgrounds (lines 1541, 2391 of `04`, and the `02` judges section). Every round file contains "fictional" labelling (counts 14–31 per file).

## 4. Fixes made (3)

1. **`02-research-and-demo-options.md` line 157: "Carl and Stephen" → "Carl and Steven."** Teammate is Steven Yang per the organizer file `team_gcp_assignments.tsv` (team `recruit-hackathon-2026-e`) and every other packet file. Same fix applied to the source line in `work/judges-research.md` line 16.
2. **`00-start-here.md`:** added a 5-line overnight close-out banner at the top pointing to `05` and this file, and naming the one thing only Carl can do (read the Shion DM). No other text in `00` changed.
3. **Created `05-saturday-runsheet.md`** — organizer times only from `event.txt`; suggested rows explicitly labelled; decision gate at 2:30 PM; Saturday-night artifact list.

## 5. Unverified / open (6)

1. **Whether Shion replied to the 22:49 DM.** Not checked. The only local Slack helper (`hackathon-brain/slack_session.py`) scrapes Carl's live browser session; not used while he sleeps. Carl opens the DM.
2. **Whether anyone replied to Hiro's 7:00 PM booking thread** for a Saturday mentoring slot. Not checked, same reason.
3. **Ebina-san's title.** `00` calls him "the VP"; `01` sources this to his LinkedIn page (external URL, not fetched tonight). The Day 1 deck (p4) lists Hidetoshi Ebina under Organizing Team with no title. Treat "VP" as LinkedIn-sourced.
4. **Template section order and word caps** quoted in `02` and repeated in `05` come from Codex's read of `hackathon_template.pptx`. The .pptx exists; its contents were not re-inspected tonight.
5. **The rules/schedule PNGs** in `work/` were not read. Every logistics claim was grounded in `event.txt` text instead, so no claim rests on a screenshot alone. If a PNG contradicts the text extraction, the PNG is the original.
6. **The 23 external URLs** in `01` and `02` (judge bios, MHLW survey, Forage, Delphi, Granola, Observable Intuition terms) were not re-fetched. Their claims stand as Codex's Sep 25 research, not re-verified.

## 6. Wrong (1)

- Teammate name "Stephen" in `02`/`work/judges-research.md`. Corrected (above). No other factual error found in the checked claims.

## 7. Not done, deliberately

- No message drafted, sent, or scheduled to anyone. The 22:49 DM was already out before this pass and is disclosed in `00`, `01` and `05`.
- No code, repo, deck, video, calendar event, or submission created. Those are Carl and Steven's, written after Friday's opening ceremony.
- Council content was not edited. It stays labelled fictional; `04` and `council/` are byte-identical to what Codex left.
- No Vertex call beyond the single audit above.
