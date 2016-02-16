---
layout: post
title: "The Minimum Viable Product"
description: "A Minimum Viable Product or MVP is a piece of software created with just enough functionality and to just enough of a standard to allow you to test some theory or investigate a risk. A Lean Startup uses cycles of MVPs as their scientific method to find out if they are having a positive impact."
category: 
tags: ["agile", "lean", "mvp", "hackathon", "nhs hackday"]
---
{% include JB/setup %}

### The NHS Hackday

On the weekend of the 25th of May I was lucky enough to attend the London [NHS Hackday](http://www.nhshackday.com) again. This was my third time at an NHS Hackday with the first being a year ago at the inaugural event in London and the second being in Liverpool. Both times I was accompanied by some [talented colleagues](http://www.kainosjobs.com) and as is the order of the day we [hacked][1] together on creating some application or service that could be of benefit to the public or clinicians.

This year, I worked with an enthusiastic crew of [@Steven Alexander](https://twitter.com/evilnevets), [@Glenn Sayers](https://twitter.com/glenn_sayers) and [@Shannon Holgate](https://twitter.com/sholgate13), and we teamed up with [Dr Henning Clausen](http://www.health.org.uk/areas-of-work/programmes/shine-twelve/related-projects/great-ormond-street-hospital-for-children/the-project/) on an idea he had pitched at the beginning of the event. Over the course of the allotted day and a half we managed to create a very basic but working application to record feedback from patients and their families in order to gather information on their stay or to report patient safety incidents. You can help yourself to the [code on Github](https://github.com/willh/hackday2013) if you're interested in how it works or even want to [fork][2] it yourself for reuse.

### The Minimum Viable Product

The software we produced (hosted on [Heroku](http://www.heroku.com) for demo and trial purposes) is clearly simple, basic and not entirely polished. It misses plenty of nice-to-have features and even a lot of could-have features due to the time constraints of little over a day of work. It doesn't have two-factor authentication and full data encryption. It doesn't email reports to hospital administrators and it doesn't send reminder text-messages to patients to ask them to fill in the form. And there's no app for that (beyond working nicely on mobile browsers).

*So what good is it then?*

It is a [Minimum Viable Product](http://en.wikipedia.org/wiki/Minimum_viable_product). Just enough to allow Dr Henning to test his hypothesis that creating an application using a more intuitive and a simpler design with an easily correlated and viewed data set will result in: 

1. more feedback being collected due to allowing patient to complete on their phone/laptop/iPad
2. more feedback being collected due to better completion rates resulting from simpler UX
3. data collected at site and time of safety incidents rather than just in end-stay questionnaire
3. more data being available for clinical staff to identify potential risks or recurring risks
4. a better view on the data being collected to ease categorisation and inference on the data

### It Doesn't Need To Do Everything

What we as the development team want from this is to give the ability for Dr Henning to collect a bit of data and to test these assumptions. We want something that works just enough to try and see if these points are correct, not something that ticks every possible box for features that a fully fledged hospital system should have. We want something that we can actually finish within a day and a half to see some value! :)

So if this means that Dr Henning can ask a few patients to trial the software by entering basic feedback (no personal information because of current lack of secure storage etc etc) then this may allow him to test these assumptions. In fact even if the creation of this application can convince The Powers That Be to fund development for a more fully-featured application with these goals in mind then that's a positive outcome.

### Minimum Viable means *Minimum Viable*

It's not realistic to expect anyone to create a fully penetration-tested, user-approved, secure, hardened, SSO-integrated, enterprise-connected system out of such an idea in a day and a half, and more importantly *that's not the point*. We know people can write plugins for your language of choice to allow people to sign in with their godforsaken Windows NT network credentials. We know people can probably take the output and squash it into [your data format of choice](http://i.imgur.com/ZxkGv.jpg) and we know there's probably a way to run it on your current locked-in vendor's hardware environment. What we don't know yet are the five points mentioned earlier. We are testing a hypothesis, not creating a fully production ready system.

At the first iteration of the NHS Hackday last year I saw a number teams get asked by audience and panel judges whether their fancy new app would integrate into existing hospital systems, or if it had full encryption on all the data that it was storing. Some attendees scoffed at applications created with what was interpreted as no appreciation for the hospital environment and its constraints. This time around I didn't see that, and I'm glad. Not glad because we don't want those kind of feature on a clinical-use system or because we don't want our developers to consider their target environment but because *that's not the point* of a hackathon. The point of a hackathon is to create the minimum viable product.

We can integrate and encrypt it all once we know whether or not it's actually worth investing the effort. If we can get some *basic subset of useful features* and get that infront of patients or nurses or doctors or hospital board members and it can demonstrate its worth by proving the hypothesis we set out to test then we'll know it's time to start looking at how to encrypt and integrate and all the other things we as rational and experienced solution-developers know are necessary. If people aren't willing to invest in the idea and if it doesn't let you demonstrate some sort of value then we won't have wasted the time involved in the things we already a lot about. [Integrating systems into a hospital environment is hard][3] - we know this. [Proper user authentication is hard][4] - we know this. 

The minimum viable product is valuable because it can tell you something you don't already know so that you can then make an informed decision about how to progress. A [Lean Startup][5] uses the MVP as its [scientific method][6] to tests its value hypothesis and to change course to increase the business impact of its actions.

[1]: http://en.wikipedia.org/wiki/Hacker_(programmer_subculture)
[2]: http://en.wikipedia.org/wiki/Fork_(software_development)
[3]: http://en.wikipedia.org/wiki/NHS_Connecting_for_Health#Failure_to_deliver_clinical_benefits
[4]: https://www.gov.uk/service-manual/making-software/logins.html
[5]: http://www.amazon.co.uk/The-Lean-Startup-Innovation-Successful/dp/0670921602/
[6]: http://en.wikipedia.org/wiki/Scientific_method
