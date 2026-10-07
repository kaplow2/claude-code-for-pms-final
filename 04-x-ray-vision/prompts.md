# 04 · X-Ray Vision — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. Last session the numbers showed you what happened: a
ping used to wait ninety seconds and now it waits sixty, people
missed pings they used to catch, and missing one counts the same as
turning one down — so four responders stopped hearing from us
altogether.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.

Can we isolate where changes were made in 4.2 vs. what is static/existed prior to 4.2?

### 2.

Provide me side by side visual workflows / process flows that show the pre-4.2 and 4.2 steps

### 3.

Looking at the starved responders, inspect the code for how their experience was changed pre-4.2 and post-4.2

### 4.

Do the changes and weighting and response window support Undertow's case story from last session?

### 5.

Using this information, complete the sentence "Based on what I found, the reason some responders are getting no pings at all is ___, because ___."

### 6.

Draft questions for Wen Li and Marcus

### 7.

Marcus asked this question in Slack on Aug 14 2:47 PM "Quick one, did the change to who gets asked first apply to responders who'd already been turning jobs down, or just new ones? Can't tell from the code and don't want to guess on this. Anyone know?"

No one has responded to this question. Based on our hypothesis statement and our data findings, draft a response for Marcus that clearly and succinctly answers his questions. Verify you have the data you need and ask me questions where you are uncertain before you craft your response.

### 8.

This is comprehensive. Provide me a one sentence version that still captures the major points and addresses Marcus' question.

### 9.

Find me the part of this code that takes points off somebody when they miss a ping or turn one down. Show it to me and explain it in plain English. Then find me every single thing in this code that puts points back on.

### 10.

Once a super hero hits zero, how do they actually recover? We can use one of our superheroes as an example -- Undertow, our case story. How exactly would Undertow recover from the current score?

### 11.

Would the following be an accurate summary? Provide recommendations for edits:

According to my findings in the code, for someone who's gone quiet, they would need to answer roughly 13 calls in a row to recover from zero. There is no scheduled reset or natural score recovery in code. There is an open TODO from 2019 that flags this for future consideration.
