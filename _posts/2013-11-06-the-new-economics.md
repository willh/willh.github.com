---
layout: post
title: "The New Economics"
description: "My thoughts on System Thinking and Statistical Process Control applied in software development after reading W. Edward Deming's book"
category: 
tags: ["management", "systems thinking", "people", "statistical process control"]
---
{% include JB/setup %}


A few months ago I read [The New Economics](http://www.amazon.co.uk/dp/0262541165) by W. Edwards Deming and I've been taking a few notes here and there to try and collect my thoughts afterwards. [W. Edwards Deming](http://en.wikipedia.org/wiki/W._Edwards_Deming) is considered the father of management science and is partially responsible for the revolution in Japanese industry in the 20th Century, and the focus on 'building quality in' rather than quality by inspection, so I was interested to see what kind of principles I could learn and potentially apply in a software development context.

I had encountered the [Plan-Do-Check-Adjust cycle](http://en.wikipedia.org/wiki/PDCA) (PDCA or Deming Cycle) some time ago, and after a [Hackathon](http://www.nhshackday.com) this year discussed with one of the medical doctors present how they were using it to focus continual improvement and scientific reasoning about change in the organisation, so I ordered this book from Amazon after assuming that it would contain the 14 principles described in [Out Of The Crisis](http://www.amazon.co.uk/dp/0262541157) but potentially be more relevant being a more recent release. Spoilers: Out Of The Crisis is your go to book for the 14 principles for Deming's description of a system of management - this book is actually more about systems themselves, the people that they impact and the means by which to analyse them, though it does reference the 14 principles.

I really enjoyed this book and the lessons I learned from it were quite similar to [The Goal](http://www.amazon.co.uk/dp/0566086654) in the use of statistical analysis and system-thinking approach to solving problems within an organisation and within a workflow. I also found though that it was a surprisingly very empathetic, humanistic attitude towards how people work and their coordination towards a goal with the direction of management.  




## Ranking, Rating and Traditional Reviews

Deming is well known for his outspoken views on ranking and rating employees using traditional merit systems, though many enterprises still seem wedded to it (and some more than others). According to Deming "*Ranking is a farce. Apparent performance is actually attributable mostly to the system that the individual works in, not to the individual himself*". This still seems pretty controversial to me and I struggle to conclude what I think about it overall. I certainly think that the forced ranking or fitting of any assessment to a bell curve (as happens at some larger companies I know of, particularly some financial companies) is at best disingenuous and at worst a dishonest malpractice designed to limit bonus pots and stratify the organisation. 

I also think it's possible that I have done well by being in the right place at the right time throughout my career to get the opportunities that I have had, to serendipitously 'tick the right boxes' and gain certain experiences that others of my intake cohort or my ability have not happened to have. Deming says that "*Reward for good performance may be the same as reward to the weather man for a pleasant day*". Perhaps that's simply the first signs of [Impostor Syndrome](http://en.wikipedia.org/wiki/Impostor_syndrome), but given the [incredible talent](http://www.kainos.com) that I am lucky to be able to surround myself with on a regular basis in work, part of me wonders why everyone does not get the same equitable feedback or reward? I do think that the opportunities/experiences some have had have simply happened to limit their chances for exposure or appreciation at any given time. Very few are truly outside of the standard deviation.

Deming argues that the ranking system introduces competition between people and diminishes cooperation. It encourages short-term performance over long-term planning. He answers the question "*How could you know whom to give raises in pay to if we don't have a merit system?*" succinctly: "*Everybody within the system. There will be no No 1, No 2, No 3  as there will be no ranking. Anyone outside the control limits is in need of special help. What to do? Easy. Abolish next Monday morning the merit system in your company.*"  




## Systems Thinking: Competition vs Cooperation

A system is a collection of functions with a constancy of purpose. Sub-divided parts within that system must understand the goal and must work together towards the goal without acting as a selfish, localised profit centre. Particularly inside an organisation, internal competition is poisonous compared to internal cooperation. Deming hammers it home early on: "*The secret is cooperation between components towards the aim of the organisation. We cannot afford the destructive effect of competition*". This can all too often be seen in organisations as they grow larger. The organisation is split into silos or 'business units' or 'divisions' or some other grouping and then they are usually pitted against one another through short term goals, financial incentives and other cooperation destroying targets. Bickering over costs and revenues between components caused by competition harms the system as a whole. 

Take the example of divisions of IBM UK and IBM Ireland competing against each other for the same contract with a customer. Doesn't that boggle the mind?! Who cares if UK gets it or Ireland gets it - it all bubbles up to the same IBM at the top, right? Well, yes, but that's not how the targets and profit & loss sheets for each individual department work regardless of the holistic system presented to shareholders. And the result of the competition is both wasted effort and potentially further driving down the cost of the contract. It is not possible for one component to win at another's expense - because they are part of a system the system loses overall. Hence the need for realisation that optimising for the individual pieces may not optimise the system. 

A component must consider how its actions work towards the goal of the system rather than its own benefit. One example I really liked from the book was how a plant manager in Toyota would get a bonus not if his own plant managed to meet some efficiency or output target, but if the entire region had met that target. This meant that ideas and improvements in one plant would be shared with others eagerly and there would be no petty competition between them for resources that would cause one to win while others lose. This is sublime in its simplicity. Imagine if project managers at your organisation had bonuses based on targets assessed at the whole-company level on a longer term and not at a project level on the shorter term. They would feel freer to make those decisions and investments with a short term cost which would pay off for the system as a whole (such as greater staff training, better tools and so on).  




## Statistical Process Control

One of the main themes was the idea of statistical process control and the process of attempting to ensure better quality output of work by reducing the spread of quality caused by common causes of variation, and eliminating factors which lead to special causes of variation. A common cause of variation is a natural statistical fluctuation within probabilistic bounds, such as flipping a coin three times and occasionally getting three heads - a result that needs no real explanation. A special cause of variation is an attributable-cause event such as productivity loss in the dev team caused by a flooded server room - a result in which we would be interested in an explanation and in finding ways to prevent the event from recurring.

In particular, Deming implores us not to confuse a common cause of variation with a special cause of variation - and vice-versa. He quotes Brian Joiner "*One necessary qualification of anyone in management is to stop asking people to explain ups and downs that come from random variation*". I was finding it difficult to cement this in my head with a concrete example but Deming uses the case of the employee who comes to work between 10 and 15 minutes late every single day. Allow me to paraphrase it by attempting to recall it from the top of my head: 

An employee thinks that every single time he is late, it is because of some special cause: a traffic accident, bad weather, no parking space (etc etc). Over time, however, this trend has entered statistical control - it is entirely typical for the employee to be between 10 and 15 minutes late. The appropriate response to this is not to seek to address every single one of these supposedly special events but rather to adjust the input based on the knowledge of the normal behaviour of the process - and as a result, to get up 15 minutes early and always end up on time.  




## Whatever Mate, Go Back To Manufacturing

"But Will", I hear you say. "We don't work on the factory floor making widgets for a Toyota subcontractor, how is this relevant to us?" I understand this criticism - it seems Lean and other forms of process level approaches sometimes come under this criticism and I can see why. Knowledge work is not the same as the process- and input-constrained practical or mechanical (for want of a better word) style of work that inspired these approaches to management and the people involved have more of an input on quality outcome than machine operators - but a significant impact still remains due to the quality going in and the constraints of the system, as in traditional engineering, and I believe a systemic overview can still be of benefit. 

Deming's lessons for management are relevant in any organisation where people are paid to work for other people, and his comments on the ranking system are at least good for starting a conversation on how your organisation operates, if not to be used to throw the system out. The statistical process control approach however is probably more alien to knowledge workers but I think still relevant. My closest experience to this workflow based regular output cadence is in developing user stories toward a story-point based estimate in an agile software development approach. It is easy to see over time, that once the system (the team) has an output (producing features measured in points value) which enters statistical control (velocity across sprints seems reasonably level) that the same principles can still apply.

*Don't treat a common-cause variation as if it was a special-cause variation*

If the team has produced an output of developed features in story points thus: `[10, 8, 11, 9, 14, 12, 8, 13, 10, 9, 14]` then this gives us an average of around 10 or 11 points per week, and a control range of from 8 to 14 as our upper and lower bounds. So if next week the team produces 8 points worth of work, don't stress out and start blaming people and try and find out what the big problem is that caused this downturn ("What happened? Our average is 11 points! Last week you did 14 points! We were doing so well!"). This is likely just common variation due to all of the normal variation-causes like the fact that estimates are estimates and not clairvoyance, stuff that doesn't really have a single cause *as such*. 

Continue normally and use retrospectives and other feedback loops to draw out what wasted people's time or held them up and other inefficiencies - assuming we want to attempt to reduce the common variation and improve predictability - which can be done by continually improving the process. We keep doing the feedback loops in case this was actually going to end up a 14 week but something did happen that brought us down to the low end. Just because it is nothing to worry about doesn't mean we're not interested in the details of the progress and doesn't mean we should not focus on ongoing improvement.

Equally if the process has not yet entered statistical control (hasn't settled down after some time), then the output on the second week at that time should not yet be deemed a drop in quality or productivity as we don't know if this is significant yet. So hopefully no "What happened, last week you did 10 points? This week only 8?" and so on.

*Don't treat a special-cause variation as if it was a common-cause variation*

If the same team above for the next week produced developed features totalling 4 points then this should be so significantly below what we previously assumed was the lower bound in a normal process (in statistical control) that it warrants investigation. Don't write this off as just the normal ebb and flow of a team dealing with natural rhythms - the statistics alone suggest this could be more important. 

However - by returning to the principles that Deming outlined earlier the appropriate response here is also not to start stress out and blame people! Through retrospectives and other feedback loops find out what happened and if an actual assignable cause was the originator of this result and take action to find the cause of it and try and prevent it from impacting upon the team again.  



