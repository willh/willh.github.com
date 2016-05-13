---
layout: post
title: "CAP Theorem for the Business"
description: "Treating an organisation as a distributed system, apply CAP theorem to identify a choice between autonomy of decision making and uniformity of results."
category: 
tags: ["business", "distributed systems", "cap theorem"]
---
{% include JB/setup %}

### CAP Theorem

In 2000, [Eric Brewer](https://twitter.com/eric_brewer) proposed [CAP Theorem](https://en.wikipedia.org/wiki/CAP_theorem) to describe how a distributed system can only meet two of the three conditions at any one time:

Consistency (C) - every node sees the same data at the same time  
Availability (A) - every request gets a response  
Partition tolerance (P) - the system continues to operate whenever some nodes are unreachable  

Most commonly seen applied in databases, designing a system to handle this is commonly then framed as a choice between the properties: ‘pick two’.

In distributed systems people often favour AP when getting things done is more important than being consistent (e.g. returning stale data or accepting writes and dealing with later conflict resolution), and CP when consistency is most important at the expense of some components not working (e.g. refusing to accept writes unless all nodes reachable). P is most often included as a given because we want the system to stay up when some components are unreachable - this leads to a criticism of ‘pick two’ where people assume you can trivially not choose partition tolerance: [you can’t](http://codahale.com/you-cant-sacrifice-partition-tolerance/).

### CAP in the human system

Businesses become distributed systems when they delegate responsibility to individuals and groups instead of running everything from the CEO’s office in a command and control fashion.

In a distributed business, we can think of people doing their work as the components of the system. I suggest that we can model how people make decisions in a similar way.

Consistency (C) - everyone makes the same decisions and are informed about the outcome  
Availability (A) - everyone can make decisions  
Partition tolerance (P) - decisions can be made without involving everyone  

Where ‘everyone’ is the subset of people in the organisation who care about how decisions are made and have to deal with the impacts.

### How CAP applies

If not everyone can be reached, then we can’t have everyone informed about the decision and involved in making it. Network partitions in the distributed computer system are equivalent to lack of communication in the human system. Be that mechanical in nature (couldn’t reach someone via email), lack of connection (communication doesn’t happen well with another part or parts of the business) or due to lack of awareness (didn’t realise another part of the business was interested in this particular decision), partitions form when people who would or should care aren’t reached during the decision making. I’d argue that this is very common in organisations, especially with increasing size and divisional autonomy.

If we have to ‘pick two’, then like in the computer system context we rarely want to sacrifice partition tolerance as we don’t want to make decisions only by synchronising on a total membership consensus.

### Balancing consistency against availability

#### Availability-Partition tolerance

People can always make decisions, though they may sometimes be different. Deal with lack of consistency.

Decision making is faster as people have autonomy at the risk of ending up with different results of their decision making. Sometimes two decisions will be made in different places at the same time and communication issues have prevented this from being realised.

> Example: two different managers need to decide how to store and report on tasks being completed by their teams, but don’t consult each other on the choice. One picks Trello and another JIRA. The reality is that both can get their work done but that reporting upwards may require some additional effort to consolidate results from both teams, or even that one team has to then move to the other tool after some time. In the meantime, though, a decision can be quickly made and the team can progress without waiting.

#### Consistency-Partition tolerance

A person who can’t reach others can't make decisions in case their decision is different.

Fear of making an inconsistent decision means the decision isn’t made until such a time as everyone is available again. This choice is less useful for most everyday decisions unless there’s a specific need to have additional input into the decision making like mandatory central approval for certain decisions.

> Example: two different managers need to purchase a tool for task tracking, and all decisions on tool purchase need to be approved by a central PMO team. One manager can’t contact the PMO team for some reason (team members engaged on other call, etc) and has to wait until the team is reachable again. Making a purchase for that manager is not possible until that time.

#### Consistency-Availability

No decision can be made without everyone.

> Example: as CP example but neither of the two managers can make a purchase if one of them is unreachable. Probably the least desirable situation unless you operate a Soviet committee.

_The choice here is better framed as one of autonomy over central control, and leading to a choice between faster decision making and identical results._

A bias towards availability (autonomous decision-making) in an organisation with a culture of trust will be a bias towards faster successful decisions. Command-and-control style of organisation enforces consistency at the expense of speed, but the motivational effect of distributing decision making and creating autonomy should not be underestimated [as outlined by Dan Pink's talk](https://www.youtube.com/watch?v=u6XAPnuFjJc).

How to deal with inconsistency in the organisation? Surely inconsistency is bad? What if it leads towards increased cost due to duplication of effort and rework when integrating different tools and processes? While in my opinion consistency should more often play second fiddle to autonomy for the sake of Getting Shit Done, these are valid concerns and consistency can be buoyed by ensuring that individuals are more likely to make similar decisions by themselves.

### Inconsistency isn’t all bad

When organisations get big it becomes increasingly costly and ineffective to insist on consistency for all but the most important of issues. If two teams use different task tracking tools, it’s better to let this happen than to ensure no new team makes a decision without contacting the Central Bureaucracy for direction. Pick up the slack by pushing the hassle up to the person who pulls the aggregated reports together. If two teams want to store their project wiki documents in different locations (Confluence vs GitHub wiki), it’s better to get out of their way and let them create the content - take advantage of people wanting to do the right thing.

Duplication is a wasteful form of inconsistency. Different groups or individuals doing things separately may work for them at the expense and overhead of duplicated effort. You need patterns of dealing with inconsistency - aggregated search for different content, task tracking tool data export APIs, federated authentication, etc. Having sensible defaults will reduce the overhead for people who want to make decisions and don’t have specific different needs without requiring a quorum from the rest of the organisation - but accept the fact that people will inevitably diverge from that for various practical reasons.

[Mission Command](https://en.wikipedia.org/wiki/Mission_Command) and other forms of modern leadership focus on alignment on higher goals as the basis of enabling an AP approach to individual decision making. Consistency is trusted to be a by-product of decisions made by an individual with an understanding of the intent of the leader. Creating a [culture focusing on a common purpose and a shared understanding of the principles](http://www.slideshare.net/reed2001/culture-1798664) by which decisions should be made will improve the consistency without requiring costly and ineffective synchronisation between individuals.

### You don’t choose for the whole system at once

Back with distributed computer systems, in reality while CAP theorem holds true between components tasked with caring about the data it’s an oversimplification to consider an entire software system as choosing two. Different subsystems can pick different approaches: a highly available AP system for recording requests and responding with stale data but another subsystem can fail to respond when consistency is paramount, and a system can change its mode depending on the type of request it receives. Eric Brewer has published an article on his view of [CAP twelve years later](http://www.infoq.com/articles/cap-twelve-years-later-how-the-rules-have-changed) covering this nuance and more.

With a distributed business, in the same way I think it’d be an oversimplification to say you need to choose entirely between consistency and autonomy for getting stuff done in the workplace. For example, setting common guiding principles across the organisation can influence how people make decisions without having to get input and approval for everything.

Consider how communicating shared goals and principles, then demonstrating trust can enable parts of the organisation can be granted more autonomy to work on an ‘ask for forgiveness, not permission’ basis and critically assess which other parts (e.g. contract approvals, major purchases) truly need to have consistency enforced.

Clearly delineate areas that people are expected to adhere to consistency so that they can use their judgement when choosing whether to wait on consensus or Get Shit Done. It’s easy to put up your hands and repeat empty truisms like “I’m a right tool for the right job kind of person” while dodging the difficult work of illustrating where consistency is a nice-to-have and at which point the benefit of fast decision making and autonomy is overtaken by the cost of the potential inconsistency.

Have sensible defaults that you trust people will only step outside for good reasons (e.g team members are allocated Mac machines unless project need dictates other hardware), and hard lines where we can’t (e.g everyone has to have full disk encryption without exception) and make the few cases where consistency is needed known. Being conservative with the consistency edicts and limiting them to where it is truly necessary and doesn't just make things easier for the people doing reports will help everyone take them seriously and engage with the important parts.

<br />
Thanks to [Rory Hanratty](https://twitter.com/Rory80hz), [Kyle Thompson](https://twitter.com/kylethompson86), [Alan Jennings](https://twitter.com/GinjaNinja2004) and [Rob Lazzurs](https://twitter.com/lazzurs) for feedback and proofreading.

_Addendum: after sketching out this blog post I found that [Jessica Kerr](https://twitter.com/jessitron) has recently written a great post on how this applies in terms of [co-ordinating development teams on technical decisions](http://blog.jessitron.com/2016/05/tradeoffs-in-coordination-among-teams.html) and coupling software components. This is a great read, and an interesting perspective into applying the autonomy vs consistency struggle when it comes to dividing work in a system across contributing groups._