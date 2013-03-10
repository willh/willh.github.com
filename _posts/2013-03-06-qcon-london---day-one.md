---
layout: post
title: "QCon London 2013 - Day One"
description: "The first day of QCon London 2013 featuring opening keynote by Barbara Liskov, closing keynote by Damian Conway, talks by Stefan Tilkov, Gareth Rushgrove, Rickard Oberg, Russel Miles, and Alex Papadimoulis"
category: 
tags: ["abstraction", "http", "web", "cloud", "architecture", "rest", "api", "cloud", "deployment"]
---
{% include JB/setup %}

####Opening Keynote - The Power of Abstraction
*by Barbara Liskov*

The keynote was given by Barbara Liskov (of the [Liskov Substitution Principle](http://en.wikipedia.org/wiki/Liskov_substitution_principle)) on The Power of Abstraction.

Rather than transcribe notes for the keynote, I thought instead I would include a visualisation of the keynote drawn in real time by Heather Willems. It was really interesting to see this drawing evolve as she took in content of the keynote speech. (click for huge)

<a href="../../../../assets/images/20130306_barbara_liskov.jpg"><img src="../../../../assets/images/20130306_barbara_liskov.jpg" alt="A visualisation drawn by Heather Willems of Barbara Liskov's talk on The Power of Abstraction at QCon London 2013" title="Illustration by Heather Willems" height="600" width="600" /></a>

____

####Web Development - You're Doing It Wrong 
*by Stefan Tilkov*

At the start of the talk, Stefan listed common antipatterns and what he saw as irrational complaints about HTTP and the Web. This included working around its statelessness, preventing browser functionality (e.g. opening multiple windows of the same site, breaking back button use, reventing refresh of the page, etc), making ads and images load before article content, and so on. At this point in the talk a guy came in and sat down next to me and having not seen the context of the opening began to write down the antipatterns as advice on his page of notes...

Stefan argued that we need to focus on the power and capabilities of the Web, as though it is not perfect, no other system comes close - imagine trying to spec out and create a system so pervasive and flexible from scratch! Stefan also argued that pushing all session-state and logic down into a heavy client-side JavaScript page was not the ideal solution, even though it seems the logical opposite of server-side frameworks and things like applets that give the illusion of statefulness.

Stefan briefly mentioned ROCA ([Resource-oriented Client Architecture](http://roca-style.org)) as a series of recommendations for more rational use of the web's intended functionality. Check out that link for some (controversial?) interesting and sensible tips on how to design your RESTful web application to treat accessing data through your web app as HTTP resources and avoid layering on too much client side logic.

We should let people use their browser features! Don't prevent them from bookmarking pages in your system, for example by using properly constructed and meaningful URLs for resources. When everything in the site is created dynamically and the URL doesn't change, we're violating users' expectations that their browser will behave the same across the web. Browser behaviour shouldn't be broken by the implementation of one particular web app.

HTTP is stateless; embrace it! Not dealing with server-side session stickiness and its associated nightmares frees you up greatly when it comes to horizontal scalability. Stefan described a few approaches for splitting large seemingly-stateful interactions into single interactions and thus maintaining statelessness. This was quite interesting, and I thought of the myriad of briefly-stateful interactions we make with many systems that could be changed in this way (most recently when booking my car's MOT online, it is an 8-step process, but that need not be necessarily stateful in server session terms).

The use of unobtrusive JavaScript enables progressive enhancement, separation of concerns and a baseline good experience for the lowest common denominator. Leaving business logic on the server, to the most reasonable extent, avoids duplication of logic in JS-heavy clients and results in low cohesion. Since working on a very JS-heavy front end application designed in Ext-JS I've been concerned with having too much logic and code in the most fragile (and often hardest to test) part of the app so this makes a lot of sense to me. Heavy JS client side action often means people forget not to trust the client, too! Have a little read [here](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript) for starters if you've never heard this term before.

____

####Clouds in Government - Perils of Portability
*by Gareth Rushgrove*

In the first half of this session, Gareth described the origin and purpose of Government Digital Services (GDS) and how they have been changing the way the UK government creates and procures digital services. Whilst this is an utter breath of fresh air compared to most people's mental picture created by any terms like "online government system", I didn't actually take a great deal of notes here because I've had the great pleasure and opportunity to work with GDS during my work with Kainos.

Gareth described the deployment process for GOV.UK, the new front page for the UK government designed to replace and improve upon DirectGov and BusinessLink. The deployment pipeline treats configuration and networking as code, including configuration management and automation using Puppet. It's clear that automation has resulted in a very safe and low-friction deployment process as evidenced by the frequency and stability of GOV.UK releases. Check out the [GDS Badger of Deploy](https://twitter.com/GDS_Badger) on Twitter to see that they've made 848 production releases since launch in the 17th of October. Impressive!

Avoiding platform lock-in is a major concern for GDS, as they're tasked with spending taxpayer money in order to get the best deal for the requirement to host various sites, transactions and platforms and they do take it seriously. Lock-in imposes risks due to the reliance on a single vendor and gives the vendor power in the supplier-consumer relationship. Having learned lessons from government being treated as a feeding trough by the likes of £Billion contracts with Big Named vendors (my words here, not his ;) ), portability in the software solution is very important.

Gareth compared the various capabilities of cloud service providers such as Amazon and Rackspace, and how there is a difficulty in comparison when the various APIs of each provider's services use such different language or in some cases the same langauge to talk about distinct terms. Avoiding platform lock-in is a big thing for GDS and lock-in comes in flavours other than the most obvious technology support ones such as capability lock-in when you rely on services or features that only one vendor provides or (implicit) capacity lock-in when you're so big that there aren't really any other options than the likes of Amazon (e.g. Netflix aren't going to realistically be able to move their systems to another provider).

Gareth also talked about cloud abstraction libraries such as Fog and JClouds which can be used to attempt to provide a uniform semantic layer over the functionality of different cloud vendors. This seems to be an admirable goal but the reality is that the abstraction leaks and vendor-specific language and configuration makes its way into the application again.

____

####Road to REST
*by Rickard Oberg*

Rickard made an impassioned defence of the principles underlying REST and their usefulness, and asked one thing of the attendees: if your application communicates with your API in a way that isn't actually RESTful - please stop calling it rest!

RESTful APIs require resource linking in order to actually meet the requirement for using HTTP as the engine of application state (HATEOAS), but most common implementations don't do this. Rickard demonstrated how most websites are actually better REST API clients of the server resources than hand-rolled REST clients for web applications, as they only interact by following links or submitting forms and do so with properly described resource links and using the HTTP GET/POST verbs as intended with meaningful URLs.

Rickard showed how rather than exposing the domain model via the API, a more semantically meaninful and truly RESTful implementation is reached by exposing use cases; actions within the application described as URLs and acted upon with HTTP verbs. This also simplifies client development and documentation. For example, instead of a URL describing /users/willhamill/changepassword from a use-case perspective this could be /accountmanagement/changepassword/willhamill for changing my own password and /administration/changepassword/username/willhamill to change the password of another user.

In terms of simplifying server side implementation, this means that we can easily determine that actions in account management act upon the authenticated current user, but the actions performed in the administration use cases must require the permission (or role or whatever) to participate in these use cases. It also means that we can have this check a requirement for any resource after /administration but not need to specify it on on each single resource. We could also do something like have /administration paths only available within the internal network.

URLs exposed in the system start with higher level use cases and each / in the path represents a sub-use case, and doing a HTTP GET on / will list the actions available to the current user within that use case. I think this approach of exposing use cases rather than data or domain models makes a lot of sense and can make it easier to arrange the resources and actions in a web application. Rickard tied his example back into the point he made about a website - if we wanted to display a simple resource on a web page in this hierarchy we would likely be constructing a URL of this nature to make a meaningful link to the resource.

Rickard argued that exposing the domain model was undesirable as it exposes implementation details of the service, and means that we can end up with an inefficient architecture. In the example he gave, where a client is building a particularly detailed screen it makes dozens of calls to the service to build parts of the screen, because its actions are oriented around the domain model and getting pieces of its data back (or getting lots of data back across lots of domain models). This is inefficient when compared to exposing the use case and having a single call to the API to which the service responds with a single request containing all the data encapsulated in that use case. This was quite an interesting approach and I think rightfully abstracts the detail of the service's implementations from the client, which needs only to know about the contract for that particular interaction instead.

____

####You Are Not (Only) A Developer! - Simplicity In Practice
*by Russel Miles*

Russel's talk was quite narrative and described common mistakes made when development teams get bogged down in implementation and the drive for productivity. Russel used an [impact mapping](http://www.impactmapping.org) approach throughout the talk to derive the valuable goals for our efforts, and urged that we draw out assumptions between our current state and the desired end goal, so that the can be tested.

Russel made the point that often as developers we question only our implementation options rather than the goal itself. For example, when someone tasks you with writing a mobile app because their goal is "We need an app on the app store" - question that goal rather than getting straight into cracking open your favourite IDE. Why do we need an app? What do they actually mean by that? Will any kind of app do? Seek to understand the business decisions in terms of the value you need to create rather than the productivity you need to have - are we creating an app so that we can increase customer retention? Or are we trying to meet the functionality that a competitor has?

Fundamentally, Russel made the point that we are involved not to produce software but to produce valuable change for the business. This resonated with points made in the pre-conference training session on 'Accelerated Agile' by [Dan North](http://dannorth.net) that I attended, where Dan described how value to the business is what we need to deliver rather than just the output of software.

____

####Racing Through The Last Mile - Cloud Delivery and Web-Scale
*by Alex Papadimoulis*

Alex's talk was an interesting look at the difference between typical, smaller, enterprise deployment and 'web-scale' deployment. Web-scale is the term used to describe the scope and size of the challenges encountered by platforms and products used by and served to vastly more users than typical applications. Think Facebook, Google, Twitter and Netflix - the problems they encounter trying to design and maintain systems for millions or billions of people are quite different to those encountered by an in-house enterprise application developer responsible for deploying their 'customer portal' or the likes to another thousand users.

In all web-scale systems with publicised details, the most obvious difference from other applications is that they are inevitably decomposed into a multitude of services and interacting components. This decomposition reduces dependency and enables parts of the product to be upgraded or deployed separately. When you reach the scale of having hundreds or thousands or hundreds of thousands of servers with deployed components, the probability that a component somewhere has failed asymptotically approaches 1. One of the most interesting things approaches to handling this in a service-oriented architecture that I've read was about is the [Netflix Chaos Monkey](http://techblog.netflix.com/2012/07/chaos-monkey-released-into-wild.html) which Netflix use to test robustness and durability of their systems.

Alex described other problems that web-scale systems have in deployment, including strategies for rollout of upgrades (half and half, random selection of servers, rolling wave) in order to ensure zero downtime. The web-scale systems involved have very different constraints compared to your office's Sharepoint document system when going down for half an hour at 1am on Sunday is going to be noticed by a million users (think any time Twitter is down, for example). Interestingly Alex mentioned how Twitter use a bittorrent-like system to push out updates to their servers in chunks and spread updates throughout their network of machines.

Alex argued that the best way to reduce pain in deployment is to do it often, and the best way to test your failure plans is to actually enact them. You don't want to be one of those nightmare scenarios you've read about where someone has to restore from a backup tape for the first time and then realises that the wrong thing has been being backed up for months. This is similar to the principles proposed in Continuous Delivery - if something is fragile, dangerous and difficult then don't postpone it; do it more often. When you do deployments frequently then you become more proficient, you tend to automate things and you tend to have fewer changes between deployments.

Rollbacks are often a cause of great pain in deployments, but I agree with Alex that the best way to do a rollback is not to create custom rollback scripts and reverse-deltas, but instead to run the deployment process for the previous, working version of the app (and that way you know the process is tested much more often).

____

####Evening Keynote - Fun With Dead Languages
*by Damian Conway*

Damian Conway is a well-known speaker and Perl programmer, and the keynote closing session of the first day of QCon was about the need for diversity of implementation to encourage diversity of thought. Using the example of the death of the Gros Michel banana from Panama Disease due to a lack of diversity (and the resulting reliance on the reportedly less-delicious Cavendish), Damian encouraged use of alternative programming languages and styles to get a different perspective on the methods that we know and use most often.

Damian lamented that modern computing education splits itself into seven or eight major topics and then teaches each one in Java instead of illustrating each area with perhaps something that could broaden perspectives beyond the typical Object-Oriented 101 approach. Damian coined Thor's Law - "Just because you know how to use one great big coding hammer doesn't make you a programming God", evocative of [Maslow's Hammer](http://en.wikipedia.org/wiki/Maslow's_hammer).

Damian demonstrated some diversity in style by using PostScript, a declarative language (old school!), to write a program that determines the value of Pi by declaring functions and using the stack to store function results, as it has no variables or methods (much like how compiled code *actually* works deep down in the plumbing, underneath all the abstraction). As a bonus, because the only common use of PostScript these days is in printers, you can still write this program and send its source file to most office printers and have them actually print out increasingly accurate estimates of Pi.

Damian also illustrated translating a C++ implementation of [Eratosthenes' Sieve](http://en.wikipedia.org/wiki/Sieve_of_Eratosthenes) into Latin (yes, *Latin*) to show how the need for ordering of variables and method operators could be removed through the use of different inflexions on the nouns being used - when you have a suffix at the end of a variable telling you it is being operated on, and a suffix on another telling you that it is operating on something then the ordering doesn't matter any more. This part of the talk was fantastically entertaining and ended with a demonstration of the actual program written in Latin and executing to produce the prime numbers up to CCLV (that's 225 for us non-Latin types).

Further reading: Damian is the author of the [CPAN module](http://search.cpan.org/~dconway/Lingua-Romana-Perligata-0.50/lib/Lingua/Romana/Perligata.pm) [Lingua::Romana::Perligata](http://www.csse.monash.edu.au/~damian/papers/HTML/Perligata.html) which I came across a few years ago which allows Perl users to write their code actually using Latin. When I asked Damian if he'd every deployed any code into production using Latin he said that he hadn't, but that a few Perl devs from Romania had written their website using it!

____
