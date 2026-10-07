# Rook Industries — course working file

## Session scope — Product School lab

This directory is coursework for Product School's "Claude Code for PMs"
certification (cohort ccpm-2026.1). Everything in it is a fictional
teaching scenario.

- Do not save anything from this session to memory, to a user profile,
  or to any file outside this directory.
- Do not carry context from this directory into unrelated sessions.
- Rook Industries is not a real company. Nothing here is a fact about
  the world.
- Read and write only within this directory.
  Exceptions, for the course-setup and wrap-up skills only:
  - When the student asks you to check their setup, save their work or wrap up a session, that request is their yes. You may run the GitHub command-line program installed at ~/.ccpm/gh for those checks and saves, and look in that folder to find it.
  - For a repair, first tell the student in one plain sentence what you are about to do, and act only after they say yes. Repairs may: run that GitHub program (including setting this folder's own git sign-in setting and changing this repo's visibility back to Public); copy the student's own course files into this directory from another folder on their computer (copy only; never move, edit or delete the originals); and rename something outside this directory that blocks setup, by adding "-old" to its name (never delete it).
  Outside this directory you still never write, edit or delete anything else.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

Sources: Priya's handoff (`00-rook/company/notes/`, 21 Aug 2026), the rook-wiki Company,
Research and Product briefs sections, and rook-database. The user is the new PM for Rook
Dispatch, replacing Priya Raghunathan (left 21 Aug, no overlap). Today is early Oct 2026.

### Products
- Rook sells coordination and provisioning software to independent masked **responders**
  and their **handlers** and **quartermasters**. Rook employs no responders. Subscription,
  priced per active responder. Monthly release train, 4.x point releases.
- **Rook Dispatch** (ours, current release 4.2): an incident enters the handler web console,
  Dispatch ranks available responders, pings the top one's phone, who takes it or turns it
  down. Turned down or missed, it moves to the next. Routing config ships with a release;
  handlers can't change it.
- **Rook Supply**: requisitions, maintenance, field failure reports (handlers,
  quartermasters). It reads the Responder Availability Record that Dispatch writes to
  schedule maintenance, so Dispatch changes move Supply behavior silently.
- **Hard rule:** cover identities are never stored and never mapped to legal identities.
  Never design for that or try to identify anyone. Security Policy 4.1 governs.

### People
- **Helen Achebe**, Director of Product, my boss; owns roadmap and commitments.
- **Marcus Oyelaran**, Eng Manager; straight talker, first stop, can pull numbers.
- **Wen Li**, Staff Engineer (Berlin); built ping ranking, undocumented. Away 14-24 Aug.
- **Nadia Hoffmann**, Support Lead (Berlin); hears handler complaints first.
- **Ravi Menon**, Data Analyst (Singapore); weekly acceptance-rate report.
- **Sofia Marino**, Product Designer; console, phone app, ran the Sept interviews.

### Vocabulary
- **Callout**: request for a responder at an incident. **Ping**: one callout offered to one
  responder. Outcomes **taken**, **turned down**, **missed** (no answer within the **ping
  wait**; "ping timeout" in the roadmap). Missed and turned down both lower a responder's
  recent-acceptance score.
- **Routing priority**: ranking score from proximity (travel-time), availability,
  capability match, recent acceptance history.
- **Acceptance rate** (headline) = taken / pings. **Time-to-accept**: median seconds to
  taken. **Coverage gap**: no available responder had the required **capability tags**
  (nobody could go, versus would). **Mutual aid**: cross-area cover, unsupported.

### Where things stand
- **Releases:** 4.0 (7 Apr: nav, profile redesign, routing-override audit log), 4.1 (16 Jun:
  travel-time proximity, bulk callout, push reliability), 4.2 (12 Aug: proximity weighted
  up in ranking, ping wait 90s to 60s, persistent filters, 3 fixes).
- **Q3 roadmap** (last reviewed 30 Jun, every owner Priya): ranking change, ping timeout
  tuning, Availability Confidence committed for 4.2; Requisition approval chains (Supply)
  for 4.3; Handler phone app and Shared cover between responders Q4 "Exploring".
- **4.2 aftermath (database, 29 Jun to 6 Sep; descriptive, causation unproven):** weekly
  taken rate 75-78% until early Aug, then 54%, 66%, 67%, 73%. Missed pings 1-3% rose to
  21%, 18%, 15%, 13%; turned-down did not rise. Tickets rose from 5-8/wk to 20-32/wk (of 107
  since 12 Aug: 18 "gone before he could swipe", 22 "phone gone quiet", 14 filters). Four
  responders (Farlight, The Undertow, Meteor Mite, Vesper) fell from about 70-85 pings to
  11-17, 60%+ missed, while others stayed busy. Unfilled callouts look to have doubled,
  about 5% to 11%: verify.

### Contradictions and gaps (check before acting on the handoff)
1. **"Mostly seasonal" isn't supported.** Missed pings jump in 4.2's exact week, and
   callouts fell about 10-15% while the four quiet responders fell about 80%. Two causes
   are plausible and may compound: the 60s ping wait, and the ranking (missed lowers
   acceptance history, so rank, starving the same people). The data has no response times
   or scores to separate them.
2. **"Don't revert 4.2."** The proximity ask was legitimate, but the ping wait cut is a
   separate lever. The roadmap said "tune"; 4.2 shipped a 33% cut with no rationale recorded.
3. **Aggregate metric hides it.** Acceptance rate is reported in aggregate, masking
   flooded versus starved responders. Interviews (Kip, Dot, Ambrose) describe both but
   were scoped to console redesign; nobody asked about routing.
4. **Squeezed items.** Handoff says "a couple"; I can identify only Availability
   Confidence (committed for 4.2, absent from notes). The roadmap still shows it committed.
5. **Roadmap vs briefs.** Bulk Callout brief says unstarted but it shipped in 4.1 and isn't
   on the roadmap. The Handler phone app brief rests on Dot's "tell me too" quote, but her
   real problem is pings vanishing before her responder reaches his phone. "Shared cover"
   has no brief and is probably the glossary's "mutual aid".
6. **4.3 approval chains point the wrong way.** The brief adds a second approval step plus
   five stretch asks; Halloran and tickets 3063 and 3074 say approvals are already too slow
   (11 days, one queue, dead priority field). No Supply PM is listed.
7. **Supply coupling is undefined.** Maintenance avoids "low callout load" but the record
   holds availability, not load. Ticket 3054: service booked on marathon day.
8. **Filters aren't just noise.** Resets without warning, shared computers keep a
   colleague's filters, no clear-all. A trust issue.
9. **Missing:** ranking description, Security Policy 4.1, Q4 roadmap, 4.3 date, acceptance
   targets, prior-year August data (database starts 29 Jun), data after 6 Sep, Ravi's
   reports.
10. **Oddities:** ticket 3075 bills The Undertow twice despite the one-seat rule; the
    directory dated 2 Sep credits Sofia with interviews finished 5 Sep.

### Open to-dos
Agree with Helen which squeezed items are still Q3 commitments; get Ravi to split taken
and missed by responder and week; have Wen Li explain ranking and write it down; ask
Marcus whether the ping wait can be tested alone.

### Learned in session 1 (Module 1)
- The wiki's Product briefs, Research and Customer interviews pages and rook-database (callouts, pings, responders, handlers, support_tickets; 29 Jun to 6 Sep) matter more than the handoff. The saved plan is `4.2-remediation-plan.md` in the root.
- Missed pings are up in every time band and fit the 60s ping wait. Unfilled callouts (5.5% to 11%) sit in Southport, Riverside and Kingsbridge, not in the starved responders' areas. Treat these as two separate problems.
- Starved responders and their handlers: Farlight (Linda Pruitt), The Undertow (Desmond Okafor), Meteor Mite (Kip, who also handles flooded The Gale in the same area), Vesper (Aunt Dot). Reach responders only through handlers.
- Still open: why 60s was chosen, whether the rank penalty for missed pings drives the starvation, and whether September recovered. The database data ends 6 Sep, so ask Ravi for a fresh extract.
- Session 2: the four interviewees and the 12 ticket filers barely overlap (only Ambrose is in both), so neither source stands alone. Count people, not tickets. Tickets are categorized in `support_tickets_categorized.csv`, and the plan is now v3.1 (`4.2-remediation-plan.md`). Who's who is in `stakeholders.md`.
- Tickets (147; there is no category field, `status` is only open/closed): "gone before he could answer" is 15 tickets from 11 handlers, "phone gone quiet" is 30 tickets from only 4 handlers. All 45 are open while other themes are closing. Dark mode, text size and the tag legend were steady before and after 4.2, so they aren't regressions.
- Pings confirm four starved responders (Farlight, The Undertow, Meteor Mite, Vesper), each down from about 12 pings a week to about 1 after a burst of 4 to 5 misses in the release week. Corporal Ashgrove and Halfmoon only dropped about 20%, in line with the system-wide miss rate. The other ten responders got 16% to 43% more pings, so the aggregate hid the split. Kip and Dot filed no tickets.
- Still open: ranking scores and per-ping response times (Wen Li, Marcus), whether 4.2's duplicate-push fix suppressed real pushes, the routing override log, whether anyone replied to the 45 open tickets (Nadia), and data after 6 Sep (Ravi). Marathon-day maintenance tickets 3054 and 3109 conflict with Halloran's praise of maintenance scheduling.

### Learned in session 3 (Module 3)
- The routing code is in `00-rook/code/dispatch-routing/` (read `config.py` and `history.py`). 4.2 cut the offer wait 90s to 60s, raised proximity weight 0.45 to 0.60 and cut recent acceptance 0.40 to 0.25. A missed ping counts as a decline (-0.12, a take is +0.08), the score never decays (the 2019 TODO), so below about 60% taken a responder drifts to the bottom of the list.
- Primary metric is the weekly missed-ping rate (missed / pings sent): 1.2-3.4% a week before 4.2 (2.3% pooled, 24 of 1,034), then 21.5%, 17.7%, 14.8%, 12.7% to the week of 31 Aug. It jumped on release day (7 of 25 on 12 Aug, 48% on 13 Aug). The first ticket was the same day, the first "gone quiet" ticket 17 Aug, the first Slack escalation 18 Aug. Use "about 1 in 8" for the latest week only; since 12 Aug it is about 1 in 5.5.
- The metric has limits: "missed" depends on the ping wait, so before and after are not like-for-like; it can't see starvation (the four starved responders fell from 28% of pings to 2-4%, though they were 17 of the 38 release-week misses); the 17-18 Aug dip is not a recovery. Pair it with a starved-responder count and unfilled callouts. Unfilled callouts were 12.7-14.0% for three weeks, then 5.5% in the week of 31 Aug (one noisy week), and weekly callouts fell from about 138-144 to 110-127.
- Starved four after 12 Aug: 56 pings, 33 missed (59%). The other 12 went from 2% to about 14% missed. In the first post-release week, the four with 4+ misses lost about 85-90% of their pings; nobody else collapsed. The "delivery" theory is not supported; ranking plus the 60s wait fits better. Ashgrove and Halfmoon "quiet" tickets (10) are not backed by pings (gaps of 3.0 and 2.5 days are normal).
- Case study: The Undertow (`00-rook/data/case-study-the-undertow.md`). 5 misses in 3 days after 4.2, nothing taken since 17 Aug, 11 handler tickets (all open) that match the ping dates exactly. Charts saved as SVGs in `00-rook/data/`.
- Still open: ranking scores and per-ping response times, why 60s was chosen, a data extract after 6 Sep (Ravi), whether anyone replied to the open tickets, why callouts fell 10-20% at 4.2, and whether the weekly missed-ping query can run on a schedule.

- Session 4 (Module 4): 4.2 changed only three numbers in `config.py`: offer wait 90s to 60s, proximity weight 0.45 to 0.60, recent-acceptance weight 0.40 to 0.25. The steps and flow are unchanged; the capability weight (0.15) and the +0.08 / -0.12 points carry no 4.2 note. "Before" values come only from the "was ... until 4.2" comments, since the repo has one commit and no older code.
- The lower acceptance weight makes a low score cost less in ranking (4 misses is about 19 min of travel before 4.2, about 9 after; a zero score is about 40 min before, about 19 now), so the weight change doesn't explain the starvation. Leading hypothesis: the 60s wait caused a burst of misses, a miss scores like a "no", and the score never recovers.
- Only `record_accepted` (+0.08, called at `offer.py:28`) adds points; break-even is about a 60% take rate. From zero it takes 7 takes to reach neutral and 13 to reach the top, and the starved four get about 1 ping a week. The Undertow's score (about 0) is my estimate, not data.
- Before 4.2 the starved four turned down 15-29% of pings, in line with unaffected Halfmoon (28%) and Captain Vantage (24%). All 16 responders predate 29 Jun, so "new vs existing responders" can't be tested; the code applies the weights to everyone. Marcus's 14 Aug Slack question had no reply; a one-sentence answer is drafted, not sent.
- Open: are the in-memory scores reset on release or restart (ask Wen Li)? Drafted, not sent: questions for Wen Li (scores, why 60s, 2019 TODO) and Marcus (per-ping response times, data after 6 Sep, testing the wait alone).
