---
layout: post
title: "QCon London 2013 - Day Three"
description: "The third day of QCon London 2013 featuring opening keynote from Ward Cunningham, talks from David Dawson &amp; Justin Holmes, Matt Asay, Mat Wall, Martijn Verburg &amp; Zoe Slattery, and Douwe Osinga &amp; Jon Tirsen"
category: 
tags: ["qcon", "conference", "wiki", "play", "grails", "nosql", "mongodb", "gds", "architecture", "agile", "recruitment", "culture"]
---
{% include JB/setup %}

###Keynote - A Forward Look at Federated Wiki
*by Ward Cunningham*

The final day of the conference began with a keynote from Ward Cunningham, inventor of the wiki, [Extreme Programming Applied](http://www.amazon.co.uk/dp/0201616408) author and original signatory of the [agile manfiesto](http://agilemanifesto.org).

Like Wednesday's opening keynote I didn't take many notes here because the talk was being illustrated by Heather Willems, so instead I've attached a photo of her visualisation. (click for huge) The power of the federated wiki appears to be in its ability to be forked and refactored and is much more of a dynamic data source than a static wiki. Ward demonstrated using it to create pages with graphs directly reading from an external, live temperature sensor, and also using the page data as input to an LED & speaker. Live refactoring and recalculating of equations was also cool. I'm interested in seeing where this goes.

<a href="../../../../assets/images/20130308_ward_cunningham.jpg"><img src="../../../../assets/images/20130308_ward_cunningham.jpg" alt="A visualisation drawn by Heather Willems of Ward Cunningham's talk on Federated Wiki at QCon London 2013" title="Illustration by Heather Willems" height="600" width="600" /></a>

____

###Play! Vs Grails - A Fireside Chat
*by David Dawson and Justin Holmes*

To be honest this first morning session was a little disappointing. Being described as a fireside chat I expected two chairs, a table with some drinks on it, and a casual but candid discussion of the differences, strengths and weaknesses of the two frameworks in question here. Unfortunately it seemed to more have been orchestrated as a humourous tongue-in-cheek head-to-head fight, which was a bit awkward and unexciting.

Under discussion were the main differences between Play! and Grails, which include statelessness, containerlessness (is that a word?) and first-class Scala & actor support on the Play! side, and Spring familiarity and expanse of plugins on the Grails side. I expect that spending half an hour on the two sites reading the documentation will tell you the major differences well enough; I don't have much in the way of notes for this session that can't be bettered with some quick Googling.

It's important to understand that in different scenarios there is often a better tool for the job but I was expecting more of a focus on advice like when Play! doesn't fit, when Grails doesn't fit, and when they've got similar utility but the implementation style and opinions baked into each framework may determine your choices. Some discussion was started when the two speakers had different viewpoints on how particular things should be implemented but there wasn't much in the way of real life examples or anecdotes to back up the use cases described and I think that more practice and preparation would be needed to make this format more valuable to the attendees.

____

###The Past, Present and Future of NoSQL
*by Matt Asay*

Matt is employed by 10gen, the makers of MongoDB and gave a talk on the emergence of NoSQL, the state of the union and briefly commented on where he thinks the future for these technologies lie. Matt described the history of data storage without SQL (which is not new!) and how the introduction of SQL in the 1970s was a great leap forward in decoupling the data storage schema design from the query design.

However more and more companies are discovering the lessons learned by web-scale systems like Facebook, Google and Craigslist: that traditional SQL based relational data stores can't scale to cope with today's huge data sets. The NoSQL paradigm emerged from a resistance to hammer the square peg of RDBMS into the round hole of loosely structured, sometimes complexly linked, sometimes unlinked, huge scale data. I would recommend some reading around [CAP Theorem](http://en.wikipedia.org/wiki/CAP_Theorem) to go alongside this. 

More and more of today's systems rely on storing differently structured patterns of engagement (e.g social interactions, knowlege based info like Netflix's movie recommendations) instead of simpler structured data (e.g CRM, ERP systems). NoSQL can in these cases be the tool that aligns more closely with these problems, and most NoSQL technologies also have made great efforts at improving developer productivity to allow for the rapid iteration of modern agile development practices.

With NoSQL persistence the benefits also include a more scalable data store though this requires awareness of the trade-offs, but being able to make these choices rather than having to misuse RDBMS is where the utility lies. NoSQL data stores, according to Matt, also result in a lower total cost of ownership over time (citation needed?).

Matt described how for many modern organisations, NoSQL is the new normal. For example at The Guardian their data persistence technology of choice is now MongoDB for ease of use and scalability, and to choose something different on a new tech project requires justifying why not to use it (which I'm sure is quite different to many organisations' approach in this area).

Matt suggested that the future of data storage lies in the 'polyglot persistence' paradigm; to have simultaneously multiple data storage styles in use for different parts of the business' data as per what best fits that data and the way it is used. For example, storing highly related data like recommendations or travel itineraries in a graph database, website user comments in a document store and HR records in the RDBMS. Horses for courses - not just the current flavour of the month for every problem!

____

###Green Shoots in the Brownest Field: Startup in Government
*by Mat Wall*

____

###NoHR Hiring
*by Martijn Verburg & Zoe Slattery*

____

###Architecture of the Triposo Travel Guide
*by Douwe Osinga & Jon Tirsen*

____






