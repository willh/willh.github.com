---
layout: post
title: "Antipatterns and Antidotes"
description: "Antipatterns in agile practices and some discussion of means to address them. Taken from my section at the BelTech2014 Agile Masterclass tutorial."
category: 
tags: ["agile"]
---
{% include JB/setup %}

This year I was fortunate to help deliver an [Agile Masterclass](http://www.beltech2014.com/attend/masterclasses/) session during the pre-conference workshops at the [BelTech 2014 conference](http://www.beltech2014.com) alongside [Ian Johnson](http://twitter.com/DeliveryIan) and [Tim Field](http://uk.linkedin.com/pub/tim-field/1b/398/937). One of the sections for discussion was on antipatterns in applying agile techniques and I thought it'd be good to list the prepared material out here as we covered only the most important few based on the votes of the audience.

Each antipattern is listed with a brief description of the trouble that we've seen it cause and some suggestions of how to approach solving them. Each one of these could be worth a blog post of its own but I've tried to simply highlight the pain points and my thoughts about tackling them. Feel free to disagree or to add some feedback in the comments section on what has worked for you when you've encountered these problems.

<br />

- [Non-technical stakeholders dictating technical feasibility or 'solutionising'](#solutionising)
- [Standups as simple status updates](#zombie_standups)
- [Phased sprints, e.g. 'design sprint' -> 'dev sprint' -> 'test sprint'](#phased_standups)
- [Poor quality user stories](#inept_stories)
- [Very long sprints with large stories](#long_sprints)
- [Developers not empowered to talk to business, give estimates, etc](#developers_not_empowered)
- [Estimates produced by a Product Owner, architect or other single person](#single_person_estimate)
- [Multipe Product Owners working on the same product](#multiple_product_owners)
- [Stagnant technical practices](#no_xp)
- [Not paying off technical debt](#tech_debt)
- [No retrospectives](#no_retros)
- [Turning people off with too many radical changes at once](#change_burnout)
- [Ultra-detailed user stories](#excessive_detail)
- [The Scrum Master is the boss](#SM_PM)
- [Acquiring an agile process and never changing it](#fixed_process)
- [Using an 'agile tool' to define the way of working](#agile_tool)
- [Product Owner == Scrum Master](#SM_PO)
- [Product backlog determined at outset and forever fixed](#fixed_scope)
- [Product Owner without authority ("proxy PO")](#proxy_PO)
- [Points mean prizes](#velocity_target)

<br />

####<a id="solutionising"> </a>Non-technical stakeholders dictating technical feasibility or 'solutionising'

This problem we've seen when people are too specific about the implementation in describing user stories or when they've jumped straight into the solution instead of describing the problem and the desired outcome. People get hung up on technical details, for example "as a trader I want an email notification so that I know my purchase has been completed". This detail precludes the ability to meet the user's needs with an SMS, or an in-account notification.

Try and tackle this by ensuring that requirements are stated in terms of an improvement to business capability or some utility for the user rather than the detail of a feature implementation. So to extend our example, "as a trader I want to be notified when a purchase has completed so that I can include the total asset value in my next decision". The goal is for the trader to use this new information in some meaningful way and this is the important outcome, not whether or not an electronic message was sent from one SMTP server to another. In terms of dictating feasibility, we've found it valuable to have a technical person involved with business people very early during story creation to ensure we root out any requirements of "I click a button and ice-cream comes out" and to give a steer on whether the goals are achievable or not.

<br />

####<a id="zombie_standups"> </a>Standups as simple status updates

I'm sure we've all seen or taken part in a Zombie Standup at some point. "Yesterday I worked on logging. Today I'll work on logging. That's it." The standup meeting isn't just meant to be a status update, it's meant to be a means for the team to keep each other on the same page for overlapping areas, problems, blockers, or need of other team members. The standup should help the team plan together for how they will accomplish the goals for the current sprint.

Instead, imagine this: "Yesterday I worked on logging. Today I'll finish the logging and merge it in. There shouldn't be any changes to everyone's current work so long as you reference the same logger class as usual. I'll need to talk to Steve to get the logging config file change made on the production templates." Perhaps if Steve isn't even needed this would still be a little better. It's not possible to give deeply enlightening information 100% of the time but just try and keep a focus on keeping others aware of dependencies and raising your needs as soon as you can.

<br />

####<a id="phased_standups"> </a>Phased sprints, e.g. 'design sprint' -> 'dev sprint' -> 'test sprint'
Sounds a lot like cargo cult agile to me. If you're doing this, what makes your approach agile? The difficulty here is it may be three sprints before you can get feedback from the test to the design. If you've got development separated from testing then you're probably not even delivering working software at the end of each sprint, [which is very important](http://agilemanifesto.org/principles.html).

To try and address this, bring design closer to the developers and include them in this. Bring testers entirely within the development team and have them work alongside developers. Try Test-Driven Development to ensure you're testing code as it is being developed. Ensure that the output of each sprint is a potentially releasable product that you can actually give to your business or your users for feedback.

<br />

####<a id="inept_stories"> </a>Poor quality user stories
User stories that are INEPT: Interdependent, Non-negotiable, Erroneous, Presumptuous or too Technical. Stories without defined personas: "as a user" instead of "as a third-party insurance broker", or "as the business" instead of "as the compliance manager". Bad quality user stories waste time between the developers and the business people as they go back and forth looking for clarification and arguing over details at acceptance time.

Ensure that stories are higher quality with INVEST: Independent, Negotiable, Valuable, Estimable, Small and Testable. Creating personas is a great way of building context in to stories, and can even help when clarifying needs. If a story is phrase like "as the compliance manager" and people are arguing over what would be useful for them - go into the business and find the compliance manager and talk to them! Again, ensure stories focus on the desired impact for that persona and not the nitty gritty details - remember [a user story is the promise of a conversation](http://dannorth.net/whats-in-a-story/).

<br />

####<a id="long_sprints"> </a>Very long sprints with large stories
The reason that sprints are so called is that they're meant to be quick and short. Long sprints means it takes longer to see value and longer to get feedback, and bigger stories means more risk and a bigger impact when something doesn't make it before the deadline. Longer sprints mean more work is integrated and tested less frequently, and less frequent integration and testing means riskier and less frequent deployments.

When integration pains and delays in testing (often caused by larger stories) cause people to suggest longer sprints, push back in the opposite direction. Make sprints shorter and you can integrate and test more frequently. [Continuous delivery](http://continuousdelivery.com/) advocates bringing the pain of integration/testing/deployment forward and doing it more often in order to make it more reliable and easier. [Split larger user stories into smaller ones](http://www.agileforall.com/2012/01/new-story-splitting-resource/) so that work can be delivered more often in smaller batch sizes. Smaller batch sizes reduces the time before the business and user can get something valuable.

<br />

####<a id="developers_not_empowered"> </a>Developers not empowered to talk to business, give estimates, etc
Devs! Huh! What're they even good for? Absolutely nuthin'! If your developers are cooped up in the development team room far away from the business people, not let out to discuss matters with the business and only responsible for "coding", you're definitely doing it wrong. Odds are pretty good as well that your team are looking around for other jobs where they can get involved with the process and are trusted as the experienced and educated professionals they are. Having a BA do the talking to business people and an architect do the estimations for them takes them out of the loop where they are the people to make the most valuable contributions as they're the ones doing the actual work.

Ensure that your developers are giving the permission, means and time to discuss features with business people.  The development team should be trusted and encouraged to work with business analysts, testers, operations staff, architects and so on. Bring the whole team together if possible. Create an atmosphere of safety where a developer can raise queries about technical feasibility, or question the detail of a requirement directly with the business people involved. Giving your team autonomy in their work is a powerful motivating factor.

<br />

####<a id="single_person_estimate"> </a>Estimates produced by a Product Owner, architect or other single person
When estimates are given by one set of people and another set are held to it, it is bad enough, but when there's only one person responsible for producing those estimates. One person alone will not recognise the unconscious assumptions they are making when estimating a piece of work, and their experience and subjectivity will skew the result. This is exacerbated if they are not going to be the person actually doing the work.

Group estimation is more effective at both producing reasonable estimates and raising points for clarification around the assumptions baked into the description of the work. Estimation amongst the people responsible for the work also brings in context and experience of recently completed similar work. Using a method such as [planning poker](http://en.wikipedia.org/wiki/Planning_poker) you can include the entire team (devs, testers, ops) of people who will contribute to the effort. I find the cards or the exact sizing scale is less important than revealing estimates at the same time so that differences of opinion can cause assumptions to be identified. 

<br />

####<a id="multiple_product_owners"> </a>Multipe Product Owners working on the same product
This one seems not entirely uncommon, especially in larger programmes of work, but can lead to a 'too many cooks' situation if each has equal authority. When more than one person is the person who is meant to have final say on the priority of work to be done by the team then quarrels can occur and unity of purpose is broken. It's very important to have one person to be able to make those decisions and provide a single source of truth. Product Owners could attempt to override each other or have 'their' stories prioritised over other product owners' stories.

Ideally, have one Product Owner. Some role occupied by one person who can make the final decision on which features are prioritsed for team work. If this can't be achieved then presumably the product owners have responsibility for different feature areas or business functions of the work - based on these divisions, attempt to split up the priority based on an agreed ratio of work. This may lead to feature teams, with one team and one product owner working on one area of the work. This would be a better approach that trying to divide one larger team's time into X fractions and promising some portion of effort for each set of features.

<br />

####<a id="no_xp"> </a>Stagnant technical practices
You may find that this occurs when an edict has come down from On High to "go agile", and the project or team has responded simply by doing standup meetings and calling their release schedule 'sprints'. [Modern](http://xprogramming.com/what-is-extreme-programming/#simple), [high](http://xprogramming.com/what-is-extreme-programming/#pair) [quality](http://xprogramming.com/what-is-extreme-programming/#test) [software](http://xprogramming.com/what-is-extreme-programming/#continuous) [development](http://xprogramming.com/what-is-extreme-programming/#design) [practices](http://xprogramming.com/what-is-extreme-programming/#coding) are the means by which agility is fostered and grown at the development team level. If you do not have developers writing tests, for example, you will find it very hard to take advantage of the faster delivery rates other teams enjoy.

You don't even need to work in an agile fashion to use most of the practices linked in the previous paragraph. They are now simply considered good practice for developers. You don't need to use TDD on every single feature to gain the benefits of having developers write unit tests. Ensure the development team are trained in these practices and create opportunities for both formal and informal if they are not. Better technical practices will mean a reduction in turnaround time for feature development and a reduction in defects.

<br />

####<a id="tech_debt"> </a>Not paying off technical debt
Technical debt is inertia experienced when trying to change or build on code that results from building up complex implementations, taking shortcuts, ignoring the need for refactoring, or simply the entropy of time and the design changes made since the inception of the system. Martin Fowler has [an excellent article](http://martinfowler.com/bliki/TechnicalDebtQuadrant.html) on types of technical debt which I would not do justice here (it's not just people not bothering to write unit tests).

Technical debt must be paid off when built up to the point where it is causing significant damage to the ability to write new code and react to change. Ideally, following the boy scout rule during ongoing development means that the team will refactor the untidy parts as they go along and try and keep debt down. Steve McConnell [makes the point](http://www.construx.com/10x_Software_Development/Technical_Debt/) that a low technical debt is essentially like slack in the system, meaning that if you need to make some short term decisions that will result in building the debt you've got 'room' to do so when you need to. Trying to convince business people of the need to pay it back may be tricky, however. Consider including some specific refactoring time in user stories to allow work in particularly gnarly areas to clean up around it as part of the story.

<br />

####<a id="no_retros"> </a>No retrospectives
Sometimes teams are plodding along, doing the same process week in and week out and avoid doing retrospectives because it's a waste of time. When retrospectives are seen as a waste of time then you are ignoring the opportunity to improve. 

Retrospectives are a chance to find out if your assumption that everything is going fine and nothing needs changed is even shared with the rest of the team! Giving other team members the opportunity to have their thoughts heard and their suggestions taken on board is a great way to ensure people are empowered and engage with the process. Try mixing the retrospective format up a little if it's getting boring. The [agile retrospectives book](http://www.amazon.co.uk/Agile-Retrospectives-Making-Pragmatic-Programmers/dp/0977616649) has a lot of different suggestions for this. Even if you're at peak efficiency and nothing can be improved, perhaps there are things to be learned that can be shared with other teams.

<br />

####<a id="change_burnout"> </a>Turning people off with too many radical changes at once
Controversial? Maybe. Blinding people with science without giving them exposure to new terms or training for new ways of working is a great way to cause inertia in any agile transformation. Appearing to reject existing shared vocabulary and in particular rejecting existing job titles and responsibilities without a clear migration for those affected is very jarring for those involved. People don't resist change itself, they resist *being changed* by outside forces.

Awareness of new techniques, training for those involved, clear corporate communication as to the plans and the exact impact and meaning on the day to day jobs, roles & responsibilities for the team and the business involved is very important to avoid burnout and too high a cognitive load. Evolutionary change may be more effective and one option to consider here is changing the process piecemeal rather than radically. Sometimes this isn't possible, though, and things just need shaken up! It seems that the argument between revolution and evolution is still taking place amongst the agile community. [David J Anderson](http://twitter.com/lkuceo) makes use of an evolutionary path to agility in the [Kanban Method](http://willhamill.com/2013/11/20/kanban-beyond-the-board)

<br />

####<a id="excessive_detail"> </a>Ultra-detailed user stories
The 300 word user story covering all possible scenarios and all details, so that developers don't need to ever seek clarification on any issue. This often seems to be attempting to solve the symptom of a problem - sometimes that stories are too vague for developers to estimate accurately, or when there has been disagreement over the acceptance criteria of previous stories. This can also be a symptom of reluctance to iterate; that the story writer has to get it exactly right the first time as this is their only chance to define the feature.

Remember, [a user story is a promise of a conversation](https://www.gov.uk/service-manual/agile/writing-user-stories.html) and shouldn't be used to obviate the need for one. The user story should be discussed before planning by a business stakeholder, a subject matter expert and a development team member and an appropriate level of detail recorded based on their agreed understanding of the user need. The story can contain acceptance criteria which should ideally then for acceptance tests, but excessive detail may preclude the ability for developers to make changes based on ongoing development (especially if changes are not allowed once the story is 'signed off' as ready). Embrace iteration and expect that even with great detail and certainty, you are unconsciously making all kinds of assumptions about user behaviour and user needs. Iterating on the features based on real feedback is the best way to meet needs, so encourage writing stories with just enough detail to create a [Minimum Viable Product](http://theleanstartup.com/principles) to test the assumptions and attempt to deliver value so that it can be put in front of real users.


<br />

####<a id="SM_PM"> </a>The Scrum Master is the boss
The Scrum Master assigns tasks, gives the team their marching orders and manages their work rather than coaching them to choose their own work and facilitating removing blockers in the way of their progress. This one sometimes happens when a traditional Project Manager enters the Scrum Master role. The Scrum Master's job is to get stuff out of the team's way so they can best achieve their work.

A good Scrum Master is a servant-leader; they are available whenever the team needs them to take care of external reporting needs, manage ceremonies and ensure team members' dependencies on other teams or parties are followed up. The Scrum Master does all the same coaching, leadership and organisation as a good manager except for actually telling people what to do. The team are within reason empowered to work on the tasks that they choose (of course encouraged ideally to start towards the top of the priority list).


<br />

####<a id="fixed_process"> </a>Acquiring an agile process and never changing it
This one sometimes happens when a parent company or a corporate division dictates that a certain process must be followed and from which must not be deviated. Mandatory steps in a process which are not seen to add value will be worked around, skipped, or fulfilled in a mediocre fashion.

A truly agile process should be owned by the team and customised and evolved over time to suit their particular situation and meet their needs. So long as their external obligations can be met (often with regards reporting progress or dependencies or deadlines to programme level) the internal implementation should be left to the team. If the team are given mastery over their own process to an extent they will be more invested in it. Let the team make adjustments as the result of retrospectives and identify the impact of each change on time to deliver features, throughput and so on in order to take a more scientific approach.


<br />

####<a id="agile_tool"> </a>Using an 'agile tool' to define the way of working
This one seems to me to be related to the previous point. I've heard a few different people complaining that they can't do certain things in their process because their reporting or tracking tools don't allow for it. Some task tracking tools for example don't have the ability to add certain states to a process flow. The process is then constrained and dictated by the tool because of the need for reporting. 

If it makes sense, do it anyway, then fit the tool around it. Remember [individuals and interactions over processes and tools](http://www.agilemanifesto.org) so ensure that the tool you choose fits your current way of working, and won't get in the way if you change it. Assume that your process will naturally evolve throughout the work when deciding how strictly to tie your tool and method of working together.


<br />

####<a id="SM_PO"> </a>Product Owner == Scrum Master
There is a likely conflict of interest between the person whose job is to decide which features the team will work upon and whose focus is on getting the most valuable work out of the team, and the person whose job is the facilitate the ceremonies for the team and get blockers out of the way for them. The Product Owner role is also most likely a full time role, and the Scrum Master is also most likely a full time role, so having one person responsible for both means they will be unable to completely fulfil the needs.

Make the Product Owner and the Scrum Master different people. These are two quite different sets of skills and making one person fulfil both sets of responsibilities is putting them under a lot of strain. The Product Owner should be a business person with good knowledge of the problem domain and sufficient authority to make decisions about the product. The Scrum Master should be someone with good coaching and communication skills. Ensure that both people have had training and clear awareness of the expectations of their roles.


<br />

####<a id="fixed_scope"> </a>Product backlog determined at outset and forever fixed
The fixed scope project causes a number of problems. It assumes that there will be no growth in scope based either on discovery made during the development, or on changes decided by the business caused by getting early market feedback from use of the product. This leads to a scenario where 'change controls' are needed to change the course of the product development which hampers the ability to gain benefits and competitive from the agile process.

This one is less easy to change once contractuals are completed. Avoid committing to a fixed scope of requirements by reminding the customer or business that it prevents their own ability to react to change. Software development is a process of discovery and making decisions at the point of least knowledge means committing to the assumptions made in both technical feasibility and in the utility of features proposed at the outset. Perhaps try and commit to a very short fixed-scope alpha or prototype to demonstrate feasibility and the utility of some features desired by the business. Based on this demonstration they can have the ability to change their minds - and encourage that they would want that ability every week/two weeks/month.

<br />

####<a id="proxy_PO"> </a>Product Owner without authority ("proxy PO")
A Product Owner with no authority to decide priority of items, change features, or make significant decisions about the requirements isn't really a product "owner". A 'proxy' PO or anyone who needs to get permission to make these decisions is not properly empowered to complete the role of Product Owner. This means increased delays on getting business decisions made, and distances the team from a capable decision maker.

The Product Owner must be someone from the business side who is given sufficient time and power to dedicate themselves to making real decisions about the work, and with availability for the team to call upon them to make decisions. Clarification of the detail of user stories or decisions between implementation options presented by the team should be made by someone close to the team and with intimate knowledge of the work that has been completed so far and the impact that it will have on the rest of the work. The Product Owner is the key to meaningful communication between business and developers.

<br />

####<a id="velocity_target"> </a>Points mean prizes
This happens when story points are used as estimates and then the team's velocity as a target for team productivity. The team estimates the amount of story points for the features prioritised and then decides how much work they can commit to finishing in the sprint. Giving the team a target for the story points means they will tend to inflate estimates and game the system in order to achieve the target. Velocity simply correlate to the amount of effort put in and does not necessarily measure important factors such as quality, utility to customers, lead time and others.

Avoid putting too much emphasis on velocity. Acceleration of velocity is an indication as to an improvement of the team's efficiency, assuming that estimates are accurate and point sizes static. If estimate accuracy and sizes remain constant then you should expect minor increases in velocity as the team improve the process and eliminate their own blockers and inefficiencies. As an extreme counter-example, a team whose velocity doubles week by week suggests either that team size is doubling week by week on perfectly parallelisable work with no bottlenecks, or that estimates are way off and the team are incentivised to reach ever higher velocity scores. Consider also adding alternative measures alongside velocity such as an indication of quality (e.g. defect count), qualitative feedback from regular customer insight (you should be getting feedback on your regularly released product after all), lead time from story inception to feature deployment, frequency of release, and other KPIs relevant to the project.




