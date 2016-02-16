---
layout: post
title: "QCon London 2013 - Day Three"
description: "The third day of QCon London 2013 featuring opening keynote from Ward Cunningham, talks from David Dawson &amp; Justin Holmes, Matt Asay, Mat Wall, Martijn Verburg &amp; Kim Ross, and Douwe Osinga &amp; Jon Tirsen"
category: 
tags: ["qcon", "conference", "wiki", "play", "grails", "nosql", "mongodb", "gds", "architecture", "agile", "recruitment", "culture"]
---
{% include JB/setup %}

### Keynote - A Forward Look at Federated Wiki
*by Ward Cunningham*

The final day of the conference began with a keynote from Ward Cunningham, inventor of the wiki, [Extreme Programming Applied](http://www.amazon.co.uk/dp/0201616408) author and original signatory of the [agile manfiesto](http://agilemanifesto.org).

Like Wednesday's opening keynote I didn't take many notes here because the talk was being illustrated by Heather Willems, so instead I've attached a photo of her visualisation. (click for huge) The power of the federated wiki appears to be in its ability to be forked and refactored and is much more of a dynamic data source than a static wiki. Ward demonstrated using it to create pages with graphs directly reading from an external, live temperature sensor, and also using the page data as input to an LED & speaker. Live refactoring and recalculating of equations was also cool. I'm interested in seeing where this goes.

<a href="../../../../assets/images/20130308_ward_cunningham.jpg"><img src="../../../../assets/images/20130308_ward_cunningham.jpg" alt="A visualisation drawn by Heather Willems of Ward Cunningham's talk on Federated Wiki at QCon London 2013" title="Illustration by Heather Willems" height="600" width="600" /></a>

____

### Play! Vs Grails - A Fireside Chat
*by David Dawson and Justin Holmes*

To be honest this first morning session was a little disappointing. Being described as a fireside chat I expected two chairs, a table with some drinks on it, and a casual but candid discussion of the differences, strengths and weaknesses of the two frameworks in question here. Unfortunately it seemed to more have been orchestrated as a humourous tongue-in-cheek head-to-head fight, which was a bit awkward and unexciting.

Under discussion were the main differences between Play! and Grails, which include statelessness, containerlessness (is that a word?) and first-class Scala & actor support on the Play! side, and Spring familiarity and expanse of plugins on the Grails side. I expect that spending half an hour on the two sites reading the documentation will tell you the major differences well enough; I don't have much in the way of notes for this session that can't be bettered with some quick Googling.

It's important to understand that in different scenarios there is often a better tool for the job but I was expecting more of a focus on advice like when Play! doesn't fit, when Grails doesn't fit, and when they've got similar utility but the implementation style and opinions baked into each framework may determine your choices. Some discussion was started when the two speakers had different viewpoints on how particular things should be implemented but there wasn't much in the way of real life examples or anecdotes to back up the use cases described and I think that more practice and preparation would be needed to make this format more valuable to the attendees.

____

### The Past, Present and Future of NoSQL
*by Matt Asay*

Matt is employed by 10gen, the makers of MongoDB and gave a talk on the emergence of NoSQL, the state of the union and briefly commented on where he thinks the future for these technologies lie. Matt described the history of data storage without SQL (which is not new!) and how the introduction of SQL in the 1970s was a great leap forward in decoupling the data storage schema design from the query design.

However more and more companies are discovering the lessons learned by web-scale systems like Facebook, Google and Craigslist: that traditional SQL based relational data stores can't scale to cope with today's huge data sets. The NoSQL paradigm emerged from a resistance to hammer the square peg of RDBMS into the round hole of loosely structured, sometimes complexly linked, sometimes unlinked, huge scale data. I would recommend some reading around [CAP Theorem](http://en.wikipedia.org/wiki/CAP_Theorem) to go alongside this. 

More and more of today's systems rely on storing differently structured patterns of engagement (e.g social interactions, knowlege based info like Netflix's movie recommendations) instead of simpler structured data (e.g CRM, ERP systems). NoSQL can in these cases be the tool that aligns more closely with these problems, and most NoSQL technologies also have made great efforts at improving developer productivity to allow for the rapid iteration of modern agile development practices.

With NoSQL persistence the benefits also include a more scalable data store though this requires awareness of the trade-offs, but being able to make these choices rather than having to misuse RDBMS is where the utility lies. NoSQL data stores, according to Matt, also result in a lower total cost of ownership over time (citation needed?).

Matt described how for many modern organisations, NoSQL is the new normal. For example at The Guardian their data persistence technology of choice is now MongoDB for ease of use and scalability, and to choose something different on a new tech project requires justifying why not to use it (which I'm sure is quite different to many organisations' approach in this area).

Matt suggested that the future of data storage lies in the 'polyglot persistence' paradigm; to have simultaneously multiple data storage styles in use for different parts of the business' data as per what best fits that data and the way it is used. For example, storing highly related data like recommendations or travel itineraries in a graph database, website user comments in a document store and HR records in the RDBMS. Horses for courses - not just the current flavour of the month for every problem!

____

### Green Shoots in the Brownest Field: Startup in Government
*by Mat Wall*

Mat Wall is a Technical Architect with Government Digital Service (GDS) and works with Gareth Rushgrove who gave [a talk I attended on Wednesday](http://willhamill.com/2013/03/06/qcon-london---day-one/#clouds_in_government__perils_of_portability). Mat also covered the details of the history, and how & why GDS operate. Mat described the evolution of the tech stack of the GOV.UK platform, and how it was not necessarily intended from the start to be a platform but rather a solution to a problem. Mat described that letting the developers involved make most of the technical decisions rather than a traditional approach to 'strategic architecture' had enabled them to solve problems faster and with the most suitable tool for each part of the problem rather than being prescriptive and restrictive about implementation details.

Mat illustrated how the architecture had changed most in terms of the interactions between the components within the publishing platform, and how simplicity has been important in solving just the problem at hand. Mat argued that the involvement of the developers as the actual problem solvers and as trained professionals rather than just keyboard bashers was critical to good communication and the kind of working environment that was necessary to keep productive, talented people at work as opposed to the kind of bureaucratic environment that has in the past often driven many people away from the public sector. Having the developers well integrated with the rest of the team (architects, product owners, deliver managers) gave them the context and information needed to make the right decisions, rather than simply isolating the developers from the outside entirely.

Mat also described how making some tradeoffs or using a 'good enough for now' approach was involved in keeping momentum, rather than stopping work and getting mired down in external dependencies and having to work to outside parties' deadlines. Mat's example of this was a project currently in progress to develop a system for individual online electoral registration, which relies on integration with approximately 400 local authority based Electoral Registration Officers (EROs), and also with the Department for Work & Pensions (DWP) in order to provide confirmation of identity data. As an aside, Mat made the point that this kind of integration was happening across many new government transaction projects because contrary to what you may infer from the tabloids - there is in fact no one 'big government database'!

In the above project, integration with EROs and DWP was necessary for the team to progress with integrating and testing their services but the dependency on an actual electrical datalink between these third parties would be a major impediment to the team's momentum and would significantly delay progress. In the interim, instead, the arrows on the diagram (as it were) were in fact connected not yet with a secure connection but with "high bandwidth, long-latency" transport: a secure motorcycle courier. Data was delivered encrypted via a vehicle in order for progress to be made. The motorbike diagram got a laugh from the audience but the real importance is in making the trade-off allowed the team to maintain momentum. This example was particularly poignant for me as the team that I've had the privilege to be working with for the last 9 months has been this project and the effect on us was that we that at the time we could make significant progress without having to seriously delay the integration phase of the project.

This is quite a bit farther than most teams developing components can take the approach of stubbing out external services to represent outside dependencies but the lesson is in dealing with a less than perfect architecture for the purpose of decoupling the team and making real progress.

____

### NoHR Hiring
*by Martijn Verburg & Kim Ross*

This session on 'NoHR hiring' was titled as a pun on NoSQL. A lot of the material covered was the kind of stuff that makes sense but often falls out of the process when formalised, homogenised and passed through various compliance and legal filters. In this discussion Kim and Martijn described important ways to focus on seeking out getting the right people.

When assessing a CV, often given the template nature and the somewhat boring list of technology acronyms it can be easier to tell whether the person fits and actually cares about applying for the job from their cover letter. Unfortunately when using external recruiters this won't be included and the CV may be reformatted (or worse) to fit their template. However a good cover letter can tell the business that a candidate has actually investigated what it is that the business does, what they expect from the job and in plain English tells a little more than the '10 years Java, 5 years .Net' does.

Analysing a candidate's CV is a great way to derive questions for an interview. Use the technologies they've listed or the projects they've worked on to ask open ended and relevant questions. By relevant, Kim and Martijn mean to avoid the kind of gimmicky "how would you implement a merge sort" basic algorithmic questions (unless the job in question actually relies upon this kind of very low level algorithmic knowledge), or something that any real developer will likely just turn to Google to answer when doing their day job.

In a telephone interview Kim warned not to answer closed questions that could be quickly Googled while the candidate stalls, which is a good suggestion. I'm personally not a fan of phone interviews after having had one before and being unable to gauge impressions from the body language and explain myself better, as the phone is quite awkward compared to a face to face interview in my opinion.

When assessing candidates, logical questions and process-flow style challenges can be more useful than coding assessments as they test the problem solving thought process rather than syntax and language semantics which change from language to language and are easy to get wrong on a whiteboard (especially without your IDE/compiler). I'm of the opinion that any kind of coding question should be something very easily displayed in pseudocode but that the process by which the candidate asks clarification questions and goes about solving the problem is more interesting than the solution.

Martijn mentioned the utility of checking up public profiles on Github and Stack Overflow to check out candidates' contributions, though not holding it against the candidate if they didn't get involved in such public-facing activities. Martijn also implored the audience not to use anything they read on the candidate's Facebook page to influence their impressions (unless they're clearly doing something awful like kicking a load of babies) because both of the inappropriate sway an opposing opinion may have on you and also out of sheer respect for privacy.

In terms of judging the candidate at interview it's very important to have a technical person in the interview (most tech companies do this already) and if possible, someone on the team for which the opening is being advertised. Fundamentally after all the logic tests, CV questions, "tell us a time you had to deal with problems on a project" style stuff you should be asking yourself the most important question: "would I want to work with this person?" I think this is sterling advice and especially in the area of software development when people mistakenly think that technical savvy is the be-all and end-all, it's really the team dynamic and the communication and interactions that make a great co-worker. I'd rather hire someone personable, enthusiastic and thirsty for knowledge who needs trained up in the technology than That Guy who is an absolute guru and can't stand people.

Kim and Martijn also argued that many businesses don't make it easy on themselves by way of creating uselessly vague or acronym-drenched job specs, without going into much effort to actually attract, inform and convince candidates why they should work there. I think this is certainly an interesting point given that the current job market makes it easy for someone in development to find employment and for someone aware of their worth to turn down a business that isn't selling itself as a place that talent should converge and flourish.

When hiring, it's important to do your best to make the job spec descriptive of what the *actual day job* entails. It's likely that both the HR and Legal departments are going to filter anything that is produced so trying to make it representative of what's actually involved will allow candidates to make better educated decisions. Describe what a developer on your team actually does day to day, who the interact with and what kind of problems they solve without just jumping into the "HTML/CSS/JS/ASP MVC" response. How do your teams actually work? Do they do agile? Are they distributed? Do they interact with business/customers? What are the salary and benefits like? What's the working environment like - cubicles and silence or team rooms and interaction?

Kim and Martijn also described how as a business getting involved in the developer community has no drawbacks but great advantages in terms of getting your brand and your work out in front of exactly the kind of people you want to hire. Attending or sponsoring user groups and conferences is especially a good way to get exposure from the most talented and engaged people - who are inevitably already employed!

**Correction:** This post originally stated the talk was by Martijn Verburg & Zoe Slattery, but Zoe was substituted with Kim Ross. Kim is not from HR as mentioned and is in fact a developer. Apologies for any confusion!

____

### Architecture of the Triposo Travel Guide
*by Douwe Osinga & Jon Tirsen*

This final session was very interesting to me - I've never heard of Triposo before and I'm also in the process of planning out a holiday to the USA for later this year so it was quite useful to see what makes this company tick and how they differentiate from the competition. Triposo's main difference is that their travel guides are algorithmically generated rather than by hand, which means that they can collate and aggregate incredible amounts of data, gaining insights into sights, restaurants, events etc from a larger scale view.

Triposo was founded by two ex-Googlers and gave a good laugh with the line from their back story of "we met while working on Google Wave, and once we'd finished making that a huge success we needed something to challenge us". The details of Triposo's application development and deployment process was an interesting insight into how a company of their small size can regularly push updates for 80~ apps to the iTunes App Store.

The team is distributed and communicates mostly via Google Hangouts or similar, but it was very important to have the team come together often in order to build social connections and camaraderie. Douwe showed photos from a project kick-off meetup when the development team had all gotten together in Gran Canaria. I've read a few other articles about distributed teams and it seems that having the ability to get everyone in the one place for dinner, drinks and a bit of fun does have a positive impact on communication and relationships in the team (where often the distance and separation can be detrimental). Triposo have a focus on expanding their product through experimentation which is done at company hackathons and the results are either built into the product or given away to the community via the [Triposo Labs site](http://www.triposo.com/labs).

Triposo's data aggregation and build process (for they are one; each app must work offline) is based largely upon crawling open data such as Open StreetMap, Wikitravel and Wikipedia for places and other sources for inclusion in the app, but also makes use of knowledge gained from crawling across closed data that can't be used directly within the app. For a simple example, the more photos found on Flickr of a given place can be used to determine how popular a site is with tourists. Much more detailed analysis and other inferences are made with these kinds of data sets and while my notes here are unfortunately sparse it was very interesting.

The data, once aggregated, is sync'd with Dropbox and accessed by the build server. Build, signing, testing and app store submission of the 80~ apps are orchestrated by a set of VMs as the process for each app takes over an hour and would be infeasible to do singly. This enables Triposo to send an app to the app store for each major city/region which is necessary for SEO reasons because their competitors all sell single region apps and otherwise a global Triposo app won't end up the search results.

____
