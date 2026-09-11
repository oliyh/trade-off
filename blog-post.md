# Surviving and Thriving in Big Organisations

Joining a Big Org is overwhelming. There is so much complexity in front of you - some of it necessary, some of it entirely accidental. There will likely be multiple regulators for your industry, and their demands show up as restrictions on what you can and can't do, because the cost of failure is extremely high for them. As an engineer you have to learn the business domain and the IT domain at the same time. Expect weirdness, inefficiency, frustration, politics and bureaucracy.

None of that is going away because you turned up. So the real question is: what can you actually do about it?

This is a survival guide. Not a manifesto for fixing Big Org - nobody fixes Big Org - but a set of things you can reframe, things you can stop worrying about and things you can actually change, so your time there is productive, tolerable and possibly even enjoyable.

## A brief history of Big Org

**Key quote:** None of this is personal - it's the predictable result of scale

Every business starts small and focused, and the ones you end up working for were successful enough to survive and grow. But Big Org didn't get big by growing organically. It got big through mergers and acquisitions - buying up competitors, adjacent businesses, whole product lines - and every merger brings confusion, complexity and a dilution of purpose. Once it gets big enough a second cycle emerges: centralisation of functions to save on overhead, followed by decentralisation when the centralised functions can't keep everyone happy. Each cycle leaves a trail of carnage and a not-quite-dead centralised function behind.

None of the weirdness that follows is arbitrary - it's no one's fault. The people you will work with are intelligent and usually want the same things you do. It's a function of size and complexity that simply outscales individuals by multiple orders of magnitude. Some things you'll see on the way to acquiring your thousand-yard stare:

*[COMIC: two small, tidy companies merging into one much bigger, visibly confused mess of departments and org charts]*

- Politics, bureaucracy, inefficiency
- Byzantine processes
- Centralised teams hidden behind ticket queues aka the black hole of service requests
- Conflicting requirements, sometimes for good reasons like regulation, sometimes because changing software is easier (not simpler) than changing the business
- One size fits all, whether it's your size or not
- Incentives for the wrong behaviour - like KPIs for how fast you close a ticket without measuring if it was closed satisfactorily
- Missing requirements and higher churn, because it's impossible to know everything up front
- Uncodified institutional knowledge - "wisdom of the ancients", "we've always done it that way"
- Spreadsheets for everything
- Documentation that's out of date the moment it's written
- Systems that will run until the heat death of the universe because we don't know what they do and we're scared to switch them off
- Budgets that won't let you hire people but will let you spend incredible amounts on IBM or Oracle

If these things are going to drive you insane, Big Org might not be for you. This is worth considering seriously, because I have seen multiple times someone join Big Org, get frustrated and leave 6 months later which is disruptive to them and the team they joined. Keep reading for some advice and tools which may help you face the challenge.

*[COMIC: someone using a spreadsheet to hammer in a nail]*


## Your first day

**Key quote:** build your mental model

Prepare to fill in some request forms. Lots of them. I tell people that the request form application is their new best friend.

You will be bombarded with information. New people, complicated systems with strange names, processes nobody wrote down properly, links you don't have access to yet, everyone is busy. Absorbing as much as you can, as fast as you can, is your first job. Everyone's brain works differently, but mine likes diagrams - lots of them, sometimes covering the same ground from different perspectives: who belongs to which team, what a given system is for, the journey of a single quote through the systems, the desks that touch it, where a piece of data actually lives, what a trader uses versus what a salesperson uses.

Each diagram builds a different facet of your mental model, and each one is something you can discuss with someone else. Show a colleague your diagram and ask "so where does the thing you just told me fit on this?" - it shows them exactly what you understand, so they can tell you precisely instead of re-explaining from scratch, and correct any wrong assumptions you made. Sometimes the diagram is wrong - tear it up and redraw it, it's your tool for understanding.

You will forget things, and you shouldn't be afraid to say you don't understand - tell people you're new up front and they will be patient with you. The one thing worth avoiding is asking the exact same question twice, because it looks like you haven't listened. Writing things down and drawing them makes that avoidable, and if you do need to revisit something, show you have been listening: "you told me X does Y because Z, but Z only seems to apply in a minority of cases - so why does X do Y the rest of the time?"

You get a honeymoon period - nobody expects you to break even before about three months, and you might not make a significant net contribution before six. That doesn't mean you have nothing to offer - on the contrary, your fresh perspective and ideas are something that you have which no one else does. Asking dumb questions can sometimes lead the person answering to realise that things can be simplified or avoided.

Your mental model is never complete; your responsbilities will grow, the world does not stand still. You should continually work on keeping your mental model up-to-date.

*[COMIC: someone tearing up a whiteboard diagram and starting again, a pair of ice skates hanging on the wall nearby]*


## How to make a difference

**Key quote:** pick fights you can actually win, make the case in the business's own language

We're usually engaged to bring expertise, both technical and domain, to a client's problem along with a team of skilled engineers who can help deliver a solution.

Our extra value as a consultancy is to look around while we're doing that and see how else we can help. It might be pain that we have during implementation, or pain we see within the wider team which impacts delivery. You can't fix everything, so choose your hills wisely. Consider how long something takes to do versus how frequently it's performed - shaving a few seconds off a small-but-frequent task is equally as valuable as saving a hours off a big task that you do once a week, or a day from something you do once a month. Time saved on a task can add up quickly over days and weeks, scaled across teams. If you have a team of 6, and you can save each one 3 minutes per hour, it gives you an extra 2 developer days per week. Wouldn't that be useful?

https://xkcd.com/1319/ + credit

### In the small

For a developer the small-but-frequent tasks are things like the code-test-refactor loop that we do hundreds of times a day. Optimisations include improving your typing speed and accuracy, the responsiveness and performance of the hardware, the IDE and tooling you use. Sadly, even these basic things cannot be taken for granted because you are often given a general purpose Windows machine, laden with endpoint security, to use for development alongside email, chat apps and (inevitably) Excel. I've found that within these environments a Linux machine will give you vastly better performance, more native tooling and the possibility of faster hardware (if it's a VM in the cloud). Finding and getting hold of one may not be easy, but worth fighting for.

Excel wasn't a joke, by the way. One piece of practical advice which seems to be an axiom: everything ends up in a spreadsheet eventually, no matter what you build or how good your UI is. Don't fight it - if your application doesn't ship with a spreadsheet import and export, you are guaranteed to eventually create a job for someone, quite possibly future you, copying data cell by cell.

### In the large

The big tasks can be very different. I spent a year working to provide an alternative to a home-grown legacy stack - old Python, a mega-monorepo that was chronically broken, an unfathomable version control system, a gnomic runtime scheduler - despite modern tooling already in use elsewhere in the organisation. There was so much inertia: sunk costs, urgent business deliveries, the local maximum paradox. A new tech stack wasn't going to help with the business aims, was it? Actually yes, it will - but you have to communicate the bigger picture, and frame it in a way the business can understand. They don't care if you use git or containers, but they do  care about more frequent releases, lower lead time for features, fewer bugs released. We communicated success with a monthly newsletter of business success stories: "Feature X requested on Wednesday, in production on Friday". The client didn't ask for this directly, but the need for it was obvious - they were struggling to release working software, with a spiralling release cadence, ever more bugs, and months to deliver features. The holistic approach we championed was a service-oriented architecture, with services encapsulating behaviour behind stable interfaces. This made testing much more automatable and reliable, allowed services to move at different speeds and gave us smaller releasable units. This allowed us to increase release cadence, which allowed us to deliver features faster.

The benefits of faster release cycles compounds as well: slow release cycles push users to ask for features to be built maximally flexible up front, because they don't want to wait months for the next fix - which makes each feature bigger, slower and buggier, lengthening the cycle further still. Fast cycles break that spiral: ship something simple, adjust it days later if it needs it. Furthermore, you get benefits with hiring - people will come in with more transferable skills, and it will be easier to find them when you're using standard modern infrastructure.

### Visible delivery

Visible delivery matters as much as fast delivery. I once worked on a project building a pricing platform for structured products, taking over from another consultancy that had used six months of the one year timeline not delivering much. My team of three delivered a basic demo within two weeks, had something akin to an MVP within six, and met the original production release date despite half the time lost before we even started. The business had lost confidence in tech delivery; small, visibly iterating increments helped build trust in our new team.

I once worked with someone who would share this image at every opportunity. I still find it useful today, along with the mantra "Make it work, make it right, make it fast". They are useful reminders for everyone that every long journey starts with the first step.
[img of agile delivery] - credit to https://blog.crisp.se/author/henrikkniberg

### Sustainability

Speaking of long journeys, your speed needs to be sustainable. The system on the legacy stack I described above would have started out efficiently and productively. How can we avoid a descent into entropy?

**Technical debt** is never given the respect it deserves; the business features are always more important. This works fine until the delivery grinds to a halt because the drag from tech debt has consumed all developer output. No one wants that, but it's very convenient to ignore it. I believe the IT team have a responsibility to communicate the cost of technical debt and should discuss it openly with the business, but also retain ownership over addressing it. This is usually done in two ways: a small tax on every change or a big work item. Personally I prefer the former; it's easier for the business to budget for and you can land your changes more cleanly if you've done a nice prefactor to tidy up all the code that you're about to touch. Big work items are sometimes necessary, and should be balanced - devote one developer to it, and have the rest keeping the business happy rather than stopping the entire line.

**Clear responsibilities** for each application. A system may need very complex behaviour, but that doesn't mean you can't compose it of simpler things. Simpler things can be developed faster, released with more confidence, fit inside a developer's head. Often the excuse of it being too hard to make a new application is used to just bundle it into something else, multiplying their complexity and vastly complicating their later extraction. If this is the case, invest in the ability to make new applications - templates, shared libraries, recipes for onboarding and integrating. It will only get harder as time goes on to pull out anything meaningful from the spaghetti you're otherwise making.

**Clean interfaces** will ensure that each application and system don't get entangled with each other, retaining their ability to change and be released independently. Highly coupled components have to be changed and released together, leading to delays and with a higher possibility of bugs. These interfaces also provide great places to hook in test and automation tools. I've seen entire systems driven through Selenium tests on a single UI, where the majority of the time and flakiness comes from simply setting up the preconditions and the assertions are weak because the outcome is not properly reflected in the UI.

**Automation** of all the things. Some of the most valuable automation in Big Org isn't technical, it's bureaucratic. At one bank, releasing anything meant lining up five paperwork systems, with a minimum of 5 working days lead time. Doing a release wasn't just a task, it was a Herculean effort (I'd argued it was Sisyphean, since Hercules only had to do his labours once). Multiple people's entire jobs were just for farming the release process, and when two of them left some of that job landed on developers, including me. My first attempt took four days. I was trying to get to weekly releases and remain a developer, and this clearly was a blocker, so I did the developer thing and automated it: an app to track releases, drive Jiras, prefill email templates for the steps needing a human, creating wiki pages through an API, filling in internal forms with Playwright driving a browser. It took a fair amount of effort, but I got the work down to about 20 minutes and it scaled across multiple applications and teams. It strangely became the thing I became best known for, even though it was just a tool I needed to do my main job in a reasonable way.

*[COMIC: five bureaucratic forms and systems all needing to be filled in at once by one exhausted developer]*

None of these things are easy or quick. They take time and dedication, so pick your battles, have a clear idea of what you want and why you want it and then see it through.


## AI

AI deserves its own section because it's undoubtedly the biggest change the software industry has ever seen. It's strange, because new technology in Big Org normally moves bottom-up against resistance - developers use something outside work, see the advantage, then have to fight the policy to bring it in where the default answer is always no. AI inverted that: enforced from the top, "you have to use this", whether people wanted it or not. None of these organisations is clear on how much value they're getting from it, but I bet they know exactly what it's costing. I suspect it's a mix of fear of being left behind their competitors and everyday exposure to AI, where the results of vibecoding a simple app get taken on faith as extending cleanly to the complex systems inside a Big Org. In these systems "typing was never the bottleneck". Although I personally find AI to multiply my output quite effectively, I struggle with detachment from the code. My solution is to double down on my mental model - it has always been how I think of the tens of thousands of lines of code that I wrote, and extends to the hundreds of thousands that AIs will write for me.

## The survival toolkit

**Emails** will attempt to drown you. Invest time in email filters to find the signal in the noise and make the best use of your time.

**Meetings** abound. If a meeting doesn't need your input and its output doesn't affect you, politely remove yourself. If a meeting invites your whole team but only requires a representative, send one person who reports back.

**Prepare** for meetings, too. In the land of opinions, the one with hard facts (and diagrams) is king.

**Empathy** put yourself in someone else's shoes. What motivates them? What frustrates them? This will help you understand what they want from you.

**Seek first to understand, then to be understood** because no one knows everything.

**Failures will happen** what matters is that you do what you reasonably could to avoid, mitigate and prevent them recurring.

**Don't boil the ocean** Big Org's todo list is infinite, and trying will burn you out, so focus on the highest-impact things you can achieve.

**Automate** what you can, not just for your own convenience, but so the knowledge becomes codified and the process becomes scalable.

## Leave it better than you found it

None of this fixes Big Org. Nothing will, and that's fine - it isn't your job to fix it single-handedly, you shouldn't try. What you can do is build your own mental model and share it generously, automate the things that grind people down, choose one or two things to make a really positive change to, and leave everything you touch a little better than you found it.

Do that consistently enough, and you won't just survive Big Org - you'll actually be glad you were there.
