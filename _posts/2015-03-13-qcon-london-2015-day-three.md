---
layout: post
title: "QCon London 2015 Day Three"
description: "Conference sessions from the third day of QCon in 2015. Talks from Roy Rapoport, Dan North, Phil Wills, Todd L. Montgomery, Phil Calçado, Yoni Goldberg and Michael Brunton-Spall"
category: 
tags: []
---
{% include JB/setup %}

The final day of QCon was back into the world of microservices, hearing from a number of speakers how they'd implemented microservices and what it meant for them. Common themes were dividing services up, monitoring and deployment needs. The keynote from Netflix tied into this very well, as monitoring is super important with a microservices approach. I came back to [my initial thoughts](http://willhamill.com/2015/03/04/qcon-london-2015-day-one/#my_thoughts) about the hype versus the cynicism again today and still think that the bottom line is that if you're thinking critically about your architecture, separating responsibilities and working towards continuous delivery then I don't care what you call it!

- [How Netflix built a monitoring platform and why you probably shouldn't](#netflix_monitoring)
- [Microservices: software that fits in your head](#fits_in_your_head)
- [Microservices are too (conceptually) big](#microservices_are_too_big)
- [Protocols of interaction: current best practice](#protocols)
- [Three years of microservices at Soundcloud](#soundcloud_microservices)
- [Building a modern microservice architecture](#modern_microservices)
- [Operating microservices](#operating_microservices)

<br />

#### <a id="netflix_monitoring"> </a>Keynote: How Netflix built a monitoring platform and why you probably shouldn't
*by [Roy Rapoport](https://twitter.com/royrapoport)*

Roy Rapoport is an Engineering Manager in Netflix's 'Insight Engineering' department, and in his keynote described how the 'Not Invented Here' problem was dealt with in Netflix when it came to creating the monitoring systems in Netflix's architecture.

Roy started with describing Netflix's culture, which is also aptly detailed in [CEO Reed Hasting's now famous 'Culture Deck'](http://www.slideshare.net/reed2001/culture-1798664) which you should definitely read. Netflix optimises their organisation to increase the speed of innovation by fostering a culture of freedom and responsibility. Netflix have an inherent anti-process bias that tends to weed out suboptimal procedures; if it doesn't work it will be corrected or abandoned.

Roy discussed '[Not Invented Here](http://en.wikipedia.org/wiki/Not_invented_here)', recommending that when you have a problem to solve in your organisation, you should ask if you are the first to have it. Most times you are not the first to have that issue which means there is good news: there are already things out there to help that you can use.

NIH happens sometimes for technical reasons that the available solution won't cut it, or sometimes for cost, or for some incompatibility with the problem domain, or in some cases when a solution (likely a product) is "overqualified".

NIH often boils down to 'not invented by us, an organisation that we can trust'. A few reasons why we wouldn't trust them are that we don't trust the technical credentials; we have been warned away from them by people we do trust; we don't trust that the other organisation has our best interests in mind (for example, they're selling us something). 

Occasionally, NIH is caused by CV-driven development. Roy argues that this is not *always* bad, as there is value in learning, there is value in improving the reputation of the company by creating a new product especially if you open-source the result, and value in keeping the developers happy in working on something challenging. I expect most people will admit this, but strongly temper it with an injection of pragmatism about when to make the decision that it is okay!

Roy discussed one method for mitigating this when using OSS; forking the project and merging contributions back into it. Roy also talked about composability of the components within your solution: consider whether you may want to replace any of these with other people's work in order to enhance the system. This would require a good separation of responsibilities across parts of the system to take advantage of such a plug-and-play approach.

[Adrian Cockroft](https://twitter.com/adrianco) once said that Netflix had invented an excellent, scalable monitoring platform that had the strange side-effect of being able to stream video to people. Netflix have invested heavily in creating a new monitoring platform as the original system which was owned by an internal IT team was not suiting the needs of Netflix as it scaled up, fast.

The new platform was created by Netflix teams because there was no good pre-existing OSS that would meet their huge scale needs (and likely for various aspects of the reasons for NIH mentioned before). The new platform which scales well, is a good match for the users who need it: developers of Netflix's many services, and it is pluggable into many other services and has been subject to [recent and impressive aggressive OSS efforts](http://netflix.github.io/#repo).

In hindsight, Roy thinks that making the platform from scratch was still the right decision given the factors considered and the needs, but that he wonders about the [sunk cost fallacy](http://en.wikipedia.org/wiki/Escalation_of_commitment) on future improvements and wants to keep a focus on pragmatically deciding where to invest and where to purchase/reuse.

Wrapping up, Roy said that when addressing NIH issues, dig in and find out which reasons are actually important to you. Find out if it's really a technical decision, and if there is any way you can mitigate the effect while still meeting the needs.

<br />

#### <a id="fits_in_your_head"> </a>Microservices: software that fits in your head
*by [Dan North](https://twitter.com/tastapod)*

Dan North took to the stage for the first talk on the 'Taming Microservices' track. Dan started by seeking to identify a shared context with the audience - advocating that the purpose of creating software is not for the software's sake; reminding the audience that they are employed not to write code but to create a positive impact for the business. The goal, Dan says, is to sustainably minimise lead time to business impact and that is the larger scope at which our improvements should be aimed.

Dan has argued for some time that software itself is not an asset but a liability, so producing more code is less valuable than making the software more effective. The costs (as well documented across the industry) cover not just creating the code, but understanding and maintaining it on an ongoing basis. The biggest problem to software development is the code in the system that nobody knows about, as this is expensive and risky to maintain. The best way to deal with this is to stabilise the offending code or kill it off.

Dan describes two complementary patterns for understandable, maintainable code: 'short software half-life' and 'fits in my head'. If you've seen Dan's talk on 'Accelerated Agile' or attended his workshop on 'Software, Faster' then these may be familiar to you. 

Short half-life results from the replaceability of discrete components with clear boundaries and defined purposes and responsibilities. Again, use of DDD bounded contexts here for defining the separation of responsibilities at different levels of granularity in the domain. Optimising components for replaceability: component tests at boundaries and good documentation on interfaces can help defeat the sunk cost fallacy when it comes to endlessly stabilising a gnarly or poorly understood component instead of replacing it.

'Fits in my head', a metric originally inspired by the length of a class on screen compared to [James Lewis'](https://twitter.com/boicy) head but not generally referring to the ability of a person to understand the conceptual whole of a component at a given level of abstraction, is used to judge whether or not other people on the team can reason about the component with the same context as whoever designed or first implemented it. This is useful as the  contextual consistency for the person understanding the component is more important than homogeneity across implementation methods, so that freedom is left to meet the needs inside the component in whichever way is best, but the people making decisions about it will come to similar decisions as the designer/implementer would have. When you have this contextual consistency you can trust that the decisions people make that result in different outcomes have been driven by different needs rather than arbitrarily.

Dan described the approach of splitting these components into services that together fit the business need as a 'replaceable components' style (no doubt familiar to anyone who understands the original intent of SOA). To reduce coupling these components should be isolated from each other and should communicate by passing messages through well-defined APIs. Implicit coupling between components can be identified by heavy use of mocks - over-dependence on mocking implies you are too tightly coupled to the behaviours of other components.

Having largely happened to not use the term throughout the talk, Dan finished up by stating that the microservices approach you've heard throughout the conference (and would no doubt hear more of on the final day) can be the replaceable component style when you focus efforts of design of the micro services upon replaceability and consistency of intent. Dan is also collating the patterns he talks about in his conference presentations and workshops in a WIP [book available on LeanPub](https://leanpub.com/software-faster).

<br />

#### <a id="microservices_are_too_big"> </a>Microservices are too (conceptually) big
*by [Phil Wills](https://twitter.com/philwills)*

Phil Wills, Senior Technical Architect at The Guardian was up next to talk about microservices based on his work at The Guardian. The Guardian has been doing this kind of work for quite some time and there seems to have been a lot of cross-pollination between them, GDS and Thoughtworks in the last few years so interesting to see how these ideas have been proliferating in the background. The Guardian website apps and site rely upon a Content API for the article data, and various other APIs for comments and so on, composed in a front end for different platforms. The Guardian has a strong focus on developing in-house tools to meet their needs for continuous delivery.

Phil explained that the main reason The Guardian had pursued a microservices architecture was for faster innovation in a high pressure media marketplace. Independent teams were needed for the different functional areas of the platform, and as on the old platform taking something experimental from a Hackday and putting it into production was prohibitively expensive, the organisation wanted the teams to be able to work independently from each other and release rapidly without overhead.

Phil discussed the lessons learned from past issues caused on the system by events like the Wikileaks Q&A event - live answers to questions posted in the comments section by readers caused a backlog of comments and a strain on the system that caused the commenting components to grind to a halt. The main application monolith depended on the response from the comments component and failure carried over, slowing the main system even for users who were not accessing the Wikileaks event content or comments. Isolating components as 'micro apps' was one of the main results of dealing with this issue, in order to limit the scope of failures.

With the 'micro app' approach, teams at The Guardian were developing independent products with ownership inside the team. This made removing and replacing parts much easier than the pain caused when they tried to do this with the monolith application. Teams were no longer dependent upon each other for releases and making changes to their interfaces backwards compatible reduced interdependencies. Phil mentioned how it was important for each team to own their own datastore and to prohibit integration via DB so as to maintain the benefit of cleanly defined APIs.

Each application had a single responsibility, and a [single key metric](http://leananalyticsbook.com/one-metric-that-matters/) that would tell teams about its performance, in terms of that responsibility. Different applications change at different rates, so we want them not to depend on each other, as this would restrict them to the lowest common denominator.

Another change The Guardian teams took was in moving away from synchronous dependencies when requesting information from other applications, whereever possible. They wanted as much as was possible for apps to be able to crash without causing problems for users (and therefore the business). An example of this is in the way that front end sports pages are composed: a front-page application for UI composition responsible for asynchronously calling a 3rd party sports stats service, advertisement service, comments service, getting article text from the content API. This way if the comments service implodes the rest of the page loads and all is not lost.

Phil warned of being wary about shared libraries, as shared libraries reintroduce coupling and create contention between teams again when it comes to making changes. Phil wrapped up with the statement "Yes, I've heard the 'if you can't build a monolith then microservices won't help' comment that has been passing about, but if you have a good team that can build a monolith, and a good team that can build microservices, I know which one I'd rather have".


<br />

#### <a id="protocols"> </a>Protocols of interaction: current best practice
*by [Todd L. Montgomery](https://twitter.com/toddlmontgomery)*

Todd L. Montgomery's talk was on the importance of protocols for addressing the reliability and safety of communications between and within systems, and how we can use those lessons to design the interactions between microservices. Given the nature of a microservices architecture tends to result in distributed systems, Todd advocated for understanding of these scenarios to understand how the services should handle requesting things from each other.

Todd began by describing some of the issues of service communication that can be observed and sometimes addressed in protocols. Data loss, duplication and reordering as the most common issues tackled and can happen even in protocols portrayed as 'reliable'. In [TCP](https://www.ietf.org/rfc/rfc793.txt), for example, connections can be closed or traffic interfered with by proxies. 

In request/response synchronous comms, throughput is limited by the round trip time for each communication multiplied by the number of requests. Asynchronous communication can reduce this to closer to the round trip time for a single communication but responses require correlation to original requests and this therefore adds complexity. Ordering of messages is an illusory guarantee, as the compiler, runtime environment and CPU can change ordering in real terms, so ordering is imposed upon events by the protocol.

Timeouts and retries are common areas of difficulty - spurious retransmits (when a response comes back just after the original request timeout) can be reduced by using measurement of recorded response times to adjust timeout. Avoiding conflicts in repeated messages should be handled by making requests and retransmits idempotent operations in case of double processing. Any protocol advertising reliability needs to deal with retransmission (for example checking a retransmit ID for having an original message processed already).

Protocols should also handle lifetime management for the communication, using caching algorithms where appropriate, performing a keep-alive using some kind of liveness check and optimising with approaches like specifically informing the other end that you are going away on error or finish, rather than relying upon timeouts. To me, these particular aspects of communication seem especially useful to microservices in the context of monitoring the service environment, for instance health checking components, handling failure scenarios when dependencies are unhealthy and both alerting and providing degraded functionality where possible.

In scenarios when multiple recipients are sent the same data set, if each recipient requests a retransmit of a different part of the data set, it will cause a retransmit of the entire set even if between them the entire set was accepted - a common problem when distributing loads across horizontally scaled consumers. Solving this is non-trivial, and Todd recommends a combination of patience, and waiting to listen for possible retransmit requests from all recipients. Todd also covered a few other examples I have omitted from this post for the sake of brevity, but for those interested you should check out the [slides from his talk](http://www.slideshare.net/toddleemontgomery) for more.

For queue management, Todd recommends using a bound total queue length and using back pressure or even dropping messages to ensure minimisation of the queue contents. Extended queue lengths leads to '[buffer bloat](http://en.wikipedia.org/wiki/Bufferbloat)' and delays between services (large queues between work states being a cause of delays should be known to anyone familiar with queuing or [ToC](http://en.wikipedia.org/wiki/Theory_of_constraints)).

Todd concluded by summarising that existing protocols such as TCP, [Aeron](http://highscalability.com/blog/2014/11/17/aeron-do-we-really-need-another-messaging-system.html) and [SRM](http://en.wikipedia.org/wiki/Scalable_Reliable_Multicast), are full of patterns for tackling complicated communications problems, and that we should look to how others have solved these problems when working on our own systems.

<br />

#### <a id="soundcloud_microservices"> </a>No free lunch, indeed: Three years of microservices at Soundcloud
*by [Phil Calçado](https://twitter.com/pcalcado)*

Phil began his talk on exploring, adopting and using microservices at [Soundcloud](https://soundcloud.com), a music uploading and sharing site, with a quick summary of scale: 11 hours of audio are uploaded every minute. Given the needs for processing and storing this quantity of data (that's about 660 days of sound every day) and serving it to ~11 million users each day, it seems Soundcloud have a lot riding on their platform.

Phil opened by referencing again [Martin Fowler](https://twitter.com/martinfowler)'s blog post on [microservice prerequisites](http://martinfowler.com/bliki/MicroservicePrerequisites.html) as the bar for "you must be this high to use microservices" - a common citation at this year's conference. Phil said that rather than falling in to it, a conscious attempt should be made to be prepared to use microservices as your architectural style due to the requirements it places on development and operations maturity. Initially a ruby on rails monolith (like Twitter pre-microservices), the teams at Soundcloud decided to break this apart and rewrite parts in [Scala](http://www.scala-lang.org), [JRuby](http://jruby.org) and [Clojure](http://clojure.org/) (clearly favouring the JVM, it seems).

The three aspects of this that Phil found most important at Soundcloud were rapid environment provisioning, basic monitoring, and rapid application deployment. The first of these, provisioning, looked a little different in 2011 than it did now when Soundcloud were preparing for what they thought would be the "microservices explosion". With [Heroku](https://www.heroku.com/) as the example, using [Doozer](https://github.com/ha/doozerd) for service discovery, [LxC containers](https://linuxcontainers.org) and the [12 Factor principles](http://12factor.net), Soundcloud managed to put together a provisioning platform much better than any other complete solution around at the time. 

However, with no resource limits on containers and a naive scheduler, Phil says that they found the had "noisy neighbours in the datacentre" - exactly the problem they moved away from shared hosting to solve. Phil says that at this stage what was important was knowing that the solution they had found that had worked so far was not the end one.

In terms of telemetry and monitoring (another hot topic at QCon this year), Phil described how in 2011 the tooling available was not quite what it is today, and dissatisfaction with some common tools led Soundcloud to build their own system. Interestingly, some of the former Google Site Reliability Engineers that had been hired by Soundcloud advocated this as they missed the detailed monitoring when moving away from the Google platform. Moving from a solution of [Statsd](https://github.com/etsy/statsd), [Graphite](http://graphite.wikidot.com) and [Nagios](http://www.nagios.org),  Soundcloud developed and subsequently open-sourced [Prometheus](http://prometheus.io) as their metrics & monitoring system, with use of [Icinga](https://www.icinga.org) and [PagerDuty](http://www.pagerduty.com) for alerting.

Teams at Soundcloud were also reorganised - component teams became feature teams with more vertical responsibility (surprisingly no explicit call out for Conway's Law).

In trying to identify easier the components that break in a microservices architecture, Phil described how with a monolith there's one obvious answer to the question of what's broken: the monolith. With microservices, it's more complex to identify the specific causes of problems, so something Soundcloud did to tackle this was to add standardised metrics dashboards and admin interfaces to each service. [Twitter-server](https://github.com/twitter/twitter-server) was used to meet some of this need in Soundcloud's platform.

The second of the three aspects Phil talked about was deployment. Soundcloud moved from a two-pronged delivery pipeline using make and [Jenkins](http://jenkins-ci.org) where Jenkins ran many sets of tests but did not build the artefacts which would actually be deployed, to a singular pipeline of Docker containerisation for unit/integration tests before commit to source, then Jenkins running a wider set of tests on the latest code, generating packages either for including in an AMI for AWS deployment, or for containerisation to allow developers to run a 'mini-soundcloud' for dev/testing purposes.

Phil admitted he realised he was nervous having read Martin Fowler's microservice prerequisites post because he had realised that they had 'messed up' having made their own tools and not incremented towards the now existing public solutions. [Adrian Cockroft](https://twitter.com/adrianco), former Netflix CTO, made Phil more reassured when he pointed out "hey, you think Netflix got it right first time?". I think having also watched Roy Rapoport's keynote I agree; that Soundcloud were doing their best to meet the needs they knew at the time and also as a by-product were creating some good stuff (like Prometheus, for example). Phil finished up his talk by specifically calling out the good things he sees that have come out of the journey (aside obviously from successfully operating the business, I assume!) - the Prometheus open source project, and highly recommended the 12 Factor App approach and [Finagle as a high performance JVM service project](https://twitter.github.io/finagle).


<br />

#### <a id="modern_microservices"> </a>Building a modern microservice architecture
*by [Yoni Goldberg](https://twitter.com/yoni_goldberg)*

Yoni works with [Gilt](http://www.gilt.com), a site specialising in flash sales for designer brand goods. Yoni's talk was on how Gilt had moved over the years from a monolith to a microservice architecture to try and deal with the pain of handling their common demand spikes and fixing and improving parts of the system.

The flash sale based business model Gilt has is based around huge though predictable spikes in demand, and in 2009 their approach was to launch thousands of instances of their Ruby on Rails application, which had increasingly complex routing and put a great strain on their [Postgres](http://www.postgresql.org) database. The monolithic RoR app had upwards of 1000s models and controllers, many code contributors but not a lot of ownership, and developers were finding it hard to identify the root cause when issues occurred.

Yoni described how Gilt made three main architectural changes to their application: moving the application platform to the JVM (primarily Scala) for perceived platform maturity, the stability & concurrency benefits and the garbage collection; refactored the single Postgres database into dedicated data stores for different parts of the application; and began splitting the monolith up by behaviours, which Yoni called entering "the era of macro and micro services".

Initially splitting the application into a small number of services met the majority of the scaling needs but most of the developer pain was not solved: the new services became almost monolithic due to size and internal complexity and still the codebases had little 'ownership' and integration and deploys were painful.

The team at Gilt then doubled-down on the microservices approach, reducing the scope of individual services and empowering the teams as the owners of the service responsible for the deployment and focusing on continuous delivery as a means of streamlining the releases. APIs used for the microservices to communicate with each other were defined by an 'API design committee' in each team and documentation generated using Swagger. The front end was decomposed into a larger number of [Play](https://www.playframework.com) and Scala applications responsible for different sections of the website. For example, the search pages, product pages, checkout and so on are all served by different apps.

Yoni described how the teams moved from their 'v2' to a more consistent approach across teams he called their 'v3'. v2 used SBT almost entirely for build and deploy, with multiple plugins and custom behaviours. A tool Gilt developed called 'Ion Cannon' was used for canary releases and rollbacks, and an `sbt release` command to push a service to production. v3 moved to immutable infrastructure: deploying Docker containers using [Amazon Elastic Beanstalk](http://aws.amazon.com/elasticbeanstalk). Each department had a separate [AWS](http://aws.amazon.com) account and budget allowing them to manage deployments entirely separately. One of the changes they noticed this implied was that they ended up needing AWS skills available to each team.

Data ownership was devolved to the teams operating the services, and each team chose the best solution for storing their data. Managing databases, a schema evolution manager independent from the service code was responsible for DB changes, deploying updates as tar files to be applied to the database. Fix-forward was the approach taken to DB migration, with no rollbacks.

Yoni also described the concept of 'mid tier microservices' which exist to aggregate multiple calls to many fine grained services (for example a 'customer' mid-tier service aggregating calls across half a dozen or more specific 'customer account' or 'customer profile' type services) to cache, decorate and collect results needed by other depending services. To me, it seems like needing an aggregating service to reduce chattiness and messy multiple calls to so many finer grained services might indicate that you have split services too far, and perhaps to roll some functions together into a unified domain concept. This however would need balanced; finer grained services are more easily understood in detail but offload the extra cognitive complexity into accidental complexity when it comes to organising calls across many services to build up the data your service needs, and obviously have operation and deployment overheads.

<br />

#### <a id="operating_microservices"> </a>Operating microservices
*by [Michael Brunton-Spall](https://twitter.com/bruntonspall)*

Michael Brunton-Spall, a Technical Architect at [GDS](https://www.gov.uk/government/organisations/government-digital-service) had the final talk of the conference, on the impact of running microservices in production and the implications that has further upstream. Unfortunately I had to skip this talk in order to make my flight, but I managed to watch it online on the InfoQ website thankfully.

I think it's worth calling out as good that Michael made most of his third person references in the female gender: for example "When your CTO comes back from QCon, she'll say she wants to use microservices" and "she will describe how teams can own the whole stack", and so on. I heard a little more of this at QCon than before and I think given the imbalance and lack of diversity, it's important to normalise the notion than other people in tech are in fact women (despite the immediate audience diversity levels).

Michael listed the three main reasons that your CTO will return from QCon and want her teams to try it:

  1. Small owned systems can be updated more easily and frequently
  2. Teams can move fast and break stuff
  3. Teams own the whole stack

Michael then went on to list the three main reasons that Ops teams hate the idea of microservices: 

  1. Small owned systems can be updated more easily and frequently
  2. Teams can move fast and break stuff
  3. Teams own the whole stack

The reasons ops teams are reluctant to embrace this is obvious: most ops teams are held to preventing risk, preventing downtime, preventing failures - things that microservices embraces but which threaten the central control of the ops team (whole stack ownership in particular). And to an extent, ops may feel like the development team is trying to obsolete their jobs.

When you want to try microservices, what you're trying to do is essentially reorganise the business. In terms of microservices as a set of patterns, some ideas already existed but are coming back up in prominence because the role of engineering and ops is changing. The wholesale outsourcing of development, operations and technical decisions is slowing or reversing thanks in part due to agile and DevOps. Michael says that though people say "we want to deploy 100 times per day but ops won't let us", ops aren't actually the constraint so much as they are just perceived to be.

When the team is wholly responsible for the application, they need to invest first in automating the infrastructure, in creating monitoring tools that are easy to use for both infrastructure and the developers, automated log aggregation using the likes of [ElasticSearch](https://www.elastic.co/products/elasticsearch), [LogStash](https://www.elastic.co/products/logstash) and [Kibana](https://www.elastic.co/products/kibana). Michael also joined the chorus in referencing Martin Fowler's blog post on Microservice Prerequisites which is getting a lot of love at QCon.

Michael also advocated for choosing cloud-friendly databases, data persistence mechanisms that have clustering as a core feature and that can handle a machine going down or being replaced. Automating deployments with a [blue/green deploy pattern](http://martinfowler.com/bliki/BlueGreenDeployment.html) by deploying new app instances, adding them to the load balancer, checking health and then taking the old instances down can be used to ensure that your platform maintains uptime during upgrades.

Though Michael suggested giving the keys of the kingdom to the development team, he balanced it with also recommending giving them pagers - [with great power comes great responsibility](http://i.imgur.com/vS0BbKH.jpg), after all. Michael also cannily points out that while few disagree with the statement "You break it, you fix it", many teams will start to wish for the 'safety' of the ops silo when this is reframed as "You break it and cost £X million, you take the blame". Developers working on these applications should be the ones to handle the support, the 3am pager calls, to feel the pain of issues caused in production instead of just seeing defect tickets raised.

Michael also points out that microservices are going to fail in more spectacular and interesting ways than monoliths. Developing a system from microservices is simpler at the individual component level but undoubtedly a complex system overall. Diagnostics tools and monitoring are needed to trace problems across services. One pattern Michael recommends is the health check: a status page simply returning HTTP 200 OK for shallow checks, and another page touching downstream dependencies that does a deeper check. Have a look at my previous blog post for [how to implement health checks in Java using Dropwizard](http://willhamill.com/2014/12/04/application-health-checks-with-dropwizard/).

Michael also showed admin interfaces and management pages for services, allowing more control over their behaviour once running. Fundamentally, as distributed systems, microservice architectures need to embrace the likelihood for failure, and this needs to be considered during design. Network latency spikes for example are indistinguishable from network partitions - the common misconception is that a network partition is only something that happens when a fibre is cut between data centres.

The ops people will become consultants to the development teams and assist them on their journey towards ownership of deployment, operation and support. Though some learning will be inevitably be required to handle the change, they'll be getting involved to automate and document these things with the team. When dealing with ops handover of microservices when rate of change slows and the team moves on, Michael recommended that good documentation be left with the ops people and that maturity models such as 'has had less than N faults in M weeks' be used to determine when a service can responsibly be passed over.


