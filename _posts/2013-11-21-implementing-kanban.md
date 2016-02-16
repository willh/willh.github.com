---
layout: post
title: "Beginning with Kanban"
description: "Starting to implement the Kanban approach is easy as the focus is on evolutionary change. Beginning with your kanban board, start to embrace the practices and principles."
category: 
tags: ["kanban", "agile", "lean", "management", "systems thinking"]
---
{% include JB/setup %}


### Implementing Kanban

Beginning to implement a Kanban approach doesn’t take a lot if you’ve already got a board covered in user stories/work items/tasks. This means you’ve at least got a visualisation of the workflow which will easily allow you to observe the effects that changes to your process will have. This is a good point at which to consider implementing the other supporting practices of Kanban, in order to continue removing waste and improving time to value for the business.


### Limiting Work-In-Progress

On my previous project it was a natural step for us to limit WIP for team members because we identified that too much concurrent task work was causing overheads with context switching and resulting occasionally with two things almost finished at the end of a sprint rather than one thing done and one thing nearly done (which is obviously better).

In practice, this meant using tape to draw swim lanes across the ‘in development’ column and assigning each developer a lane, to physically limit the number of cards that could be in progress at a given time.

We began to use the board to being to identify bottlenecks in the process which first resulted in the change from the state of `development -> done` into `development -> review -> done`. This helped us more accurately measure when tasks had been completed by developers and were waiting on some time from a tech lead for code review.


### Dealing With Blockers

We had also created a ‘blocked’ state area into which we would move cards when they couldn’t progress, which allowed us to identify the obstacles to our progress. Over time, however, I noticed that things would get ‘left behind’ in the blocked area and we saw a few long-term-blocked cards of low priority which were inadvertently neglected. 

I thought that this might be due to moving cards out of a team member’s swim lane meant they were "out of sight: out of mind", so I changed this to representing a blocked task with a red tag attached to a card and removed the blocked area. This allowed us to ensure it was more visible for that team member and could be noticed at each daily stand-up meeting if it was still blocking. This seems to have been more effective at encouraging discipline around focusing attention on these blockers.


### Making Policies Explicit & Tightening Feedback Loops

We also involved the practice of making policies explicit by more carefully documenting the definition of done for stories in order to ensure that they could cleanly be pulled from one state to another. 

Retrospective actions were stuck up beside the main story tracking wall in their respective columns: ‘do more’, ‘do less’, ‘start doing’ which helped us keep track of the tasks we took on after the retrospective to chase up and improve our process. This helped reinforce the retrospective as a feedback loop as it had a greater visual presence than simply digital notes and allowed me to glance over the actions after each morning’s stand up meeting to see if there was anything that I could specifically tackle or update at that time.

Kanban makes a specific effort to remind you that the process itself should change based on the insights your team makes about it and encourages changes to be made, tested and measured for their effect which is something that can be forgotten when we slip into the ways of just following the textbook with methodologies. There’s no point in mastering a process and then never changing it when based on the knowledge we gain about our work and ourselves on a regular basis we can attempt to foster a process of ongoing improvement - the principles behind the Agile Manifesto remind us that “At regular intervals, the team reflect on how to become more effective, then tunes and adjusts its behaviour accordingly”.


### Simply Start With What You Do Now

In my current project I am using these principles to guide changes we consider making to the process and to the workflow. A good point to start is always by looking at what the board tells you - where we've got a lot of items in a state marked 'Awaiting Review', these items actually represent features that are awaiting review, features currently being reviewed by a tech lead and co-related tasks which are awaiting integration. So the next step for us to try in improving the process will be to divide this column on our board and to observe the effect of being able to accurately track which state these items are - and to make explicit the policies of how things should move between these substates. I hope to eventually blog about the progress we make and include a before & after of our boards and how they've improved (and therefore how our process has improved).
