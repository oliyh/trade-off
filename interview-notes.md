# Interview notes (raw material, verbatim/near-verbatim from conversation)

Working doc — captures answers as we go, organised by CLAUDE.md section. Not copy,
just raw material to draft the blog post from later.

## Section 5/6 material: Release paperwork automation (strong opening anecdote / xkcd #1)

Five paperwork systems that all had to line up for a single release:
1. Invisible/undocumented system driven by emailing a human — described the release,
   timing, teams involved, collected signoff.
2. Getting all Jiras into the right state, including uploading testing evidence to a
   third system, at a precise moment in the Jira workflow. Three extra Jiras created
   per release (regression, performance, UAT) — wording had to be very precise
   because a human review team checked epics/Jiras against a rulebook.
3. Recording which budget the released applications came under.
4. Engaging the actual release team for the time window.
5. A wiki page with release and rollback notes.

Could take days — first attempt took the user 4 days. Some people's entire job was
"farming release paperwork." Human review always found something, forcing rework of
multiple steps. No single person knew the whole end-to-end process. When two key
people who held that knowledge left the bank, the job fell on developers.

Motivation: user was trying to get weekly releases (vs the 4+ week cycle everyone
else used) — 4 days/week on paperwork was not sustainable.

Automated via: driving Jiras through their API, email templates to drive required
human steps, creating wiki pages via API, reverse-engineering portal forms so the
app could fill them in, and a Playwright script to drive a UI when another team
refused to provide an API.

Result: best case got the whole process down to ~20 minutes. Weekly releases held.

Pushback: yes, especially from teams who discovered their API had been reverse
engineered or their site was being driven automatically. Handling it: be respectful,
don't corner people, offer to help — "I'm happy to be a pilot user for you" reframes
it as helping them, gets you what you want, lets you tailor it to your needs, and
gets it sooner. Also important to make clear you're not trying to cause harm.

## Section 3/6 material: Fast Linux dev envs (strong xkcd material)

Standard bank issue: Windows build on standard (or "trader spec") hardware, but I/O
strangled by multiple endpoint security apps — the exact things developers hammer
(git, IDEs, compilers). Worst case observed: `git status` took ~3 seconds, vs ~3ms
on a normal machine (~1000x).

Attempted fixes and their limits:
- Special directory (e.g. `C:\dev`) with reduced scanning.
- Special developer security profiles — didn't help much.
- Hardware bumps — at best ~50% faster, so 1.5s instead of 3s for that git call.
  Still nowhere close.

Only real fix: a Linux machine without the endpoint security stack, made secure by
design instead (segregated network, containers) rather than by bolting scanners onto
everything. Best setups seen: Linux VMs via SSH/X-forwarding, or Linux containers on
the Windows host, using something like Coder for templated dev environments —
new joiners spin up a working dev image in minutes.

Contrast: getting software approved/installed on a standard Windows machine could
take many days. Everything requires a separate request, through tortuous forms,
chasing multiple approvers — documentation on what to request is usually out of
date, so new joiners spend their first weeks following stale instructions and
chasing approvals. If not all approvals land in time, the request auto-cancels and
you have to start over. **[xkcd candidate: the request-timeout-cancel-restart loop]**

How it actually happened: not an org-wide initiative — the Linux VMs already existed
but weren't advertised. Got there by finding the people leading devex in the org,
learning what they were building, contributing to it, offering to be a pilot user,
trialling and refining it on his own team first, then sharing more widely.

General principle (transferable): every big org has forward-looking pockets and
"stone age" pockets who never question their tools or dismiss new approaches as
fads. Your own team is unlikely to be doing everything the best way — worth
exploring the rest of the org, building connections with people who get things
done, and listening to the grapevine for better tools/approaches already in use
elsewhere internally.

## xkcd image candidates so far
1. Release paperwork — five systems needing to line up, days of manual chasing.
2. `git status`: 3ms vs 3s (endpoint security strangling dev tools).
3. The request-approval-timeout-cancel-restart loop for getting software installed.

## Section 4 material: Keeping business people happy (concrete incident)

Structured notes platform: a UI "price explorer" for pricing structured notes, with a
highly automated workflow behind it (traders tweak prices, quotes turn into deals,
securitisation, termsheet generation, etc). Innovative feature: structurers could add/
update structured products without large-scale dev work — normally end-to-end support
across multiple applications for a new product could take months, and being first to
market with the right product for market conditions could capture ~80% of the
available revenue if no competitor had one. Solved by describing products as JSON
Schema and passing that blob through every application — UI built its displays/forms
from the schema (product-agnostic apps). [Direct link to the jsonschema-talk repo.]

A consultancy had a year to deliver the UI; 6 months in, hadn't really delivered
anything and was struggling. The user's team (3 people) took over with the remaining
6 months. Strategy: demo something within 2 weeks, get something basic into prod
within ~6 weeks, then a demo every week. Helped by inheriting wireframes/design from
the previous team. Business had lost confidence in tech delivery — showing small,
working, iterating increments rebuilt trust. Looking good mattered too: it gave
people's imagination somewhere to start, so they could project forward onto what they
really wanted. Hit the 6-month go-live; product/team went on to be very successful.
Also credits good product owners who shielded the dev team and were always available
to discuss features/behaviour.

## Section 5 material: Choosing a hill

### Small hill (reframed: "small" refers to the task, not the effort)
Getting one line of code to production can be a huge effort — it's the lowest common
denominator of every software project, so it's worth automating heavily: fast tests,
faster/better CI feedback, deflaking tests, release automation, better release
cadence, faster dev machines (e.g. Linux VM compiling faster).

Principle: **frequency × cost** determines what's worth optimising. Things done
constantly (shipping code) deserve heavy investment; things done rarely don't.
Concrete math: saving a team 7 minutes/hour ≈ 1 hour/day ≈ half a day/week per
person — at scale, equivalent to an extra developer.

Same math applies to eliminating low-value recurring costs, e.g. a daily 30-minute
status call every team member sits through — also costs about a developer-week.
Fixes: send one person to summarise back to the team, ask to be invited only when
relevant, ask for notes instead of attendance if you need to be informed but don't
need to contribute. Be respectful but honest about it. Observation: people over-fill
their calendars with calls, then can't get their actual job done during working
hours, creating pressure to work out-of-hours — this is avoidable.

### Big hill: rewriting off a home-grown legacy ecosystem
Old stack (as of 2026): old Python, a mega-monorepo that took forever to build and
was chronically red/broken, an unusable proprietary version control system, a fixed
old set of libraries, an opaque homegrown scheduler (couldn't tell what code was
running or when something was actually deployed), a homegrown DB — despite modern
tooling (Bitbucket, VS Code, current Python, k8s) being available and used elsewhere
in the org. Cause: pure inertia, no "modern SDLC experience" team owning the gap.

Took about a year — much longer than it should have — because it had to route
through many disjointed teams each owning one small piece (provisioning,
architecture, process), justifying effort/time to rewrite in modern Python, working
out new CI and release processes from scratch. User "wanted to give up many times."

Case made to business people (who saw no visible functionality from this work) in
their own terms: more frequent releases, lower lead time, features delivered sooner.
Reinforced with a monthly newsletter of concrete metrics (e.g. "48 application
releases this month") and individual stories ("feature X requested Wednesday,
delivered Friday"). Programme lead specifically praised this — called it exactly
what the business wanted from IT: responsive and fast.

Rationale/benefits argued: modern SDLC as a foundation with years of compounding
benefit — new developers arrive with transferable skills and aren't put off by an
ancient ecosystem; developers get more control and are happier; a service-oriented
architecture becomes possible, with service interfaces as testable contracts,
letting services release on independent cadences instead of one bug derailing a
whole release; smaller focused codebases per team; smaller blast radius for bugs/
build breaks.

## Section 3/6 material: Onboarding — the diagram technique (transferable skill)

Onboarding is scary: lots of new people, complicated systems with unfamiliar names,
unfamiliar processes, information overload. People hand you links you don't have
access to yet. Everyone is busy. Everyone's brain works differently, but the user's
approach is diagrams — lots of them, of the same underlying information but from
different angles/starting points, each building a different facet of the mental
model:
- who belongs to which team
- what those teams actually do
- what a given system is for
- the journey of a quote — which systems it passes through, which desks touch it
- where a given piece of data actually lives
- what systems a trader uses to do their job; what systems a salesperson uses

**Why diagrams specifically:** you can hand one to someone and ask "where does the
thing you just told me fit on this?" — it shows them exactly what you currently
understand, so they can correct a misunderstanding precisely or explain the next
layer more efficiently, instead of re-explaining from scratch. Sometimes the diagram
turns out wrong and you tear it up and redraw it — that's fine, it's a tool for
building understanding, not a deliverable. Starting a fresh diagram from a different
entry point (e.g. "the quote's journey" vs "the trader's toolset") surfaces a
different perspective on the same territory and fills gaps the other views didn't
reach.

**On asking questions:** you will forget things, and you shouldn't be afraid to say
you don't understand — tell people upfront that you're new, most people are patient
with that. The one thing worth actively avoiding is asking the *exact same*
question twice, since that reads as not having listened/paid attention. Writing
things down and diagramming is what makes that avoidable — and if you do need to
revisit a topic, reframe it to demonstrate what you retained and narrow in on the
actual gap: e.g. "You told me X does Y because Z, but Z only seems to apply in a
minority of cases — so why does X do Y the rest of the time?" This is the concrete
mechanism behind the "ask questions once, integrate the answer" toolkit principle
already in notes.txt (line 69/100) — ties Section 3 (first day) directly to Section
6 (toolkit/personal qualities).

## Section 4 material: Excel is inevitable — build for it, don't fight it

Extends the existing "spreadsheets for everything" symptom (notes.txt line 103)
into an actionable engineering principle, not just a diagnosis: everything ends up
in Excel eventually, no matter what you build. Don't fight that. If your app
doesn't ship with an Excel import/export, you are guaranteed to eventually be
creating a job for someone (possibly future-you) to copy data cell-by-cell into or
out of a spreadsheet by hand. Good transferable skill for Section 4's "concrete
weird bank things" list — pairs the symptom with the fix, which the other items in
that list currently don't have. Also a clean xkcd candidate: someone manually
retyping a spreadsheet that should have been an export button.

## Section 6 material: Personal qualities — reminders/habits (not concrete moments yet)

Framed by the user as: you can't rewire your personality on the fly, but there are
habits/reminders that help.
- Put yourself in the other person's shoes — what's actually motivating them.
- Prepare for meetings: know the one point you want to land and the facts you'll
  need to back it. User likes to screen-share diagrams in meetings specifically —
  gets everyone looking at the same picture, focused on the same thing (direct
  callback to the onboarding-diagrams technique — same tool, now used to persuade
  rather than to learn).
- Be prepared to learn new things — seek first to understand, then to be
  understood. The mental model you build is the single most useful tool you have
  (ties back to Section 3 diagram material again).
- Failures will happen. What matters is that you did what you reasonably could to
  avoid them, to mitigate them when they happened, and to prevent recurrence.
- Don't try to do everything yourself — a Big Org's to-do list is infinite; trying
  to clear it burns you out. Look for the highest-impact things and focus there
  (echoes the frequency × cost framing from the small-hill material).
- Small, unplanned favours for someone can build goodwill that pays off later when
  you need them to unblock you — worth doing even off-plan.
- Stay on top of the emails that matter by investing real time in good filters
  (reinforces the existing "signal from noise" toolkit line).

**Resolved — no anecdotes, staying as principles (confirmed by user):**
- *Stupid question that mattered*: no specific anecdote to hand — keep as the
  general principle only (ask it, say you're new, don't ask the same one twice).
- *Left it better than I found it*: deliberately **not** meant to be one anecdote —
  it's a general habit to apply to anything you touch (a test, a CI pipeline, a
  deployment architecture, a UI, documentation). The payoff is reputational: you
  become known as the person who *makes things better*, not the one who *leaves a
  trail of destruction*. This is itself the section's takeaway line — works well as
  a closing principle for Section 6, maybe even echoed in the talk's actual Close
  (Section 7 is literally "leave it better than you found it").

## Section 5 material: Ask forgiveness vs declare upfront — tech debt

"Ask forgiveness" is most often the pattern needed for **technical debt**. Sometimes
something becomes enough of a drag on the dev team that it has to be dealt with, but
the business sees zero direct benefit from time spent on it — worse, if performance
is already in question, spending visible time on "fixing technical things" reads as
not delivering. Even sympathetic/"enlightened" stakeholders who say they understand
often can't act on it: asking permission explicitly tends to get **"yes, but
later"** — a later that never arrives. Timing matters too: if your team is the last
piece of the puzzle before a feature ships, that is not the moment to raise it.

**The actual technique used is a hybrid, not pure ask-forgiveness:** fold tech debt
into planning as *reduced delivery capacity* — "here's our capacity for this
sprint" with some already set aside for tech debt — rather than asking for
permission as a separate, explicit ask. This gives the business something concrete
to work with and sets expectations, without opening a debate that stalls on "yes,
but later." Stay honest about it — but honest is not the same as asking upfront for
approval.

**Two flavours of tech debt, two different remedies:**
- *Incidental* debt builds up passively — volume growth the app wasn't designed
  for, a library that's become hard to major-version-upgrade. This tends to need a
  dedicated, visible chunk of time.
- *Active* debt builds up through normal feature work — skipping DRY, not writing
  representative test scenarios, while under feature-delivery pressure. This can be
  paid down incrementally rather than in one stop-the-line effort: budget ~10% of
  feature implementation time to refactor (or prefactor — restructure *before*
  writing the new feature code, which the user prefers, since it makes the actual
  feature change land cleanly). The delivery line slows slightly but visibly keeps
  moving, and the team compounds toward a more sustainable codebase — important for
  multi-year, multi-person projects.

*(Still open: a specific example of the "declare upfront" side of the pair, if one
exists distinct from the sprint-capacity framing above — that framing is arguably
already "honest but not upfront," a middle path between the two poles named in
CLAUDE.md.)*

## Section 5 material: AI adoption counterexample (confirmed + expanded)

Normal pattern for new tech adoption in Big Org is **bottom-up and adversarial**:
devs use something outside work (containers, Selenium/Playwright, MongoDB, newer
languages like Clojure/Kotlin/Go), see the clear advantage, then have to fight the
restrictive toolset and policy to bring it in — downloads blocked, security
scanners flag unapproved software on your machine. You have to prove it doesn't add
an attack vector, that it's battle-tested, that there's a large enough hiring pool
for it. Default answer is always no. Even the Openshift/platform-adoption fight
(the "big hill" example) was comparatively easier — that was adopting something the
bank itself had already provided; getting genuinely new tech in from outside is a
harder fight again.

AI adoption inverted this completely: instead of developers asking permission, it
was **enforced top-down** — "you have to use this" — regardless of whether people
wanted it. Behaviours that would normally be discouraged (e.g. "tokenmaxxing" —
burning as many tokens/calls as possible) were actively incentivised. From
conversations, none of these organisations have a clear read on how much value
they're actually getting from AI, but they know precisely what it's costing them.

Likely cause (a mix, not blaming anyone for it): C-suite fear of being left behind
competitors, sales hype and promises from AI fanatics, and firsthand exposure to
AI's power in everyday life — the astonishing results of vibecoding a simple app
taken on faith as linearly extensible to the highly complex systems inside a Big
Org. **Framing/xkcd candidate:** like a medieval peasant handed an iPhone — dazzling
interface, but an enormous amount of invisible infrastructure has to work correctly
before it does anything meaningful. Easy to get caught up in that when you're the
peasant.

Thesis for the talk: AI adoption is proof that fast, org-wide change *is* possible
in a Big Org when the motivation/mandate is strong enough — it's just that this
motivation almost never points at the things engineers actually want changed
(tooling, process, tech debt). Useful contrast with the "choose your hill" /
ask-forgiveness material: change that normally takes years of grassroots argument
can happen in months if it's mandated from the top.

**Core insight / recurring thesis candidate — "the flexibility spiral":** when
releases are slow (cycle times stretching to months), businesses ask for features to
be built maximally flexible/configurable up front, because they can't afford to wait
months again for a fix or adjustment. This makes the feature bigger, slower to
build, and more bug-prone — which lengthens release times further and can make the
feature irrelevant, buggy, or over-engineered by the time it ships. Fast release
cycles (days, not months) break this spiral entirely: ship something simple, adjust
it days later, fix bugs as soon as found. Combines directly with the small-hill
material (this big-hill rewrite is what made the small-hill discipline possible at
scale).

## Section 7 material: Audience / venue / closing

**Audience:** colleagues within the user's consultancy — most already placed at Big
Org / banking clients, so the banking-specific detail lands directly and doesn't
need heavy translation. Secondary audience: the blog post version may reach new
joiners at those clients, who are expected to get the most value from it —
especially those early in their careers. Implication for tone: keep the
banking-specific texture (it's recognisable and credible to the primary audience),
but keep each section's takeaway generalised/reframable enough that an early-career
new joiner reading cold gets an actionable idea, not just an in-joke.

**Close / takeaway:** wants the audience to leave with ideas they can actually
apply — reframes that make the day-to-day experience more positive, approaches to
meetings and conversations, and above all a path to being productive *and* happy.
Confirms "leave it better than you found it" (Section 7, and now echoed from
Section 6) as the right note to end on — it's the through-line: individually small,
locally-scoped actions (a diagram, a prefactor, a filter, a favour, a slightly
better test) are what compound into both personal sanity and organisational
improvement.

## Still to interview (from CLAUDE.md open list)
- Ask forgiveness vs declare upfront — got the tech-debt / ask-forgiveness side in
  full; the pure "declare upfront" contrast case is still open (see note above).
  This is the only remaining open item — everything else on the original list is
  now covered.
