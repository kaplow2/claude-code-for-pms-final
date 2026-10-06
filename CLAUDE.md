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
