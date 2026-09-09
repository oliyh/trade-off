# Surviving and Thriving in Big Organisations

Talk (20-25 min, reveal.js) + blog post (markdown), same content, blog written first
in full detail, slides summarise it. Slides: minimal text, image-led, detail lives in
speaker notes. xkcd-style images generated via a Gemini gem — one image can replace a
slide's worth of words.

Style reference for slide construction/reveal.js conventions: https://github.com/oliyh/jsonschema-talk

Process for this project: don't generate copy. Organise the user's own words into
structure, move notes into sections, and interview the user to fill gaps. Write the
blog post first (detailed), then derive slides from it.


Each section should have a transferable skill which is the key takeaway. This is a survival guide,
advice to people working in these orgs to help them survive and thrive, it should be
giving them something actionable. It could be reframing something, re-evaluating what is actually important,
saying no / I don't know, identifying something that slows you down / speeds you up.



## Narrative arc

1. **Intro** — the overwhelm of joining a Big Org: necessary and accidental complexity,
   regulators, learning business + IT domains simultaneously, bureaucracy and politics.
   Framed as: what can you actually do about it?
2. **History lesson (short)** — SmallCo → MiddleBiz → Large Inc → merger → Big Org.
   Purpose: symptoms of Big Org are consequences of this growth path, not arbitrary
   dysfunction. Sets up section 4.
3. **Your first day** — onboarding overwhelm, ramp time, the human cost of complexity
   (skating metaphor).
4. **Symptoms of Big Org** — the diagnosis. Two merged lists: abstract symptoms
   (centralisation, incompatible incentives, one-size-fits-all, churn, uncodified
   knowledge) and concrete "weird things banks do" (spreadsheets everywhere, tribal
   knowledge, stale documentation, meetings, never switching anything off, manual
   processes, budget quirks). Includes the IT-centralisation-decentralisation cycle
   (front office devs vs central IT) as a recurring pattern.
5. **Strategies for change** — choosing your hill, finding allies, build-alongside vs
   ask-forgiveness vs declare-upfront, the AI-adoption counterexample (top-down
   mandate proves fast change is possible when motivation is there).
6. **Survival toolkit / personal qualities** — practical, individual-level tactics:
   filtering signal from noise (email, meetings), learning to search/find the network
   of competent people, asking questions once and integrating the answers, automating
   for sustainability (not just personal time but codifying institutional knowledge),
   not needing to fix everything or stay 30 years.
7. **Close** — leave it better than you found it.

## Where your existing notes go

- Lines 15, 73 (duplicate intro paragraph) → Section 1.
- Lines 18–30 (SmallCo → Big Org history) → Section 2.
- Lines 34–35 (first day, skating metaphor) → Section 3.
- Lines 38–44 (symptoms list) + Lines 102–109 (weird bank things) + Lines 75–79
  (IT centralisation cycle) + Line 81 (guardrails) → Section 4.
- Lines 59–63, 83, 85–94 (hills, allies, network, change tactics, AI counterexample)
  → Section 5.
- Lines 67–70, 96–100 (toolkit, personal qualities, automation, asking questions)
  → Section 6.

## Open areas to interview the user on

Thin or asserted-but-not-illustrated points — need concrete stories/examples,
especially ones that can become xkcd-style images:

- **Automating the "unautomatable"**: the specific release-paperwork automation
  story — what was the manual process, what did the automated version look like,
  what was the resistance?
- **Fast Linux dev envs**: what was the actual obstacle (virus scanner specifics,
  policy owner), how was it resolved, was it a "build alongside" or "ask forgiveness"
  case?
- **Keeping business people happy**: a concrete example of communication/delivery
  focus winning trust — a specific incident, not just the principle.
- **Choosing a hill**: a real example of a "small hill" (line-to-deploy) and a "big
  hill" (Openshift/spuds-snow-scale programme) the user actually fought.
- **Finding allies**: an actual instance of building independent-seeming consensus
  before a change.
- **Ask forgiveness vs declare upfront**: a specific example of each, and what made
  the user choose one over the other that time.
- **The AI adoption counterexample**: what did the user actually observe — timeline,
  what changed, who mandated it.
- **First-day/onboarding**: the user's own first-day story, or a new joiner they
  onboarded, to ground the skating metaphor.
- **Personal qualities section**: this reads as the most abstract/least anecdotal —
  needs 1-2 concrete moments (a "stupid question" that mattered, a case of leaving
  something better than found).
- **Closing note**: how the user wants to land the talk — a specific takeaway for
  the audience (engineers currently in a Big Org? considering joining one?).
- **Audience/venue**: who is this talk for (conference name/audience type) — affects
  tone and how much banking-specific detail vs general Big Org framing to keep.
