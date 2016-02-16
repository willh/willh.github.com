---
layout: post
title: "Internet of Things, or Your Property as a Service"
description: "Stick a sensor in it, add wifi to it, gather all the data and show a fancy graph on the iPhone. Now you can micromanage your entire life, but what does it cost?"
category: 
tags: ["internet of things", "security", "privacy"]
---
{% include JB/setup %}

###The Internet of Things

For the last few years there has been a surge of 'Internet of Things' devices making their way into the mainstream. Aside from the tech industry's enthusiasm for attaching all kinds of sensors to the internet and beyond gimmicks like the fridge that orders milk for you when you've run out - wearable fitness trackers, beacons for tracking shipping, sensors for goal-line technology in sports, wifi-connected scales that integrate with recipe apps and the like are making their way into the new normal of our lives.

What this means for consumers is the 'service-isation' of everyday things - your property as a service. The impact of turning simple devices or appliances from a product into a service has is multi faceted. IoT devices can make a lot of things much more convenient, more intelligent when it comes to tailoring the service, embraces helpful customisation, can reduce costs and brings us data we never before had to improve decision making from business to consumer life. However, it introduces a dependency on whoever runs the service, and grants them a great deal of power and control, and adds cost, risk and uncertainty to usage. It's important to consider both the new shiny convenience and also the hidden costs or pitfalls:


###Depending on others for service

There aren’t many things that’ll take a regular dumb fridge offline other than the electricity supply being out. However, with internet-controlled devices taking the place of regular appliances across the home, you now depend on both an internet connection _and_ the manufacturer’s service for your use. Though I found a friend’s Nest thermostat impressive and intriguing, the news that the [Nest service being offline means no heat for Nest users](http://www.bbc.co.uk/news/technology-35311447) doesn’t fill me with excitement.

I recall an amusing conversation with a colleague over Skype who explained he was sitting in the dark because he was still waiting on a firmware update on his ["Smart Light"](http://www2.meethue.com/en-gb/) to finish. A small price to pay for the decadent luxury of being able to control your light from your phone instead of standing up and reaching for the switch, I'm sure. I had my own problems recently when my [Pebble Time](https://www.pebble.com) watch [decided it had fallen over](https://twitter.com/willhamill/status/691867625631170560) and left me with an expensive funny-looking bracelet. Even a stopped analog watch provides a service twice per day.

Adding connectivity, app integration, social/gamifying/whatever to dumb electronics means making even stuff that can be mechanically simple fundamentally much more complex. Crucially, given the dependence on the service operator, you are not buying a smart fridge/watch/coffee machine/bathroom scale - you are subscribing to it, even if for free.


###Lifetime of equipment

One big drawback of running your property as a service is that of planned obsolescence by manufacturers, who no longer want to shoulder the support or operational burden of the services - or who more cynically may want to force consumers to upgrade and replace more often. The lifetime of household appliances and personal electronics is significantly reduced when you tie it to security and firmware updates from the manufacturer, and an operating back end service. Contrast that with the fact that smartphones tend only to get updates for two to three years (depending on your telco's efforts), whereas a fridge or a watch can last for five to ten years without issue.

Another important fact to be aware of is that the terms you agree to now are not necessarily the terms of service in one year. Phillips drew ire recently for pushing out an update to the Hue Bridge, a kind of hub for internet-connected lightbulbs (rolled eyes too hard, stuck looking at inside of own head, please send help), which [disabled the use of third-party lightbulbs](http://www.cnet.com/news/philips-hue-cuts-support-for-third-party-bulbs/) - a feature previously relied upon by many users until that point. The company eventually [gave in to pressure and reversed the firmware update](http://siliconangle.com/blog/2015/12/18/philips-backtracks-on-hue-bridge-software-update-after-internet-backlash/) in an embarrassing climbdown, displaying their own lack of understanding of their own user base. What happens when a company doing the same thing doesn't backtrack? 

Even without accounting for changes of business strategy, acquisitions or collapse of the operating service, some products are sold with a use-by date already on the box: for example this [VR headset in which the manufacturer reserves right to terminate the app in 18 months](http://www.apple.com/shop/product/HJKB2LL/A/view-master-virtual-reality-starter-pack).


###Security

Making this criticism is a bit like shooting fish in a barrel given the last year's worth of security breaches and exploits. Starting with the small fry, there are the WiFi connected lights which will receive commands [without HTTPS or decent security](http://easybulb.com/api/). One of the biggest stories in this area recently has been the [VTech kids toys leaking data](http://www.bbc.co.uk/news/technology-35532644) for comms/pics between kids and parents.

Instead of just multifunction printers with default admin/password credentials being exposed to the internet by lazy sysadmins, it's now [WiFi baby monitors and home security cameras](http://arstechnica.co.uk/security/2016/01/how-to-search-the-internet-of-things-for-photos-of-sleeping-babies/) inadvertently being exposed by unknowing parents and even [X-Ray machines](https://www.shodan.io/host/189.70.248.193) that are accessible to anyone with a correctly crafted search query out there.

As systems are exposed via wireless networking, even if just on local networks, it adds attack vectors that didn't exist before. [Stuxnet was so impressive and hard to pull off](http://www.vanityfair.com/news/2011/03/stuxnet-201104) because the target network of the Iranian centrifuge control system was air-gapped, but as we plug more things into our home networks and add wifi to more 'dumb' electronic control systems, the potential for mischief and mishaps increases.

For example, US vendor [Target was hacked for credit card details by a heating and ventilation monitoring system](http://krebsonsecurity.com/2014/02/target-hackers-broke-in-via-hvac-company/) which was connected to their main network. Security researchers discover exploit on 'Smart' sniper rifle enabling them to [prevent firing or change target](http://www.wired.com/2015/07/hackers-can-disable-sniper-rifleor-change-target/) - not something Police hostage negotiators want to discover at the wrong moment. One Wired journalist reported on security researchers [taking control of his Jeep as he was driving down the highway](http://www.wired.com/2015/07/hackers-remotely-kill-jeep-highway/) and the ever-popular [Nest thermostat and camera has also been targeted for exploits](https://www.blackhat.com/docs/us-14/materials/us-14-Jin-Smart-Nest-Thermostat-A-Smart-Spy-In-Your-Home-WP.pdf).


###Ownership of data

Using the internet today in any normal sense means that your usage is [extensively collected](http://www.economist.com/news/special-report/21615871-everything-people-do-online-avidly-followed-advertisers-and-third-party), [fingerprinted](http://www.telegraph.co.uk/technology/internet-security/10982252/The-new-technology-which-advertisers-use-to-track-your-every-movement-online-canvas-fingerprinting.html), [tracked](http://venturebeat.com/2013/03/04/online-tracking/) and [sold to advertisers](https://marco.org/2015/08/11/ad-blocking-ethics). Thanks to the Internet of Things, information that companies previously would never have access to, like sleep patterns, body weight, food consumption, heart rate, [sexual activity](http://thenextweb.com/insider/2011/07/03/fitbit-users-are-inadvertently-sharing-details-of-their-sex-lives-with-the-world/), TV viewing habits and more are all now captured and indexed. Information that sometimes even your partner would not even know in this detail is being collected and [aggregated at unprecedented rates using innovating and devious new ways](http://motherboard.vice.com/read/the-internet-of-things-that-talk-about-you-behind-your-back).

It sounds like something from the book [1984](http://www.amazon.co.uk/Nineteen-Eighty-Four-Penguin-Modern-Classics/dp/014118776X/) but Samsung Smart TVs [actually eavesdrop on conversations and send all recognised speech to a third party](http://theweek.com/speedreads/538379/samsung-warns-customers-not-discuss-personal-information-front-smart-tvs). This, by the way, is not a security defect. _It is a feature._ 

We've heard of the anecdotes of the [shops being able to tell you're pregnant before your family](http://www.forbes.com/sites/kashmirhill/2012/02/16/how-target-figured-out-a-teen-girl-was-pregnant-before-her-father-did/) can and people [being able to tell if you're gay simply from your Facebook activity](http://www.theguardian.com/technology/2013/mar/11/facebook-users-reveal-intimate-secrets) of likes and interests. But most people don't realise how detailed the profile can become and how linking data together can enable advertisers and other companies to make more interesting leaps, like [how you'll vote](http://fusion.net/story/268108/dstillery-clever-tracking-trick/).

There's also a risk of abuse of the data when [employers](http://edition.cnn.com/2015/09/28/health/workplace-wellness-privacy-risk-exclusive/), healthcare providers, insurance companies and others get their hands on this new, [unprecedented level of detail about you](http://www.ft.com/cms/s/2/d7eee768-0b65-11e5-994d-00144feabdc0.html). How about if the Police want to access this data? Not a scenario the user anticipated when their [Fitbit data was used to undermine an accusation of rape](http://fusion.net/story/158292/fitbit-data-just-undermined-a-womans-rape-claim/).

Back when it was just advertisers profiling your web browsing habits it was portrayed as enabling 'targeted advertising' (as if anyone actually wants ads and the issue is the irrelevant ones). Now that simple playback devices are smarter, the targeted advertisements can [infect previously ad-free areas of your life](https://twitter.com/PaulM/status/689272494331531269) like watching a movie on Netflix (ironically a service people pay for partly because it has the content they want on demand without ads). Expect to see the same thing to happen with the IoT: slim benefits touted to users, such as fractionally reduced health insurance premiums, in exchange for an incredible amount of data on your personal and private life that can be used to better improve the provider's margins and find more avenues to wring a few pence out of you. 


###Standards

It's a jungle out there at the moment for IoT despite the term's growing age, as no major players have yet emerged to dominate the market and gobble up the smaller players. Someone with a Fitbit, Pebble, Drop kitchen scale and app-enabled treadmill won't yet find themselves with a cliché-peddling Minority Report style home and life dashboard showing how if I make these cookies I'll end up needing to do another 15 minutes on the treadmill at my usual rate, but will more likely find themselves staring at four separate apps that don't talk to each other. (For now, thankfully, I think, given the security and data ownership issues I mentioned before...)

Samsung have produced what appears to be a [well-meaning IoT hub thing](http://www.theguardian.com/technology/2016/feb/08/samsung-smartthings-hub-review-internet-of-things) which tries to solve some issue of interoperability, but many of us working in tech know what happens when you [try and solve the standards issue by yourself](https://xkcd.com/927/). In many cases, though, hardware manufacturers want you to use their smart devices but they want you to have to use their app as well because then they can create an ecosystem into which they can lock consumers (c.f. Apple). In many cases it's hard to get data out and do new things with it that the manufacturer hasn't thought of yet or just take control of your data and export it if you want to change from one wireless bathroom scale provider to another.


###Where do we go from here?

It's easy as consumers and professionals to be dazzled by the latest tech coming out of [CES](http://www.forbes.com/sites/scottdavis/2016/01/19/iot-moves-from-smart-to-wicked-intelligent-at-ces/) or the latest trends in the [Gartner report](http://www.gartner.com/newsroom/id/3165317). As Smart-$product becomes the new default $product, be aware of the new features your latest TV or scales or coffee machine have and consciously make the decision about each internet-enabled device you add to your home or business network.

It can be a slog but it's prudent to look into the security standards, change the default passwords, and to get info on how much data is collected and with whom it is shared. The IoT integrated utopia is at odds with standard security practices to restrict and isolate - so understand the compromises instead of siding with one approach over the other. 
On a practical economical sense, compartmentalise parts with short shelf lives - instead of a £700 Smart TV, buy a Chromecast/FireTV/Apple TV and a £600 vanilla TV (or given that almost all TVs are becoming Smart TVs, buy the lower featured one and don't use the Smart TV parts) so that you can replace the smart parts in three years and keep the main investment instead of throwing out the whole thing.

Consider the track record of the company you are trusting with your data or needs - big companies like Google and Apple are arguably more likely to understand and correct issues in service than non-tech companies that have bolted wifi onto something, as evidenced by the VTech data leak debacle.

Something that goes against my natural inclination as a bit of a tech magpie: don't buy version one of something. Let someone else find the bugs in the bleeding edge. Installing the latest Chrome browser and dealing with the occasional crash is fine but given the depth of data collected and the more difficult nature of hardware, be a little bit more cautious when it comes to automating your house and your personal life.

Look for smart devices that have APIs and open standards so that you can be in charge of integrating them or pulling out your data, if you so desire (e.g. choice to use the Fitbit app vs use the integrations and have data pulled into another app).

Hopefully more open and integration-friendly products will appear and at the same time more manufacturers will take security seriously - but who do you trust to be the Systems Integrator of your house? Yourself? Few will have the ability or inclination. Google, Apple, Amazon or Samsung? Given what they already know about you, should you hand them any more? If you do, do it with your eyes open and knowing what you're going to get in return.

