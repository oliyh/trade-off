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

## Still to interview (from CLAUDE.md open list)
- Ask forgiveness vs declare upfront — a specific example of each.
- AI adoption counterexample — what was actually observed.
- First-day/onboarding — user's own story.
- Personal qualities section — concrete moments (stupid question that mattered,
  leaving something better than found).
- Closing note / audience & venue.
