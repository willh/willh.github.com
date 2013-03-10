---
layout: post
title: "QCon London 2013 - Day Two"
description: "The second day of QCon London 2013 featuring opening keynote from Damian Conway, talks by Glen Ford, Katherine Kirk, Benjamin Mitchell, Dan North, and Gojko Adzic &amp; Lukas Oberhuber"
category:
tags: ["presentations", "agile", "testing", "culture"]
---

{% include JB/setup %}

###Keynote - Instantly Better Presentations
*by Damian Conway*

Damian Conway gave a great keynote presentation on the second day of QCon about how to improve style, delivery and content. I was very interested in this session because it always greatly bothers me when I attend a presentation on something and find that the presenter reads just a huge block of text off his slides, or has text too small to read from the back of the room, or any number of other obvious but often made mistakes. Technical presenters are often guilty of this because they don't get the same kind of training that the slick sales types get, though I've seen salespeople give lacklustre presentations too!

I'm interested in improving my own presentation skills because it seems pretty hollow to be able to point out when someone makes a crappy presentation without being able to do better myself. Practice makes perfect and the better I get with my own presenting the more confident I'll be in it, so I highly value tips from great speakers.

It's easy to improve your presentation greatly by taking the first step of only presenting something that you *actually care about*. The audience can always tell when someone has to stand up and unconvincingly rattle on about something in which they're not very invested. Damian also makes other good points about slide layout (spartan), narrative structure (have one), selecting topics (not searching), and harnessing anxiety to channel it into excitement.

Damian made a [more detailed prose version of his content](http://damian.conway.org/IBP.pdf) (PDF) available on his website, which is very good of him. He is a hugely compelling speaker and skilled orator and as he fairly points out that full time presenting is his only day job, you should consider hiring him to speak for your corporate event or conference :).

____

###People Over Process - Applying It In Real World Software Development
*by Glen Ford*

Glen Ford's talk was about applying the principle of *individuals and interactions over processes and tools* in real terms, and how the impact of considering the human factors involved in development can make a real difference in team performance. Glen began by recounting from his experience as a team lead of a time when he was given feedback illustrating that his impression of how he led the team was different from how the team were experiencing it and that he wished he had been given the feedback sooner. Glen encouraged us to constantly seek feedback rather than waiting for it, and actually apply it to ourselves.

In a high performing team (especially a team with many experienced members) there is often significant inertia to change, so overpowering that inertia really requires making people emotionally invested in change. In order to give your people direction, you need to sell them on the vision and relate your short term plans back to that vision to demonstrate its relevance. Glen said that we must have a stated motivation to work effectively, and that if you can't understand the reason for doing something (in terms of the vision) then perhaps you shouldn't be doing it.

The processes used to guide the team are a set of concepts and not the law; the better your interactions with the people involved then the less you will require the process to instruct or control. This was very much an emphasis of [MacGregor's Theory Y](http://en.wikipedia.org/wiki/Theory_Y) over Theory X. Giving your people the right reasons to do something means they'll usually make the right decision.

____

###Climbing Out Of A Crisis Loop @ The BBC
*by Katherine Kirk*

Katherine began her talk by describing the situation of one of the teams in the BBC working on a high-demand backend media service. When she was brought in after previous managers had quit, she knew that there was a massive percentage of time spent firefighting and a huge gulf between the expectations the team were setting and their ability to deliver, given the quality of the system, the time spent on urgent fixes and communication issues.

Katherine described how her first action was actually to absorb the situation rather than diving in and proclaiming new strategies as some higherups had expected of a new manager. This seems like a personally risky but very wise move, as better decisions can be made with deeper understanding rather than a knee-jerk reaction. She collaborated with the team to understand their problems and their frustration with estimation & planning work that could never all be delivered in the required time, and then ensured that the expectations of the team were reset so that they instead could under-promise and over-deliver.

Planning was reduced and capacity was projected based on a more realistic understanding of what can actually be tackled and how much time must be spent on urgent fixes. Team members were rotated through dev/ops/test/firefighting workstreams on a two-week basis, which I think is a great idea. This spread knowledge around and also reduced the perception amongst the team that some people got to do the "new" stuff and some people just got to fix bugs.

The team used finer grained boards to display more accurate progress - 'done' became two columns of 'development complete' and 'in review' in order to eliminate the typical progress update of "I'm nearly done". Being open and truthful both within the team and in the team's capacity and progress to others was important to improve communication. Katherine also described how they defined all the implicit and assumed parts of the process in order to ensure they could properly track what work needed to go into particular actions. This is one of [Kanban](http://en.wikipedia.org/wiki/Kanban_(development)#Six_core_practices)'s core principles in "make policies explicit".

Katherine's main push was to improve the communication and to try to empower the team that they could solve the problems on their own; that they would essentially become self-managing. A good test of this would be if a manager of the team could take a few days' leave during a week without having to necessarily have a replacement step in for the entire time. A common theme during this talk as with most of the talks on Thursday was of following the [agile principles](http://agilemanifesto.org/principles.html) rather than any particular strict process.

____

###Between Fluffy Bunnies and Command & Control: Agile Adoption in Practice
*by Benjamin Mitchell*

Ben's talk on how implementing agile worked out for him in practice was less of a narrative and more of a series of anecdotes interleaved with lessons learned/points for thought. Ben started by describing an agile team he had led in an organisation that had previously had bad experience with agile, so when running his team they were actually having their standups in secret. I can understand why this was done, in order to ensure the team can actually be productive without a top-down command being used to force them into ineffective practices, but as Ben said, you can't be open and transparent when you're hiding in the stairwell to have a meeting.

Ben described a few of the things he had done to try and encourage open communication; people avoid embarassing or threatening truths so it was important to make negative views discussable. Reducing the barriers to people raising problems was important - for example having the question "what wasted your time today?" being a stock question at a standup meeting gets people being more direct about it. One nice touch was to implement the 'two hand rule' at standup meetings to ensure people are being concise and relevant: if at standup someone is saying something you think too long, detailed, irrelevant, etc then just put your hand up. When two people have put their hands up, the person currently blabbering on will take their issue offline, no questions asked. This is a good suggestion to ensure smoother flow of the standup and prevents it from turning into a 20-minute affair.

Ben had in one team noticed poor morale regarding progress and productivity, which turned out to be because the entire product backlog had been stuck up to the left of the board. This meant that team members looked at their progress for that sprint and at a glance only saw that there was a huge amount of work still to do. I've heard this before on the Agile NYC podcast when a team was depressed by the insanely long and detailed product backlog. I think there are two issues there in terms of the need only being to illustrate the current sprint backlog in terms of glance & go progress on the board, but also a hugely detailed and long product backlog may be a symptom of too much analysis.

When it came to making decisions about the process and the project, Ben said that we should explain the observations and inferences that lead us to make suggestions; say what you have seen and ask what others think about it in order to draw out your own assumptions and to encourage communication. When it comes to negotiating with business owners, it is best to show people rather than just telling them. Demonstrate your progress and negotiate based on the real data to hand. This is surely a very powerful notion - it's much easier to make your point when you can point to hard facts and say "well, here's what we actually have and what we know from this already". This is similar to what has been mentioned about decision making in Facebook, ['code wins arguments'](http://money.cnn.com/2012/02/01/technology/facebook_hacker_way/index.htm).

____

###Accelerating Agile
*by Dan North*

I was lucky enough to attend the pre-conference workshop on this topic with Dan North, which I highly recommend. Dan describes how he went from working in a high performing team and delivering every week to working with a couple of developers in a trading company, where no strict 'agile' process was followed to the letter, code wasn't always TDD'd and despite various other popular rules bring broken they were delivering at an incredible rate (many times per week). Dan's experiences in working with this team led him to describe a number of patterns for effective delivery.

Dan North's material is great stuff and he speaks a lot of sense. One of his previous talks on [Embracing Uncertainty](http://www.infoq.com/presentations/Embracing-Uncertainty) is very interesting and worth a watch.

I took less notes during this session, having already taken some down from the workshop, so I've just made a few bullets under the points that Dan described in his talk:

1. Learn the domain (use BA to educate devs not as permanent conduit)
  <ul><li>Devs sent on same domain course as real business people!</li></ul>
2. Prioritise risky over valuable
  <ul><li>Opportunity cost -  when doing X be aware of every other Y you could be doing and if Y is more valuable, change</li>
  <li>Within MVP, order doesn't really matter so do risky first</li></ul>
3. Plan as far as you need
  <ul><li>Review your planning horizon</li></ul>
4. Try something different
  <ul><li>Assume there is something you haven't tried that could benefit you</li>
  <li>Different languages to get different perspectives, likewise programming styles</li></ul>
5. Fire, aim, ready
  <ul><li>Get something in front of actual users for actual feedback</li>
  <li>Showcase frequently</li></ul>
6. Build small, separate pieces
  <ul><li>DRY is the enemy of decoupled (counterintuitive perhaps but be aware)</li></ul>
7. Deploy small separate pieces
  <ul><li>Make component deployment quick</li>
  <li>Make product deployment consistent</li>
  <li>Make components self describing and environments unsurprising</li></ul>
8. Prefer simple over easy
  <ul><li>Don't always just bring in big, complex things just because it's a one line dependency</li>
  <li><a href="https://github.com/mfoemmel/fig">A cool little dependency/package management tool called Fig</a></li></ul>
9. Make the trade-offs
  <ul><li>build v buy v oss</li>
  <li>Framework v roll your own (e.g logging via System.out.println)</li></ul>
10. Share the love
  <ul><li>Code Reviews - keep quality up, spread knowledge</li>
  <li>Learning lunches</li>
  <li>Great On-boarding</li></ul>
11. Be okay with failure
  <ul><li>Be broad-minded, see bigger picture of business significance of actions</li>
  <li>Think about the product rather than the project</li>
  <li>Progress via experiments</li></ul>
12. There are always 12 steps
  <ul><li>Delivering in this fashion can be addictive!</li></ul>

This talk was great and again I think calls back to an underlying theme for this track of the conference which was about embracing the sense in the agile principles and not just applying process at the expense of people. Some of these things can seem counterintuitive but it's usually when you zoom out and take in a wider context that you realise the greater sense in them. 

For example thinking about the product rather than the project - instead of having two workstream managers arguing over which 'project' is going to pay for something that's of wider benefit, making a more reasonable decision to take one for the team or split it or anything that results in the wider-scope longer-term benefit. I see this sometimes and watching talented and well-meaning people getting caught up in bureaucracy and budget-driven arguments when they need to look past the short term goal is frustrating. Similar to a few things mentioned on Friday's sessions, like if someone skimps on spending money on developer hardware for the sake of profitability, they'll just lose out on the productivity that could have been gained by buying a better machine. A lot of this is down to siloed thinking and project-protectionism driven by [fundamentally flawed](http://www.amazon.co.uk/dp/184767769X) per-project-profitability incentive schemes for management which narrow the vision, but that's definitely a topic for another day...

____

###Yanking Business Into Testing
*by Gojko Adzic and Lukas Oberhuber*

I was quite eager to see this talk, which combined Lukas' experience of a project that needed help with Gojko's advice on agile testing/impact mapping, as it seemed like a good combination of speakers for one session. (Not entirely unrelated: have a read of Gojko's book on [Specification by Example](http://www.amazon.co.uk/dp/1617290084), it's very good.)

Lukasz and Gojko made observations about the difficulties in the team structure and organisation. One of the biggest problems was that separating development from testing leads to much longer delivery cycles. This happens even when you pretend that you're agile "because we're doing sprints" and you do all your development in one sprint and throw it over the wall to be tested in the next. The grief you're causing yourself here is that it's at least one sprint before you can tell that your work isn't actually done and needs fixing. Seems obvious to some but some organisations have a real problem in bringing testing within the development process and leave it after the fact.

Testing is not done to prevent business risk, because this at best just creates inertia. Testing is done to enable change - it should provide a safety net and feedback. Tests should be isolated from unnecessarily testing implementation when they should be testing outcome. Sure, unit tests are going to be testing implementation details but higher level tests shouldn't be relying on really low level stuff. If your test steps describe just how to test something and not what it is you're actually testing then you're doing it wrong. The test should be for the action and should not in most cases describe a long workflow.

Instability in automated testing is like kryptonite for applications. "Just run it again, that one always fails" means you've got a test that is worth less than no test, because it's giving false negatives. Ensure that your integration tests are testing how components interact with each other, not the business logic. This should be done at a higher semantic level of acceptance testing. This part reminded me of the agile testing pyramid [as described by Mike Cohn](http://www.amazon.co.uk/dp/0321579364) and also mentioned in [a good article by Martin Fowler](http://martinfowler.com/bliki/TestPyramid.html).

Gojko and Lukas also described how the role of the tester had to change in order to be more beneficial than that of a keyboard & mouse operator. The tester should assume a more QA & BA role than previously and should be well integrated into the team - and the team should integrate testing into their work, ensuring that the devs aren't done until something has been tested and accepted.

Gojko also mentioned that most tests are optimised for writing, particularly the very heavyweight front-end step recorder type tools that produce huge scripts and end up being very fragile, hard to debug and hard to change. Tests instead should not be optimised for writing but for reading and running, the two most common uses of tests. All tests that are kept in the system long-term should be able to re-justify their existence.


