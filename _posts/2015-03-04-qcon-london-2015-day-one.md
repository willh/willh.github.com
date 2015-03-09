---
layout: post
title: "QCon London 2015 Day One"
description: "Conference sessions from the first day of QCon in 2015. Talks from Rebecca Parsons, Peter Pilgrim, Adam Tornhill, Colin Garlick, Rachel Laycock, Mike Pearce and Betty Enyonam Kumahor"
category: 
tags: []
---
{% include JB/setup %}

Another year, another QCon. I'm glad this is becoming a bit of a tradition for me, because I find the conference very interesting and valuable! Another QCon day one roundup post, so the post is a little long; use the links to jump to each talk (or read it all, you wonderful person you).

- [Microservices and evolutionary architecture](#microservices)
- [Scala in the enterprise](#scala_enterprise)
- [Treat your code like a crime scene](#crime_scene)
- [An architect's world view](#architect_world_view)
- [Adjusting your architecture](#adjusting_architecture)
- [Cake drive development](#culture_moo)
- [Software tales from the continent](#africa)

####<a id="microservices"> </a>Microservies and Evolutionary Architecture
*by [Rebecca Parsons](https://twitter.com/rebeccaparsons)*

Rebecca Parsons is the chair of the Agile Alliance and [ThoughtWorks](http://www.thoughtworks.com)' CTO and had the first presentation of the day giving a view of microservices and the direction they lead us towards: evolutionary architecture. This paved the way for quite a lot of the rest of the conference it seems, having a lot of the architecture talks cover this topic in some way, and there being in fact a microservices track on the Friday.

Microservices has emerged as an approach out of the dying light of SOA, after the darker times of enforced 'component reuse' and the unspeakably evil 'integration via database'. SOA, according to Rebecca, got some things right: breaking the monolithic apps into services with separate responsibilities; focusing on integration of services rather than internal coupling; encouraging the acceptance (or at least the discussion) of eventual consistency; and made us think differently about how to separate concerns and reason about the domain,

SOA however, for various $reasons not limited to marketing, hype, and ivory tower types, didn't quite give us the utopia we desired. It led us down the path of creating monster-sized services, focused on the producer of the data and not the needs of the consumers of the data, required complex orchestration, bombarded us with tools that got in the way, and fundamentally made some things harder to change and harder to test.

(*Aside*: To me, this year it seems we're in some sort of transition period between the blowback of the microservices hype and the blowback-blowback, where people stop arguing that microservices is just 'SOA done right' as a means of dismissing it, but instead say "Hey - this is SOA done right!" as a means for giving context, and revisiting some ideas once buried under the baggage that accompanied them. As far as I'm concerned if it means people considering options, thinking more about what specific needs they have and which approach they want to take - and are willing to revisit their decisions once made, then we're going to be moving in the right direction.)

Microservices is an emerging approach, loosely defined on [Martin Fowler's site](http://martinfowler.com/articles/microservices.html), tend to be smaller than SOA services. Conceptually, rather than literally (cue the undying twitter arguments) smaller, and focused around single business capabilities instead of technologies. Microservices need to be independently deployable as they change at different rates, require little centralised management, and isolate tech choices internally from the other services that depend upon it. Microservices are often described as having smart endpoints but dumb pipes. Another very common factor is the lack of (what I call) the BandwagonDB - the single monster database that All The Data lives in; microservices are often responsible for their own data and sharing access or reporting is done via APIs.

More granular services become smaller and chattier but larger services are more inflexible and can suffer from complexity and coupling, so getting the size appropriate is tricky. The implications of pursuing a microservice based approach are heavily weighted towards the operations side: independently scalable inplies great investment into deployment automation and continuous delivery; monitoring for services is crucial; it is impossible to pretend that service failures will not happen; eventual consistency in data needs properly addressed. Flexibility in implementation detail needs balanced against going nuts with the technologies used (probably having a different language for each of fifteen services is not a great path to take). One theme common to many of the day's talks was a maturity in continuous delivery needed as a "you must be this tall to ride" marker for adopting microservices.

Decomposing the monolith: consider [DDD bounded contexts](http://martinfowler.com/bliki/BoundedContext.html) to help split responsibilities and business capabilities. Think about what the consumers for the service need - and if there is no consumer, then perhaps there is no need for that service? Consumer driven contracts for services can also form client tests for the interfaces. Identify the change patterns and places where tight coupling will constrain the rate of change of components. Be prepared during the implementation to combine and split services; to change the architecture as the needs of the business change or as more becomes known about the domain (and be aware that having to change is not a failure of the initial architecture). Rebecca also mentioned [Postel's Law](http://tools.ietf.org/html/rfc760) (loosely: be liberal in what you accept and conservative in what you send) and specifically late binding as a means of reducing fragility in the coupling that will then exist at interface points.

Evolutionary architecture is derived from evolvability of the system as a first class concern during its design. Tolerate and expect change rather than attempting to predict the future and lock in requirements that don't exist yet. Being aware of [Conway's Law](http://en.wikipedia.org/wiki/Conway%27s_law), we can try and design our teams to reflect how we intend the architecture - in particular arranging teams around the services to create for business capabilities.

Microservices is clearly a hot topic right now, but requires discipline, insight into the problem domain and above all is no silver bullet.


####<a id="scala_enterprise"> </a>Scala in the Enterprise
*by [Peter Pilgrim](https://twitter.com/peter_pilgrim)*

Peter began by quoting [Dianne Marsh](https://twitter.com/dmarsh), Director of Engineering at Netflix: "Learn a new language!". I'd like to spend some more time learning new languages as I think it's a good way to learn how to think differently about problems. I went along to the Scala talk because I've mostly been writing Java recently and I thought I'd like to refresh my Scala skills and see how people are using it in bigger companies and the problems they've had with adoption, Java interop etc.

Peter started with some simpler Scala examples of pattern matching, reducing boilerplate compared to Java code, collections operations and Futures for asynchronous method processing. HSBC were used as an example of a larger enterprise that has some Scala adoption along with [GOV.UK](https://www.gov.uk) who use the Play Framework in some places. Peter said that Scala adoption depends on a confident and talented team, and delivering something working was the key to proving viability. The team he had worked with had the responsibility for the end product which used a combination of Scala and Java. Peter said that it was hard to convince some organisations and teams, and that a business case had to be made for the change to the sponsors so that they could get permission to change. I had expected some more information on what types of work they were using Scala for in these organisations, what had made them pick Scala, how they dealt with interoperability and support issues, and specifically what kind of business case they made to convince people.

Next up was a look at Java 8 functional aspects newly available in the latest version such as lambdas, predicates and filters. This was interesting to me as I've been playing around with converting some smaller services that I'm working on to Java 8 to see what kind of a difference it makes when it comes to the more complex code. Peter referred to Java as the mother language, as features implemented in new versions of it will trickle down into old school 'Enterprise' development places even if newer technologies such as Scala and Clojure are off-limits due to FUD and risk. Functions types for producing output, predicate types for filters, .stream() as the gateway to iterators on the built in collections, and passing lambdas or method references all got a look in, which was nice. Java 8 doesn't seem to really have the same power as Scala and Char seems to have been neglected in the primitive-type-workaround classes, however.

Scala was then demonstrated for the same types of behaviours as the Java 8 examples. Personally I really like Scala having used it for a major project in the past and find its functional style very expressive and natural, and these examples were pleasantly concise and punctuation-free compared to the Java 8 ones. Peter covered function composition, partial functions, tail recursion, functions returning other functions and standard map reduce type examples. Futures and Promises were also briefly covered, though I think that should be focused a little more given the power of this in Scala compared to Java.

Peter finished his talk by stating that while Java 8 is new, Scala is here already and can be used as a full-fat functional language as well as object-oriented. Java 8 however changes things by making functional paradigms accessible to a much wider and arguably slower-changing audience.


####<a id="crime_scene"> </a>Treat your code like a crime scene
*by [Adam Tornhill](https://twitter.com/adamtornhill)*

Adam had a really interesting talk; a take on analysis of existing codebases from a forensic angle using psychology to understand where complexities lie, where change happens the most and to plot where issues may arise.

Adam began by reminding us that most of our time spent during development is actually in understanding code rather than writing code. Identifying where the gnarly parts are and improving them is a big deal, though most of our tools for static analysis focus on metrics like cyclomatic complexity which is a fairly naive measure. Intuition based on judging a class or component tends to be better for identifying whether something is complex but that doesn't scale across larger codebases and multiple teams.

Adam gave us a bit of background in forensic psychology to identify how statistical analysis and an understanding of human behaviour is used to plot likely locations of offenders based on the pattern of offences - geographic offender profiling. While hardly exact, this helps indicate areas for law enforcement to focus on to track down offenders. What aspects of this can we apply to our codebases, asks Adam?

In software, we can focus our attentions on hotspots caused by previous problems and use those to identify location of likely next problems. This would give us a new way of trying to choose which parts of the codebase we should refactor or redesign or add further tests and stability around. Adam began this with a CodeCity visualisation of code changes in certain areas to identify the most volatile locations of the codebase. In a case study with 480k LoC and 89 devs working for 18 months Adam displayed the visualisation of the code changes, then augmented this with a projection of areas of the codebase with identified defects. This detail was derived by plugging into source control history as the forensic history of the codebase, using some [tools Adam has developed called Code Maat](http://www.adamtornhill.com/code/codemaat.htm).

This led us to identify that only 4% of the codebase contained 72% of the reported defects, and we can see that certain areas which are much more likely to change have a history of defect incidence. This intelligence can be used to make decisions about stabilising or redesigning aspects of the codebase, as we pre-empt defect hotspots.

Adam's next part of the talk focused on temporal coupling: areas of the codebase that frequently change at the same times. This can identify areas that are not just coupled together by explicit coupling but also those areas that change at the same time due to the copy and paste design pattern. Components that are temporally coupled require co-ordination and collaboration between the people working on the changes.

The second hit of the conference on Conway's Law appeared next, as Adam graphed the dependencies between the components in the codebase and the people from different teams who worked on the different areas. Areas in the codebase that were changed mostly within the team areas identified shared context and areas that required change across teams identify more difficult cross-team comms. 

Adam described how a team of 6 were scaled to 25 to try and get a large amount of upcoming work done in a quarter of the time (elephant in the room being project management evidently not having read The Mythical Man-Month). The comms pathways in the codebase were completely interdependent and cross-team collaboration was strained, code quality was down, complexity was up and merge conflicts became very painful. Being aware of Conway's Law, at this point we need to decide either to change the product architecture or the team structures to address this. 

Adam's stats demonstrated (as we all know and routinely ignore) that quality was negatively correlated with the number of developers on the project. The main developers for each component area were identified by visualising the changes made across the codebase, to create a knowledge map of the people who know the most about the product. The subsystems of the codebase which had frequent changes from multiple teams have multiple reasons to change, so may form the first candidates for splitting up into discrete components. Adam also illustrated how to identify abandoned subsystems - areas of the codebase which were mostly maintained by people no longer with the project and which can be risky to change without detailed knowledge.

In the future, Adam wants to see more advanced behavioural analysis of the code using these kinds of tools, to give dynamic analysis such as "5 people changed this class this week" and possibly even recommendations "people who changed this class also changed XYZ" - these would be useful to give people an idea as to what impact their changes may likely have or which areas they need to know about.


####<a id="architect_world_view"> </a>An Architect's world view
*by [Colin Garlick](http://www.softed.com/Staff/ColinG.aspx)*

Colin began his talk by outlining the structure of the architectural world view he wanted to describe: values leading to principles which are implemented by practices. The analogy given was how the agile manifesto states core values, and is backed by more specific principles and then implemented with particular practices. So without getting as prescriptive as practices, Colin told us about the values that he thought a conscientious architect should have and the principles they inform.

The values of an architect as Colin describes them are as follows: the customers of the architect are both the business and IT; an architect is interested in the big picture (conceptual integrirty, as Fred Brooks puts it); leadership and humility - specifically being an enabler of the system rather than the boss; teamwork and an understanding of the types of people involved in the team and their needs (Myers-Briggs given here as an example of differences between different archetypes of persons); and finally the integrity and consistency to warrant the trust invested in the architect to deliver.

Colin described next the principles by which he thinks these values should be applied to real-world situations. Communication is important to understand the business and to persuade the people you work with, in a cycle of listen -> observe -> design. This reminded me of the principle from the Toyota Production System of *[genchi genbutsu](http://en.wikipedia.org/wiki/Genchi_Genbutsu)*: go and see how the work is done in order to understand it.

An architect should involve everyone in their work: get buy-in from the team and create motivation by involving them in the designs and in the process. Asking for help from the team is not a sign of inadequacy but a sign of maturity and humility in knowing that a collaborative approach is needed when the people involved may have more knowledge than you on the low-level specifics involved.

Simplicity is an important principle, ensuring that the models created, documents generated etc are done for a specific audience and purpose rather than for their own sakes. Injecting patterns into solutions adds complexity rather than simplicity - less is more. Colin then shared with us a good quote from [Tony Hoare](http://en.wikipedia.org/wiki/Tony_Hoare) "There are two ways of constructing a software design: One way is to make it so simple that there are obviously no deficiencies, and the other way is to make it so complicated that there are no obvious deficiencies. The first method is far more difficult."

The next principle Colin talked about was just-in-time design. Delayed decisions are made with more knowledge about the situation. Deferring decisions to the last responsible moment allows us to investigate and try and attack the assumptions we would make. Decisions that are easy or cheap to change can be deferred most easily. This topic to me links quite well with creating options to allow us to defer decision making, [as I've blogged about before](http://willhamill.com/2013/06/12/fear-of-commitment-you-need-options/).

'Deliver working solutions' was Colin's next principle. This one seems obvious once you've said it, but given our industry's history of failed solutions and our habit of tracking progress with documentation produced or gates passed and not working software, it merits being specifically stated. Proving your proposed architectures and designs; demonstrating that you have carefully invested the project sponsor's money is important to keeping people on board and creating value for the business - the real purpose of any software project.

An architect should also keep learning; using retrospectives, lessons learned sessions and the likes to find out how the architecture or design you proposed actually fared in the real world. Find out what happened when the decisions you made and plans you set were actually carried out by teams, and how the implementation panned out in reality. To me this principle seems to be present because of a traditional divorce between planning and implementation; an artefact of architects who are not involved in the actual carrying out of their designs. In my opinion this is a Taylorist legacy of the division of labour between thinking and doing, but that's a topic for another day...

Quality should be a main consideration of the work of an architect - planning for testing and verification of the assumptions is important. An architecture that does not consider testability is usually not a good architecture. Know when 'good enough' occurs for your work, and try to attain this balancing point in ensuring you have built in enough quality and not over-egged the pudding.

Managing change and complexity was Colin's final principle, something I think is even more important as architects, teams and businesses embrace an agile and iterative way of working. Expect that your architecture will need to change as we find out more about the problem domain. Don't try and prevent change or pre-empt future needs, but create systems where changing your approach or throwing away parts of the architecture can be done if needed.

Instead of prescribing individual practices to underpin these principles, Colin finished by describing a series of antipatterns - practices to avoid. I've briefly listed these below:

- 30,000 feet and climbing. Too high level and no low level context to guide detail decisions.
- Real world disconnect. Architects need to know the real life implications of their designs.
- Detailed modelling. Losing sight of the big picture by getting caught in details.
- Gold plating. Docs and designs should be necessary and sufficient. 
- Buzzword driven architecture. Clear comms and simplicity is more important.
- Ivory tower architecture. Beware the architect who works on his own.
- Perfectionism. Delaying implementation because architecture not ready yet. Instead, assume evolution.
- Over complexity without communication. Tester/BA on the project can't draw the high level design. Good test for communicating understanding.


####<a id="adjusting_architecture"> </a>Adjusting your architecture
*by [Rachel Laycock](https://twitter.com/rachellaycock)*

Rachel Laycock is a Technical Principal at Thoughtworks, and gave a highly animated talk on implementing continuous delivery by adjusting your architecture. Rachel began by describing the scenario when she was brought into a client site and given a demand by a customer exec "We want Continuous Delivery". From working with the client and understanding their environment Rachel's response was "you can't have CD" - not a satisfying answer for an exec who wants to get to value. When working with the client and their complex codebase, Rachel came across a lot of the aspects of ["you must be this tall to ride"](http://martinfowler.com/bliki/MicroservicePrerequisites.html) barriers to entry of a microservices architecture and implementing CD. Three of the main things she learned were the implications of Conway's Law, the importance of keeping things simple, and evolving the architecture.

Conway's Law (the third hit on the first day of the conference!) results in organisational silos being reflected in architectural divisions. A front-end team talking to a middleware team and a DBA team will likely generate a classical three-layer architecture. Being aware of this is the first step to addressing the design that is implied by having these knowledge silos. Rachel quotes Conway's line "the design that occurs first is almost never the best possible" to evoke the need for adjustment and realignment of the architecture. Rachel also quoted [Michael Nygard](https://twitter.com/mtnygard) from: "team designs are the first draft of your architecture", from his book [Release It!](http://www.amazon.co.uk/Release-Production-Ready-Software-Pragmatic-Programmers/dp/0978739213/)

The 'big ball of mud' architecture often results because expediency in releasing the system is focused over a clean and evolvable design. More code is added as more features are rushed out the door, increasing technical debt as no slack exists to preserve or improve quality as we go along. Big coupling problems happen in the codebase and the components in the design are pulled tighter together as this happens, which leads to inflexibility in operation. Rachel gave the example of an airline business whose retail site crashed during high load after the [Eyjafjallajökull eruptions in 2010](http://en.wikipedia.org/wiki/Eyjafjallaj%C3%B6kull#2010_eruptions) - a bad enough incident for any business but in this case the retail system was coupled via the database to the boarding system, taking this out of action and leaving angry passengers stranded at the airport. I always find it interesting to hear of incidents like this when bad software design brings real-life consequences far beyond the imagining of the development manager who is pushing back on requests for time to refactor or redesign. This should give us some food for thought the next time we wave away concerns about technical debt!

Rachel describes the pain of software architecture as dealing with the tension between striving for low coupling and high cohesion. Attempting to mitigate this on the big ball of mud systems means identifying the seams and interfaces between areas of different behaviour and writing tests around those boundaries to allow us to safely separate the components from each other. Rachel also described the [Strangler Pattern](http://www.martinfowler.com/bliki/StranglerApplication.html) to begin replacing parts of the older system and redirecting functionality to newer, cleaner components. 

Rachel then went on to discuss the aspects of a microservice architecture that can mitigate against these issues. The monolith tends towards complexity, dubious reusability, slow and hard to change systems which are difficult to deploy or understand in their whole. [SOA](http://www.infoq.com/news/2010/11/SimpleIT) introduced boundaries between services, contracts for service-client interactions, and autonomy between services. SOA got breaking up responsibilities correct, also introduced the business to preferring [BASE](http://queue.acm.org/detail.cfm?id=1394128) over [ACID](http://en.wikipedia.org/wiki/ACID), and directed us to focus on integration between services rather than coupling. However what SOA tended to lead us to (maybe not by principle but by the consultants, vendors and salesmen associated with it) was reducing change, missing Conway's Law and building über services while keeping the architecture as a grandiose and abstract thing.

Microservices don't solve all of these problems for you, but pick up some of the important principles from SOA: making boundaries explicit (often using DDD bounded contexts); preferring eventual consistency and BASE over ACID transactions (and starting the wider discussion about CAP theorem and distributed systems that we've been avoiding); choreographing services instead of orchestrating them by ensuring services report on their own health, check downstream dependencies and handle faults more gracefully; standardising on integration patterns and protocols rather than the languages and platforms for the services; and paying more attention to coupling so that when it happens it does so at the integration points and not inside the applications so therefore more explicit and coarse grained.

Rachel described that what this tends to mean is that Alastair Cockburn's [hexagonal architecture pattern](http://alistair.cockburn.us/Hexagonal+architecture) is somewhat resurgent in terms of how we consider application components interacting with each other. Things to watch out for when moving to microservices include distributed transactions and an understanding of the domain (as services should split along domain boundaries and not technical ones). Rachel says that we don't need to microservice-ify everything; that maturity and competence in continuous delivery is an important pre-requisite, and that automation and close collaboration with operations are very important to help manage the overheads of going from single monolith deployments to deploying, operating and maintaining many services.

Rachel finished off her talk with calling for an appreciation of evolvability in system architectures. You don't need to design for Google scale now, but you should design for the ability to be changed. Architecture of the system is the things about it that are hard to change. The parts these are usually correspond to -ilities and bigger decisions made that can't be unmade cheaply or quickly; to identify where these decisions are you need to be talking to the customer about their scale, security, business needs, and future direction. Creating an architecture where components can evolve separately, with less constraint to change, is more important than trying to predict an unknown future. Areas which need to change most often are likely to hide the most complexity. Putting more emphasis on the testability of these areas and treating the testability as a top level requirement of the architecture will result in a higher quality system.


####<a id="culture_moo"> </a>Cake driven development - culture at Moo
*by [Mike Pearce](https://twitter.com/mikepearce)*

Mike is a development manager at [Moo](http://www.moo.com) (that place that does the nice business cards) and described the journey that Moo has taken as a growing startup in addressing greater demand from the business and preserving a quality engineering culture.

Mike described how a few years ago Moo was facing troubles internally with meeting the needs of the business to release new products to market quickly - the teams were suffering with long cycles and many handoffs during the release. Initially the response to this was to perform post-mortems to identify issues and suggest ways to address them (which is a good idea). The first outcome was the creation of a centralised project delivery department which would determine processes and procedures.

Mike admitted that this was not a good solution, as taking the decision making ability away from the people doing the work did not result in highly motivated people working faster together. The next approach to this was to create a humorously titled 'Committee for Work Domination' as a cross-business forum for direction of the projects, but this attracted too many cooks and did not have sufficient momentum to result in useful change. Moo next took the approach of creating an anonymous staff forum for people to raise issues and submit their suggestions to improve the business. All staff were encouraged to contribute to this, and they found out as a result that most people in the organisation did not know where the business was going, with whom they were going there, or even how they were to achieve it.

As a result of this, and the friction caused by trying to blend traditional management with agile development, the teams were dissolved and reformed into cross functional groups responsible for specific business areas/products. The news teams, called crews, had responsibility for making a new cocktail and hosting an event to welcome each other into the new form of the business - this seems to me like a good team-building exercise and an important way of having the new teams gel once instead of just dumping them all back into the daily grind. Crews were given specific business-aligned goals for their areas of work, were allowed to create their own workflows and were not forced into homogenising with the rest of the company. Autonomy in how the crews accomplish their goals is a powerful factor of motivation.

Mike then revealed that most crews had stopped doing formal estimation of work items - instead of producing estimates for each item and planning an iteration, the crews moved to a flow based system, doing planning as needed and working to improve the product backlog. The business don't care that you are not doing detailed estimates for each piece of work when you can prove that you are releasing new working software on a regular and reliable basis. Product managers from the crews were mediated when they clashed by a crew lead representing the overall business goals.

After the reorganisations, the smaller cross functional crews had better decision making as everyone needed to understand how they can release working software was embedded in the teams. The development manager role is being replaced with a platform manager, someone with vision across the teams and who can help balance doing things fast with doing things right. Another role added was the 'people engineer', combining HR responsibilities with the tech team lead responsibilities.

In day to day work terms, Mike described the culture in Moo as being focused on teams aligning their releases with a fortnightly release train. This currently causes some problems with co-ordination and ties up testers in regression testing the releases, so I'd be interested in hearing what way Moo tackle these issues as they grow. 'Bug squashing Tuesday' is set aside for people to tackle defects and improve complex or low quality areas, and people in the crews typically use XP practices such as pair programming, regular retrospectives and collective ownership. Moo have an interesting buddy system for on-boarding new people allowing new starts to find their way around and arrange getting set up. Wrapping up, Mike stated that overall they aim to create a culture which empowers people to be proactive to solve problems.


####<a id="africa"> </a>Software tales from the continent
*by [Betty Enyonam Kumahor](https://twitter.com/enyok)*

Enyo took to the stage for the closing keynote to give us an insight into some of the different challenges and opportunities that are encountered in Africa in software development. This was a really interesting session, giving a completely different view to how to enhance people's lives with technology than the standard software company style of talks that filled the rest of the conference.

Enyo described with graphs and maps how Africa is considered a mobile-first and mobile-only continent. Mobile penetration is high with the average person having more than one phone [though it is likely a featurephone] in contrast to a very low uptake of wired broadband internet access, which is typically only prevalent in coastal areas where internet fibre connections join the continent. 

Voice content and SMS based services are more popular, forming the majority of traffic on mobile networks, with data use very low. Interestingly, Enyo answered a question from the audience about low smartphone uptake and didn't give the "smartphones cost a lot up front" answer I think most people (myself included) were expecting. Smartphones cost more initially but cost a lot to operate, as they must be charged every night. Not every person has on-demand access to reliable power, so charging would require going to somewhere a diesel generator is being operated. The cost of fuel has gone up considerably in recent years so this is prohibitively expensive. 

I found this particularly eye-opening as I'd presumed the barriers were based on smartphone cost, as in developed countries we have ubiquitous access to relatively cheap power. This underlined for me the type of assumptions we make based on our lifestyle and environment that may not apply in developing countries. Another example of this was authentication of users for paid systems being based not on registration and verification of personal info, but in linking to pre-paid scratch cards for payment. Storing user data is a side effect of needing to process certain payment details yet we assume most systems need to start with customer information in order to provide their services.

Enyo stated that it was most important to use design thinking to get the critical context for how the software was actually to be used in order to solve the real problem. One of the side effects of being a developing continent means that few constraints to new systems already exist in this regard - Enyo elicited an "oooh" from the attendees as she deployed the line "we don't have legacy code on the continent"!

One of the examples that Enyo gave about designing systems in this environment was of a hospital moving to electronic medical records (something I've seen a few stories of with from other work we do in [Kainos](https://www.kainos.com/our-work/evolve/) ). Many of the problems they have are similar to hospitals in the UK that still use paper records: missing files, unordered files, duplicates caused by inability to find files, important patient data unavailable to care practitioners. One of the first steps taken was to help organise the piles and disarray of patient data by barcoding the patient files with a reference for sorting and locating them prior to any digitisation process.

The cost constraints for these systems are quite different from those we experience here, with Enyo stating that the shelves pictured in a large, newly organised patient records room having cost more than the manpower and the system to categorise them. Labour is inexpensive and widely available so technologists on the continent are less concerned with replacing people with technology and more about adding value that manual work can't reasonably do. Job creation is also an important aspect of regeneration and development - in the hospital case, older patients resident in the hospital were paid a small reward for finding and returning stray patient files that had been left around the hospital (reminiscent of bottle-bank return rewards).

When the electronic patient record system had been rolled out in the hospital, waiting times reduced from three hours to 10 minutes, which had a knock on effect of spreading the news about better service in the hospital, which in turn meant that more people needing care came in for it rather than ignoring it or going elsewhere. This is a very positive result to see the beneficial social impacts of the technology systems; something my colleagues in Evolve must enjoy!

