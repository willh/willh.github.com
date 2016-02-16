---
layout: post
title: "Fear of Commitment? You Need Options"
description: "A book review of Commitment by Olav Maassen, Chris Matts and Chris Geary, a business novel about managing project risk"
category: 
tags: ["lean", "real options", "feature injection", "deferred decisions", "project management"]
---
{% include JB/setup %}

### A Business Novel in Graphic Form

<a href="../../../../assets/images/20130612_commitment_real_options.jpg"><img src="../../../../assets/images/20130612_commitment_real_options.jpg" alt="A sample of the art and content in Commitment" title="A sample of the art and content in Commitment" height="600" width="600" style="margin-bottom: 20px;" /></a>  
  

Last week I picked up a new book about managing project risk called [Commitment](http://commitment-thebook.com) by [Olav Maassen](http://twitter.com/OlavMaassen), [Chris Matts](http://twitter.com/PapaChrisMatts) and [Chris Geary](http://twitter.com/ChrisAGeary). Commitment is quite unlike most books I've read recently in that it's a graphic novel (and isn't about [Batman](http://en.wikipedia.org/wiki/The_Dark_Knight_Returns) or [Spider Jerusalem](http://en.wikipedia.org/wiki/Transmetropolitan)). [Dan North](http://www.twitter.com/tastapod) kindly pointed me in the direction of this new book after I mentioned that I had enjoyed the novel style of [The Goal](http://en.wikipedia.org/wiki/The_Goal). I thought the novel style of [The Goal](http://www.amazon.co.uk/Goal-Process-Ongoing-Improvement-ebook/dp/B002LHRM2O) was a really engaging and interesting way of describing the lessons by building up a realistic scenario to which the reader can relate and I find it a better way to consume a lot of content than a more academic document.

The book centres around a project manager called Rose who is drafted in at short notice to turn around a failing project. Like in The Goal, the main character discovers new ways of approaching her work and applies them to discover new ways to apply the principles across her environment - demonstrating that the principles are fundamental rather than context-specific. The 'sequential art', as the inside of the dust cover calls it, is drawn to a high standard by Chris Geary and I think the visuals add more than text alone simply would (such as facial expressions and the high level view of the [Kanban][1] board).

### Real Options

The book describes how Rose can manage risk to her project by exploring the concept of [Real Options](http://www.infoq.com/articles/real-options-enhance-agility). Real Options are a concept created by the application of the notion of a [financial option][2] (the *right*, but not *obligation* to perform a certain act, e.g. buying shares) with a little bit of understanding of human psychology, to real life situations. This results in the ability to defer certain decisions to the last responsible moment. Real Options intentionally inject controlled uncertainty in order to avoid the typical human response to just make a decision - any decision at all, even if wrong - instead of deferring it until later.

Real Options are underpinned by three principles:
1. Options have value
2. Options expire
3. Never commit early unless you know why

In the book Rose deals with choices to be made during managing her project by understanding which things are inevitable or immutable - commitments - (e.g. delivering the project) and which things are mutable choices - options - (e.g. adding another tester to the team). By deferring decisions to the last responsible moment (subtly different from the last *possible* moment) we keep options open and can eventually make decisions with more knowledge.

Often in projects we assume that many things are commitments when in fact they are options. Say we're building an online bookstore, for example. Storing customer data is a commitment, which should be obvious. Using an Oracle relational database isn't necessarily a commitment; it's an option. Being able to identify which of our assumed commitments are options lets you decide if you want to act upon these options. Not every option is something in which you want to invest the time and effort ensuring it is kept open and exploited.

It's also interesting to see how Rose moves from an overly complex WBS gantt chart pinned inside her office to a team-visible Kanban system illustrating to the team the current process and helping identify bottlenecks. In the process of identifying the current bottlenecks, options for altering the constraints or alleviating the problem are exposed (e.g. backlog in testing -> add another tester? Reduce number of devs? Deliver smaller releases more frequently?).

Maassen and Matts, in Commitment, also discuss [Feature Injection](http://www.infoq.com/articles/feature-injection-success) - how a focus on the goal for the solution helps identify options that would be obscured simply by focusing on the current feature list: *"The great thing about starting at the end is that you cannot miss something that is needed to produce the outcome. Not only that, but you do not include things that are unnecessary"*

### Applying Real Options

I found the well-explained description of these concepts very valuable as recently I've tried to describe to others the benefits of responsibly deferred decisions compared to making decisions at the moment of greatest ignorance - the very outset. I am also reminded of the talk [Uncle Bob](http://cleancoders.com) gave at NDC Oslo in 2012 [in which he talked about deferring technology decisions](http://vimeo.com/43612849) so that they could be made with more knowledge of the actual requirements. 

In a purely technical example consider envisioning an architecture and providing technology options for a project: starting out with a vision of the solution and suggested frameworks or technologies is all well and good but based on the potential risk in these known unknowns (e.g. does the database technology handle [network partitions](http://aphyr.com/posts/284-call-me-maybe-mongodb)?) we should make a [spike](http://www.extremeprogramming.org/rules/spike.html) to test these theories. Perhaps we create some scenario to test this need and test our preferred technology and find that it might not be as suitable as another not previously considered given the current knowledge. 

Eventually we identify something suitable for the scenario but in our plan we specifically decide to make time for this spike rather than just go ahead and suggest a technology [up front without the hands-on experimentation](http://www.igloocoder.com/2271/ivory-tower-architect). Instead of prescribing this detail, by leaving time for this experiment and making the effort to isolate the rest of the solution from this dependency we have created the *option* to choose a database technology at a later stage once we have greater knowldege.

Coming back to our three principles:

1. this option has a value because we gain more knowledge about the problem the longer we defer this decision; 
2. this option will expire because sooner or later we'll have to make a commitment to some decision;
3. if we commit early we must be aware that we're doing so and what our reasons for this were (e.g. decided we could save money by using existing Oracle license from another project in the business, or whatever).

So applying the principles of Real Options we can track and exploit the decisions we make and ensure that we are consciously making them at the right times. I'd highly recommend [Commitment](http://commitment-thebook.com/products/commitment-the-book) to anyone involved in any kind of product development or decision making - check it out!


[1]: http://en.wikipedia.org/wiki/Kanban_(development)
[2]: http://en.wikipedia.org/wiki/Option_(finance)
