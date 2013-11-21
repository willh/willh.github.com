---
layout: post
title: "Kanban: Beyond the Board"
description: "The Kanban Method is a lot more than just cards on a notice board. Using the principles of Kanban you can evolve your current process into a process of continuous improvement."
category: 
tags: ["kanban", "agile", "lean", "management", "systems thinking"]
---
{% include JB/setup %}

Many agile development teams today use a task tracking board to display their work. These boards help visualise work that is underway and the stages through which work should pass. I hear that these teams (and I’ve said it myself in the past) are “taking elements of [Kanban](http://www.amazon.co.uk/Kanban-David-J-Anderson-ebook/dp/B0057H2M70/)” into their process by adding a task tracking board. But just sticking the work up on post-its or cards on the board and then visualising the work (while beneficial) is only one small aspect of Kanban itself. 

There are many beneficial aspects left beneath the surface of this approach which can help teams begin and continue to improve their work. “Doing Kanban” means restricting concurrent work-in-progress (WIP limit), progressing work with a 'pull based’ system, and working to optimise flow through the system. If you’re not considering these things, you're just adding a board to your current process.

Considering, understanding and using the values and practices behind the Kanban method can help you change and better the process you currently have - much like embracing the practices behind the Agile Manifesto rather than being beholden to any particular textbook implementation. In this post I want to talk a little about Kanban and its core concepts, and an example of how you can apply the approach to improve your way of working.




###The History

Kanban (with a capital ‘K’) was formulated over the last 8~ years by [David J Anderson](http://twitter.com/lkuceo) and draws on principles from the [Theory of Constraints](http://en.wikipedia.org/wiki/Theory_of_constraints), [Toyota Production System](http://en.wikipedia.org/wiki/Toyota_production_system) and [Lean](http://en.wikipedia.org/wiki/Lean_software_development) in order to create a way of improving and evolving processes and systems without the friction and emotional inertia of a big-bang all-change transformation. 

Kanban takes its name from the Japanese term *kanban* or signal cards (with a little ‘k’) used in the Toyota Production System to signal downstream that work is ready to be ‘pulled' from one state to the next. This ‘pull-based’ system, whereby workers begin work on a task only when finished their current one and are responsible for allocating themselves work when they have capacity (rather than upstream workers pushing the work onto the next person) is one of the cornerstones of Kanban, and is a component of empowering the team.

Kanban has four main principles describing the intent of the method and six supporting practices which enable the evolutionary process change.




##4 Principles


**Start with what you do now**  
Kanban begins with your current process. This is probably the biggest differentiator from other agile or lean approaches in that we don’t start with a new process straight away. There is no such thing as a Kanban software development process as such.

**Respect current job titles and responsibilities**  
At least at first, avoid changing titles and responsibilities. People aren’t resistant to change, they’re resistant to *being changed*. Many big-bang agile transformations suffer from resistance because people are threatened by the idea that their skills are no longer useful.

**Agree to pursue evolutionary change**  
This is the foundation of the Kanban approach - Kanban is a method of evolutionary improvement. It should be easy enough to get the team to agree that the current process can be improved and to work towards its improvement.

**Encourage leadership at all levels**  
All team members from management down to individual contributors should be enabled to identify waste, improvement, value to add and beneficial changes in the process. This is not intended to be a top-down change management method.




##6 Practices

**Visualise workflow**  
Show work items and states in a visual process flow; on a virtual board or physical kanban board. A Kanban implementation doesn’t need to have physical cards (and that can be different with distributed teams). A virtual board representation in a task tracking system can be used too (I like [Trello](http://www.trello.com) personally).

**Limit work in progress**  
Focus on completion and reduce multi-tasking to improve efficiency and to reduce the time wasted context switching.

**Measure and manage flow**  
Using pull-based allocation, record the lead time and cycle time for items in the process. Focus changes on reducing cycle time and variation, and identify bottlenecks in the system by measuring both end to end and from state to state and using the visualised workflow.

**Make policies explicit**  
By realising that a process is a set of policies, the process can be changed by changing the policies for how work flows. Make policies explicit to empower workers to pull work through the states and to identify the effect of changes of policy on the system. The transparency created by identifying exactly how work progresses through the system is also empowering for team members.

**Implement feedback loops**  
A fundamental agile principle; use retrospectives, operations reviews and other feedback loops as appropriate in order to identify changes, reflect on the current system and draw out potential improvements to the process.

**Evolve the system using a model based approach**  
Use a model based method to identify and exploit opportunities for positive change, for example bottleneck identification and elimination in Theory of Constraints; using Systems Thinking to optimise the system rather than the parts; and/or Deming’s System of Profound Knowledge to reduce variation in flow.




###A Systems Thinking Approach

This sounds like a lot, but in reality it's more of a mindset shift towards changing the current process for the better and the things that are required to enable that. It's not like jumping into Scrum straight from a waterfall methodology, and it can be used to take a Scrum-based process which may have stagnated towards a process of ongoing improvement.

[After reading The New Economics](http://willhamill.com/2013/11/06/the-new-economics) by [W. Edwards Deming](http://www.amazon.co.uk/dp/0262541165) I found myself coming back to some of the things I read in the Kanban book and noticing the focus on a higher level elimination of variability, a systems-thinking approach to process optimisation (over local optimisation) and the same empathetic approach to dealing with people. Anderson includes numerous experiential anecdotes illustrating these concepts such as how avoiding local optimisation (peak utilisation for all workers) by creating slack in the process seems to add inefficiency but at the bigger picture allows for time to be invested in things like training and addressing technical debt to enable continuous improvement and therefore the improvement of the process overall.




###The Operations Review

The Operations Review is a feedback loop described like a kind of cross-project retrospective focusing on quantitative reporting on how the organisation is performing, rather than the low-level, higher detail qualitative result of a typical sprint retrospective. Attendees can reflect on the higher-level data provided about the processes presented and how they interact, so that they can suggest changes or improvements. 

This involves open and objective feedback from managers across projects and in which many levels staff of can contribute - also tying in with the fourth principle to encourage leadership at all levels. This seems like it would be quite beneficial in organisations in which multiple teams are using an agile approach or interfacing with other teams on a programme of work which are using other approaches. I’m not doing it justice really, you should read up about it!




###Other Goodies

In the Kanban book, Anderson talks about a few things that seem to be skimmed over in some texts on agile development methodologies, such as co-ordination between and across teams using a Kanban system. He talks in particular about using Kanban to create a lean and agile approach to software delivery with teams in maintenance mode and which deal with different service levels for bugs and urgent issues as well as ongoing development. There is some very interesting material on this and 'class of service’ for work items, which I haven’t really found a lot of good material about in other methodologies.

There are also good guidelines for identifying waste and focusing on valuable work by reducing co-ordination costs (the overhead of communication, meetings, etc - things we have to do to keep in sync with each other) and transaction cost (the overheads of setup/teardown for deployment actions etc - things we have to do simply as a cost of business). Deming’s System of Profound Knowledge is also referenced and the important difference between common-cause and special-cause variation reiterated.

One of the most interesting parts of these sections I found was the rule of thumb for identifying if an action is valuable or an overhead: ask yourself “if we could, would we do more of this?” A simple and effective way of helping discover if an action, ceremony or stage in the process is actually adding value. For a contentious example, the daily stand-up is a *necessary* overhead, as we want to effectively coordinate our team members, but if it takes 15 minutes, we wouldn't want to extend that to an hour because it doesn’t strictly contribute to the end goal.




##Implementing Kanban

Beginning to implement a Kanban approach doesn’t take a lot if you’ve already got a board covered in user stories/work items/tasks. This means you’ve at least got the visualising workflow thing under control and makes it easy to start on the next practices.

On my previous project it was a natural step for us to limit WIP for team members because we identified that too much concurrent task work was causing overheads with context switching and resulting occasionally with two things almost finished at the end of a sprint rather than one thing done and one thing nearly done (which is obviously better).

In practice, this meant using tape to draw swim lanes across the ‘in development’ column and assigning each developer a lane, to physically limit the number of cards that could be in progress at a given time.

We began to use the board to being to identify bottlenecks in the process which first resulted in the change from the state of `development -> done` into `development -> review -> done`. This helped us more accurately measure when tasks had been completed by developers and were waiting on some time from a tech lead for code review.

We had also created a ‘blocked’ state area into which we would move cards when they couldn’t progress, which allowed us to identify the obstacles to our progress. Over time, however, I noticed that things would get ‘left behind’ in the blocked area and we saw a few long-term-blocked cards of low priority which were inadvertently neglected. 

I thought that this might be due to moving cards out of a team member’s swim lane meant they were "out of sight: out of mind", so I changed this to representing a blocked task with a red tag attached to a card and removed the blocked area. This allowed us to ensure it was more visible for that team member and could be noticed at each daily stand-up meeting if it was still blocking. This seems to have been more effective at encouraging discipline around focusing attention on these blockers.

We also involved the practice of making policies explicit by more carefully documenting the definition of done for stories in order to ensure that they could cleanly be pulled from one state to another. 

Retrospective actions were stuck up beside the main story tracking wall in their respective columns: ‘do more’, ‘do less’, ‘start doing’ which helped us keep track of the tasks we took on after the retrospective to chase up and improve our process. This helped reinforce the retrospective as a feedback loop as it had a greater visual presence than simply digital notes and allowed me to glance over the actions after each morning’s stand up meeting to see if there was anything that I could specifically tackle or update at that time.

Kanban makes a specific effort to remind you that the process itself should change based on the insights your team makes about it and encourages changes to be made, tested and measured for their effect which is something that can be forgotten when we slip into the ways of just following the textbook with methodologies. There’s no point in mastering a process and then never changing it when based on the knowledge we gain about our work and ourselves on a regular basis we can attempt to foster a process of ongoing improvement - the principles behind the Agile Manifesto remind us that “At regular intervals, the team reflect on how to become more effective, then tunes and adjusts its behaviour accordingly”.




###Try Kanban

Consider the principles and practices I’ve described above and how you could apply them to your work. It doesn’t have to be a Scrum-influenced agile development process; after all Kanban is intended to be a method for evolving an existing process to become more agile, it’s not a new process you drop in instead of your current one. Making small, measurable changes is the easiest way to start.

The example I often give when training people is that of the HR department tracking applicants through a number of different states: `CV received -> telephone interview -> in person interview -> contract accepted`. This common workflow itself can be illustrated on a board easily using index cards or post-its to represent the applicants and then the process of evolving this system using the Kanban practices can begin (e.g. adding a ‘CV reviewed’ step after ‘CV received’ to identify bottlenecks in people’s availability to read through CVs).

To get more detail and a better explanation of these concepts, you should also read David J Anderson’s [Kanban](http://www.amazon.co.uk/Kanban-David-J-Anderson-ebook/dp/B0057H2M70/) book!

