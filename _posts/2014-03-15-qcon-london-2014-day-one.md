---
layout: post
title: "QCon London 2014 Day One"
description: "The first day of QCon London 2014 with opening keynote from Damian Conway, talks from Daniel Schauenberg, Damon Edwards, Graham Steel, Dave Farley, Michael Nygard, Ola Ellnestam, and closing keynote from Tim Bray"
category: 
tags: []
---
{% include JB/setup %}

This post is a coagulation of my notes from the first day of QCon London, so it's a bit long. Use the links below to jump to the different talks.

- [Opening Keynote - Life, The Universe And Everything](#opening_keynote)
- [Development, Deployment & Collaboration at Etsy](#etsy)
- [Devs Programming Ops For DevOps Success](#devops)
- [How I Learned To Stop Worrying And Love Crypto](#crypto)
- [The Process, Technology and Practice of Continuous Delivery](#cd)
- [Exploting Loopholes in CAP Theorem](#cap)
- [DevOps At A Small International Bank](#devops_bank)
- [Does The Browser Have A Future?](#browser)

<br />

####<a id="opening_keynote"> </a>Opening Keynote - Life, The Universe And Everything
*by [Damian Conway](http://damian.conway.org/)*

Damian Conway was back again at QCon this year with the opening keynote, with a very specific topic of 'Life, The Universe and Everything'. For 'Life' he began by describing [Conway's game of life](http://en.wikipedia.org/wiki/Conway's_Game_of_Life) (no relation) and how the cellular automaton can provide a full computational platform. This was an interested suggestion which he backed up by demonstrating how various self-replicating and migrating patterns can be used to form logic gates by combining streams of 'gliders'.

Using the NOT gate, then the NOR, AND and XOR gates that can be created using the cellular automata lets us create a fully Turing-complete computation engine. In fact he demonstrated an instance of the game of life set up by Paul Rendell which created a [Turing Machine](http://rendell-attic.org/gol/tm.htm) out of the game, which was fascinating.

The 'Universe' component of the talk was focused on that most popular of languages: [Klingon](http://rendell-attic.org/gol/tm.htm). Klingon (a synthetic language created for sci-fi TV show Star Trek) was designed from scratch to be unlike human language and uses a typical sentence construct of Indirect Object - Object - Verb - Subject. The I-O-V pattern matches postfix or Reverse Polish Notation making it possible to program in Klingon without brackets. 

This entertaining twist was familiar to last year's conference attendees who saw Damian move from programming in Postscript to programming in Latin. Damian demonstrated some KlingonScript programming, using the Klingon language verbs and the correct declension to write basic methods. Damian also showed both functional programming and object-oriented programming.

'Everything' in Damian's talk started with "let there be light" - Maxwell's laws describing light as an electromagnetic wave and introducing [Maxwell's Demon](http://en.wikipedia.org/wiki/Maxwell's_demon) which posed a thought experiment challenging the 2nd Law of Thermodynamics (that entropy increases in a closed system). Damian then illustrated a cellular automaton implementation of Maxwell's demon as a gate between two areas with cells representing positions which could be occupied by particles modelled as bouncing around the container at various speeds. All written in Perl of course, with some additional code for the quantum superposition (no joke) of a single cell position representing multiple particles passing through. 

The culmination of the talk was a demonstration of the Maxwell's demon cellular automaton written in Klingon. This talk was quite entertaining but seemed to have less of a direct lesson than his previous year's version after which I was left with the message of trying different styles of programming to change the way you think about problems.

<br />

####<a id="etsy"> </a>Development, Deployment & Collaboration at Etsy
*by [Daniel Schauenberg](https://twitter.com/mrtazz)*

Daniel's talk on continuous delivery at [Etsy](http://www.etsy.com) was an interesting one and surprisingly showed a highly performing set of teams working on a mostly monolithic PHP application. Search and photos at Etsy are split out from the main application and use Java, but the main Etsy product is a LAMP stack augmented with [Redis](http://redis.io) and [Memcached](http://memcached.org).

Etsy achieve an impressive 50 deploys per day covering both code and config across a team of 150 developers. Daniel urged us to consider our progress towards continuous delivery with the question "How comfortable would you be deploying a change right now?", which seems a good companion to the classic continuous delivery question of "how long would it take for a one-line change made now to get into production?"

Etsy manage this co-ordination and granular level of deployment through focusing on very small changes, using config flags (feature toggles), communication through company IRC channels and an eagerness not to shy away from deployment. Daniel said "if this is your first day at Etsy, you deploy the site" - once the new start has gotten set up with their development VMs which use [Chef](http://www.getchef.com) to replicate the entire Etsy application stack.

[Jenkins](http://jenkins-ci.org/) is used for CI, building and running sets of tests before a deployment followed by a QA suite of tests and production deployment smoke tests. The 'Try' branch takes your current changes, makes a patch of the diff, applies it on master and runs the full test suite. Build assisting tools based on LXC containers called Bobs are used to build the site (about 400 instances) and mostly used to run the Try branch on developer VMs. IRC commands in the company channels are used to display VM usage and builder status and a Push channel is used to queue deploys and is watched by an IRC bot to manage deployment.

Etsy seems to have put a lot of effort into their monitoring and support processes (probably related to the fact that they're deploying such a large monolithic application) with developers responsible for designing the monitoring for the features they've developed, [statsd](https://github.com/etsy/statsd/) (actually created by Etsy) and logging pumping into dashboards for everything and developers on rotation for support calls for when outages happen. One thing Daniel mentioned was that all of their application wide configuration was composed in one huge PHP file which sounds like it'd need a lot of careful handling to prevent suffering and sadness.

Etsy have a war room IRC channel to discuss outages and do post-mortems after significant incidents which are treated as a learning experience with everyone blameless. They have an ongoing effort of creating a learning culture where knowledge sharing is encouraged via lunch & learn, data centre visits, senior member rotations and their [engineering blog](http://www.codeascraft.com). 

<br />

####<a id="devops"> </a>Devs Programming Ops For DevOps Success
*by [Damon Edwards](https://twitter.com/damonedwards)*

Damon began his talk by talking about the purpose of DevOps as he sees it: to break down silos in the software development stream, to improve time to market by closing the gaps between dev and ops. Damon talked about a dev-initiated transformation of ops, started by having individual developers taking an 'ops first' mindset when working on their code.

An ops-first mindset, Damon explains, means understanding the pressures that ops are under in regards auditing, compliance, availability and security, and to understand what your business' product is in this regard. Ops requirements for features should be first-class citizens and in particular the "-ilities" should be considered as feature requirements. This seems to align with people trying to reframe Non-Functional Requirements as Cross-Functional Requirements that I've read recently, and the focus on how these needs for the system can be tested functionally.

Damon urged us to consider that we are delivering a service rather than just software; to consider the environment in which the software runs, is managed, configured, etc so that our procedures from build to deployment are prioritised - and automated. Testing, monitoring and health checks should all be part of the developer's work when completing a feature and Damon urged us to redefine 'Done' for feature development as meaning 'behaving properly in production'. A feature can be Done but a service isn't Done until it is turned off.

Damon talked about building organisational alignment using Mission Command rather than command and control, and touched on the Three Ways from [The Phoenix Project](http://willhamill.com/2014/01/15/the-phoenix-project/) to see the system as a whole, focus on the flow of work and recognise feedback loops. Damon also advocated continuous improvement as the means to sustain positive change.

Continuous improvement, Damon describes, can be achieved through building alignment in five steps: 1) Socialise the concepts of the goal with the right vocabulary, 2) Visualise the system (value stream mapping, timeline analysis, waste analysis), 3) Picking metrics that matter (e.g. cycle time, quality at source, Mean Time Before Recovery), 4) Identify experiments to perform, measured against the baseline, 5) Repeat steps 2-4.

Damon also talked about establishing a new model for working with ops - describing both what devs want (clarity, room to work, stable & predictable platform) and what ops want (their needs considered earlier in life cycle and confidence in the system). He suggested replacing queues & ticketed requests with self-service interfaces à la AWS control panel to prevent ops from becoming a blocker and to reduce turnaround time. Damon encouraged rehearsing deploys, ensuring everyone tests all stages using the same tests and also a typical deploy pipeline of [git](http://git-scm.com) - Jenkins - [Nexus](http://www.sonatype.org/nexus) - [Puppet](http://puppetlabs.com)

<br />

####<a id="crypto"> </a>How I Learned To Stop Worrying And Love Crypto
*by [Graham Steel](https://twitter.com/graham_steel)*

I went along to this talk because I know that crypto is not one of my strong points. I've implemented PKI in systems, basic symmetric and asymmetric encryption and have a decent awareness of security but I'm aware that it's a huge space with a lot going on that I've barely scratched the surface. I thought it'd be good to at least pick something up from QCon that helped my knowledge in this area and particularly in the wake of the [Snowden revelations about RSA](http://www.reuters.com/article/2013/12/20/us-usa-security-rsa-idUSBRE9BJ1C220131220) I was interested to see if that changed security experts' thoughts about encryption.

Graham started his talk addressing this: "The tinfoil hat brigade were right" but follows up with a [quote from Snowden](http://www.theguardian.com/world/2013/jun/17/edward-snowden-nsa-files-whistleblower#block-51bf3588e4b082a2ed2f5fc5) - "Encryption works. Properly implemented strong crypto systems are one of the few things that you can rely on." Obviously the key parts here are the definitions of "properly implemented" and "strong".

Graham then described the typical disconnect in how crypto is used in organisations: the dream scenario of the PM discussing the threats and the engineers and PM working together to consult literature and choose the most appropriate security, versus the nightmare scenario of engineers planning to use some 'fun' crypto tech as their reason for picking security (followed by inevitable explosions). The reality is somewhere in between - the client may end up telling the PM why they have to use certain crypto libraries or implementations (e.g. for interop with legacy hardware or outdated compliance policies) and that constraint being passed on to engineering.

The next part of the talk covered how to judge crypto implementations - what makes a good crypto API? Graham suggested a number of points: to be wary of proprietary implementations that can't be subject to review by the community; support of modern crypto primitives; support for flexible and secure key management; mistake resistance; interoperability. Graham suggested that the mistake resistance one may be controversial but I agree that if we make these tools easier to use and harder to get wrong using sensible defaults and the like, then we're protecting ourselves better.

Graham touched on a number of crypto systems in his assessments, providing breakdowns of each one against his criteria for judgement described above. I'll attempt to give a micro-summary of his thoughts on each one here.

[PKCS#11](http://en.wikipedia.org/wiki/PKCS_11): Standard loose, implementations different. Relies on old SHA-1 hash. Good interop. Not very mistake resistant. Pre-2013 not clear though new versions more modern but contain lots of legacy stuff.

[Java JCA/JCE](http://en.wikipedia.org/wiki/Java_Cryptography_Extension): Standard crypto interface used across many enterprise Java apps. Hardware support limited. API under Oracle control but providers often open (e.g. [Bouncycastle](https://www.bouncycastle.org)). Not very mistake resistant. Support for modern and a lot of legacy stuff, good interop.

[OpenSSL](https://www.openssl.org): Originally just used for TLS and SSL, not used for lots of crypto. Source available but decision making process murky. Contains legacy crypto as well as modern extensions. Minimal key management. Easy to get wrong. Interop ok.

[MS CAPI/CNG](http://msdn.microsoft.com/en-us/library/windows/desktop/aa376210.aspx): CNG slowly replacing CAPI on MS platforms. Proprietary software and most providers closed. CAPI a lot of legacy code. No key management. Plenty of things to get wrong. Not very interoperable.

[W3C Crypto API](http://www.w3.org/TR/WebCryptoAPI): New crypto API for HTML5 apps. Contains mostly modern crypto but despite fresh start also legacy crypto. Some key management though currently WIP. Some efforts to make easier to use (SubtleCrypto vs WorkerCrypto, IV management).

Others mentioned: A quick look at [NaCl](http://nacl.cr.yp.to/) and [Cryptlib](https://www.cs.auckland.ac.nz/~pgut001/cryptlib/)

Graham also listed common crypto gotchas, which was particularly useful to give a novice like me something to check against when working on these things. He mentioned avoiding using legacy modes or weaker algorithms as the default settings for some crypto tools, e.g. ECB mode being used by developers because it has the least params and doesn't ask for an IV to be set up. Graham warned against using improperly initialised random number generators and reuse of stored random values. Graham also warned against blindly letting the app or API handle IV management and also warned about unauthenticated encryption (e.g. forgetting to validate certificates, not requiring HTTPS) to ensure we know we've got a real ciphertext from the expected source.

Graham concluded his talk by advising us to use mature, open, checked protocols rather than making our own. He suggests that we favour open API standards over proprietary ones and avoid common pitfalls and legacy defaults. He finished by advising that we get our security choices and implementations reviewed by a third party - "it's easy to write crypto that *you* can't break" (which strikes me as a logical extension of one's inability to even proof-read one's own writing!)

<br />

####<a id="cd"> </a>The Process, Technology and Practice of Continuous Delivery
*by [Dave Farley](https://twitter.com/davefarley77)*

Dave Farley is one half of the pair who literally wrote the book on Continuous Delivery (CD) so I thought this talk would be good. Early and continuous delivery of valuable software is the first principle behind the agile manifesto and represents a holistic approach to development: from concept to production. Dave started his talk by going over the basics of CD and then followed up with principles and practices.

Why should businesses embrace CD? In order to reduce the feedback loop between business idea and customer reaction; in order to iterate on value faster. CD brings out the pain; the slow, inflexible, risky, costly parts of the traditional software life cycle to address these issues. CD uses lean thinking to deliver fast, build quality in, optimise the whole system, eliminate waste, amplify learning and empower the team.

This is done, in theory, through smart use of automation - through creating a repeatable, reliable process for releasing software beyond just tooling. In order to create this process you must automate almost everything and keep everything under version control. If some part of the deployment process hurts: do it more often and find a way of making it better. 'Done' no longer should mean 'code complete' or 'tested' but released to production. Dave advocates making everyone involved responsible for the process and encouraging a culture of continuous improvement.

Dave described some assisting practices: only building binaries once and promoting rather than rebuilding to eliminate the possibility of variance; using precisely the same mechanism to deploy to every environment; smoke testing your deployments; and stopping the line if any part fails.

The example process he gave was by now familiar: Source control for all project code linked to a continuous integration build. An artifact repository for build binaries output by CI build. Acceptance testing, exploratory testing, staging environment testing and promotion to production.

What I found particularly interesting was that Dave mentioned that when he coined the term 'deployment pipeline' he didn't intend it as a single-stream like a huge oil pipeline, but more like process piping. He illustrated this by showing the deployment pipeline as a star-shape rather than a line, with performance tests, exploratory tests, acceptance tests, staging tests all running in parallel on an artifact. A deploy would only proceed once all test suites had tagged the artifact as passing.

This method of running many types of tests in parallel and tagging the artifact as having passed tests means you don't need to wait for an artifact to finish acceptance testing to start performance testing or exploratory testing. Obviously you can kill the cycle if any one stage fails if that's what you want, but that simple shift in perspective makes it obvious that there is a lot more room for parallelism in the build and test part of the pipeline, potentially further reducing the time between idea and feedback. Dave advocated using many virtual hosts to run acceptance tests in parallel in order to try and keep test time constant when adding new tests.

Dave described how using this system they had no bugs identified in production for the first whole year. The cycle time in an emergency release was only an hour end to end, with no stages skipped. Dave recommended writing unit tests for bugs found in later stages rather than adding further top-end acceptance tests in order to keep the build fast. I agree and think this is a great way to keep test coverage up and have a confident regression test suite without [making your testing top heavy](http://willhamill.com/2013/08/12/automated-testing-and-the-evils-of-ice-cream/).

<br />

####<a id="cap"> </a>Exploting Loopholes in CAP Theorem
*by [Michael Nygard](https://twitter.com/mtnygard)*

Michael Nygard began his cheekily named talk with an explanation of [CAP theorem](http://en.wikipedia.org/wiki/CAP_theorem). The short explanation for those who can't be bothered to click through to Wikipedia is that consistency requires all nodes in a distributed system to agree on all values, availability requires that a request arriving at a node will be given a response, and partition tolerance requires that some subset of messages between nodes will be lost if the system is to remain active (otherwise the entire system goes down when one node goes down). 

Broadly, we want to keep our distributed system alive if one node fails so we typically don't bargain with the P part and as a result we end up having to pick two between C and A. As CAP theorem has been mathematically proven, we can't have all three on an asynchronous message passing network with fallible messages (such as the internet) so we either pick C&P and lose some A, or A&P and lose some C.

Michael's talk acknowledged the strict proof of CAP theorem but interestingly discussed how we can skirt around the edges - how we can try and pick perhaps looser definitions of availability, or deal with inconsistency, or perhaps swap between C and A in some parts to try and have the best of all three. Michael proposed ten loopholes, some joking and some serious, to try and tackle the problems that CAP theorem presents to reliable distributed systems.

The first was a write only system, without reads, using a distributed commutative operator (e.g. +) as the only method of interaction so that atomic and linearisable history was trivial. Unfortunately as a write-only system this was clearly a joke option! 

The second proposal was immutability - write once, no rewrite, no variable reassignment. Inconsistent reads are impossible as you either receive null or the expected value and as a result state is much easier to reason about. This option is quite attractive in some programming models and can help deal with the synchronisation problems in multi-threading.

Michael's third proposal was for a looser definition of consistency, not as strict as atomic and linearisable but like database transaction modelling. A temporary inconsistent state is experienced but so long as it is only observed as consistent we can be satisfied about the data. [CRDTs](http://hal.upmc.fr/docs/00/55/55/88/PDF/techreport.pdf) (pdf link) - Commutative Replicated Data Types were discussed as a means of eventual consistency.

The fourth proposal was about splitting networks into availability zones when network partition happens and to simply live with the split until a resolution. The fifth took this a step further and suggested a 'core' region with a focus on high consistency and a 'nebular' outer with eventual consistency, e.g. ACID RDBMS for core and Riak in nebula. Michael for this option gave an example of an ebay-like web store splitting functionality into different areas, with A&P for item display but C&P for bid history.

Options six and seven were 'stop building distributed systems' and 'get a better network'. The former being obviously the joke proposal and the second being ruled out due to difficulty and ubiquity of existing networks. The eighth was to use GPS clocks to sync node time in order to relinearise messages - which sounds esoteric but is being developed by Google - check out [Spanner](http://www.infoq.com/presentations/spanner-distributed-google) for a bit more on this.

The ninth option was to redefine availability (classic consultant answer) to consider the system available until partition happens and then turn off availability to prevent edits during partition. The tenth option, touched upon in the third is that the system can pass through undesirable inconsistent intermediary states so long as the observer only interacts with the data during consistent states.

Overall, Michael's point in this talk was to get people to think about CAP and how it applies to their systems. There is no loophole to CAP, but too many people labour under [the fallacy that they don't need to consider network partition or consistency conflict resolution](http://en.wikipedia.org/wiki/Fallacies_of_Distributed_Computing). You should consider the implications of different definitions of C, A and P. Pick the right one for your system.

<br />

####<a id="devops_bank"> </a>DevOps At A Small International Bank
*by [Olla Ellnestam](https://twitter.com/ellnestam)*

Olla talked about his experience at a small online bank responsible solely for loans and savings, and their journey towards DevOps over the last number of years. The bank had a very small number of staff, a well understood architecture and three main values in system development: minimalism, pragmatism and holism.

Olla described the small business that he worked in having a close relationship with the users of the software. The domain expert made decisions based in business impact, e.g. "If we don't delay this release it will cost us $20k tomorrow, so we will delay it". The team focused on doing just the minimum to meet the business' needs and their close interaction allowed them to break down typical communications barriers. "I need an estimate for X" becomes a cue for a longer conversation between the developers and the business rather than just an estimate.

Olla's team went from doing incremental builds to full builds with a 10s revert window, then added interaction tests, smoke tests and better test coverage throughout the application and eventually brought their build process down to three steps by iterating on the pain points. They avoid destructive DB changes so that they can always rollback in case of failure, though interestingly claimed that they didn't have the time to focus much on automation, which seems to me like an investment decision should be made about the time involved.

During the three years of evolution of the process they moved to a single-artifact release and migrated from svn to git (initially painful but soon beneficial) and expanded the business to take on additional account types. One particularly significant thing that Olla mentioned was how the developers suffered when a business decision was made to move them from 3 floors away from the business to 3 blocks away. The communications overheads and the tiny instances of friction in making decisions and understanding needs reduced their effectiveness until eventually the development team were moved back in, infact into the same room as the business team and with much better results.

In 2010 they went from deployment decisions of "let's schedule a date" to "let's use the lunch break" in 2012, and in 2013 to a status quo of "can you pause what you're doing for 30 seconds" before new functionality could be delivered to the business.

<br />

####<a id="browser"> </a>Does The Browser Have A Future?
*by [Tim Bray](https://twitter.com/timbray)*

Tim Bray's closing keynote on the first day inverts [Betteridge's law of headlines](http://en.wikipedia.org/wiki/Betteridge's_law_of_headlines) asking if the web browser has a future in our interactions over the internet. Tim's talk was curiously not based in slides but in browser tabs. Every new 'slide' was in the next tab over, which was different but also useful for Tim to demonstrate many screengrabs of websites during the presentation. The fact that he didn't close each tab as he was done with them drove me a little mad though.

Tim began his talk by describing how we're currently in the golden age of server-side programming. Between Rails, Django, Node.JS and others we've got a lot more at our disposal than just the post-90s nuclear winter of the choice between Java and .Net. Server side programming is easier to reason about and has great testing support - unlike unit testing mobile client side code.

Tim briefly talked about functional programming, showing love for Erlang and giving a demo of Go to lookup mail provider based on a supplied email address. Tim said that functional programming may be the way of the future as Moore's Law is held now not by making faster chips but by adding cores and parallelism to CPUs. Functional programming provides a paradigm with better support for parallelism and without shared state to cause the typical synchronisation woes.

The trend towards mobile is real, with 'mobile' devices becoming soon the most used way of interacting with the web. Tim pointed out the tension between mobile web development and native mobile development by illustrating the gap between the quality and support for SDKs like Cocoa Touch and Android SDK and the relative jungle out there for browser compatibility fixes and shims and widgets making up the difference in experience between client programs. 

The migration to mobile however, Tim claims, has not been 100% positive for users despite the features we have made available for them, as apps can't be indexed, bookmarked, archived and require installing and granting permission to device features and local user data. Doing it right on the mobile web, with a focus on simplicity, produces a much more pleasing experience for browser users be they mobile or desktop, and Tim called out the New Yorker and Medium as good examples of this purity of design.

Tim concluded his talk by suggesting that though times are hard for the browser and web development, it's not going away any time soon. The only difficulty may be for us as developers as the money and glamour moves into the native device space, given the power and customisable experience that dedicated devices can provide. Tim finished with a tease of the capabilities of a [Project Tango](https://www.google.com/atap/projecttango/) device that he had managed to get his hands on - cool stuff!

