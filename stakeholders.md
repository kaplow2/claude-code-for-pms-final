# Rook Dispatch stakeholders

Sources: the Team directory (updated 2 Sep 2026), the `responders` and `handlers` tables, the 4.2 release page, the Sept interviews and the support tickets. Ping and ticket figures are through 6–7 Sep.

**Rules for contact:** reach responders only through their handlers. Cover identities are never stored or mapped to legal identities (Security Policy 4.1, not yet read; check it before any new per-responder reporting).

## 1. Rook team

| Name | Role | Location | Owns | Why they matter here | What I need from them |
|---|---|---|---|---|---|
| Helen Achebe | Director of Product (my boss) | Site Aleph | Roadmap and commitments | Decides which squeezed items are still Q3 commitments; owner of the "don't revert" instruction | Why 60s was chosen; which commitments stand; acceptance targets; a brief this week |
| Marcus Oyelaran | Engineering Manager, Dispatch | Site Aleph | The Dispatch engineering team | Controls any hotfix and can pull numbers; raised the ranking question on 14 Aug | Can the wait change without a release; test the wait alone; response time per ping; override log; next release date |
| Wen Li | Staff Engineer, Dispatch | Berlin | Built the ping ranking (undocumented). Away 14–24 Aug | The only person who knows how ranking works | How a missed ping affects rank and for how long; what happened to the four starved responders in the first week; write ranking down |
| Ravi Menon | Data Analyst | Singapore | The numbers; weekly acceptance-rate report | Source of fresh data and the prior-year baseline | Extract past 6 Sep; all responders ranked by change in pings; time-to-accept by responder; earlier August data; his weekly reports |
| Nadia Hoffmann | Support Lead | Berlin | The tickets | Hears handler complaints first; 45 Dispatch tickets are still open | Replies and close history; a holding reply to the 45 open tickets; first-reply times; other channels such as the forum |
| Sofia Marino | Product Designer | Site Aleph | The console and the phone app; ran the Sept interviews | Holds the full transcripts (we have excerpts) and the console backlog | Full transcripts; routing questions for follow-up interviews; home for dark mode, text size, tag legend |
| Priya Raghunathan | Former Product Manager, Dispatch (left 21 Aug) | n/a | Owned every roadmap item and the 4.2 change | Her handoff says "mostly seasonal, don't revert" and isn't supported by the data | 30 minutes if reachable: why 60s, what she saw in August (Marcus has her number) |

## 2. Handlers (they sit at the console and are my route to responders)

Tickets span 29 Jun to 7 Sep. Status is my read from the tickets, interviews and pings.

| Handler | Responder (area) | Tickets filed | Interviewed | Status and notes |
|---|---|---|---|---|
| Linda Pruitt | Farlight (Uptown) | 19 | No | Starved. 10 quiet tickets. Call first |
| Desmond Okafor | The Undertow (Harborside) | 21 | No | Starved. 10 quiet tickets, also reported a double bill (3075). Call first |
| Kip | Meteor Mite and The Gale (Eastgate) | 0 | Yes, 4 Sep | Mite starved, The Gale flooded (+43% pings). Wants dark mode and a distinct alert sound per responder. Call first |
| Aunt Dot (Dorothy Pell) | Vesper (Old Town) | 0 | Yes, 3 Sep | Starved. Describes pings vanishing before Vesper reaches his phone. Call first |
| Yusuf Demir | Corporal Ashgrove (Northfield) | 14 | No | Mild drop (about 20%); 5 quiet tickets |
| Simone Fischer | Halfmoon (Westbury) | 15 | No | Mild drop (about 20%); 5 quiet tickets |
| Mr. Ambrose | Captain Vantage (Hillcrest) | 1 | Yes, 2 Sep | Reports "one boot on" callout loss; filters, small status badge, tag legend |
| Halloran | Sgt. Bulwark (Foundry Row) | 0 | Yes, 5 Sep | Mostly Supply: requisition approvals, failure reports, catalog search. Also runs the gear cage |
| Renata Kovač | Stormwrack (Southport) | 10 | No | Southport has unfilled callouts |
| Teresa Alvarez | Ironvale (Riverside) | 12 | No | Riverside has unfilled callouts |
| Owen Bramwell | Sgt. Falkirk (Kingsbridge) | 11 | No | Kingsbridge has unfilled callouts; +40% pings |
| Marjorie Sung | Nightwell (Midtown) | 12 | No | Busiest responder overall |
| Graham Petrov | The Longcast (Lakeshore) | 11 | No | No special pattern |
| Beatrice Calloway | The Drift (Greenway) | 11 | No | No special pattern |
| Farid Haddad | Cindermark (Mill District) | 10 | No | No special pattern |

Handlers who use Supply as well as Dispatch (Halloran, and any handler raising requisitions) are the likeliest to feel the Supply coupling.

## 3. Responders (independent, masked, reach only through handlers)

Pings per week before 12 Aug versus after, through 6 Sep.

| Responder | Handler | Area | Before | After | What the data shows |
|---|---|---|---|---|---|
| Farlight | Linda Pruitt | Uptown | 11.9 | 3.0 | Starved; last ping 28 Aug; 64% of post-4.2 pings missed |
| The Undertow | Desmond Okafor | Harborside | 11.9 | 3.8 | Starved; 64% missed |
| Meteor Mite | Kip | Eastgate | 11.1 | 3.8 | Starved; 57% missed |
| Vesper | Aunt Dot | Old Town | 13.7 | 4.6 | Starved; last ping 1 Sep; 53% missed |
| Corporal Ashgrove | Yusuf Demir | Northfield | 10.0 | 7.8 | Mild drop; 14% missed |
| Halfmoon | Simone Fischer | Westbury | 11.0 | 8.9 | Mild drop; 15% missed |
| The Gale | Kip | Eastgate | 13.0 | 18.6 | Flooded (+43%); "exhausted" per Kip |
| Sgt. Falkirk | Owen Bramwell | Kingsbridge | 10.0 | 14.0 | +40% |
| Captain Vantage | Mr. Ambrose | Hillcrest | 12.1 | 15.9 | +31% |
| Stormwrack | Renata Kovač | Southport | 13.0 | 17.0 | +30% |
| Ironvale | Teresa Alvarez | Riverside | 8.1 | 10.5 | +30% |
| Nightwell | Marjorie Sung | Midtown | 15.1 | 18.9 | +25% |
| Cindermark | Farid Haddad | Mill District | 9.1 | 11.3 | +25% |
| The Drift | Beatrice Calloway | Greenway | 6.2 | 7.5 | +22% |
| The Longcast | Graham Petrov | Lakeshore | 7.2 | 8.6 | +20% |
| Sgt. Bulwark | Halloran | Foundry Row | 9.1 | 10.5 | +16% |

Every responder outside the starved four also saw misses rise from 0–3% to about 10–18%.

## 4. Not in the directory (roles to find)

| Role | Why |
|---|---|
| Supply product manager | None listed; Supply reads the availability record Dispatch writes, and 4.3 adds an approval step |
| Quartermasters | Own the approval queue behind the 9 to 11 day waits; never interviewed |
| Owner of Security Policy 4.1 | Sign-off before new per-responder reports |
| Finance | Churn risk from starved responders; duplicate billing in tickets 3023 and 3075 |
| Release manager or QA | Hotfix path for the ping wait |
