---
layout: post
title: "Starting a New Project as a Technical Architect"
description: "Getting the lay of the land - who to talk to and what to ask when you start into a project that is currently underway"
category: 
tags: []
---
{% include JB/setup %}

I've just started work on a new project, one that is already well underway (and has been for over a year). Probably half the projects I've worked upon in [my career at Kainos](http://www.kainos.com/careers) I've started when they are already in motion, so getting up to speed and finding out how things work is really important. In this new project I'll be reprising the role of a technical architect, so I need to understand how my work is going to fit in and around the other people who are already there, and get a bit of context on what is needed to help me think about how I make an impact.

A lot of the questions I list here are ostensibly answered in detail on wikis and network shares and so on, but as documents are static and idealised but the practice is live and real I wanted to hear these things straight from the horse's mouth - and it will hopefully help me get to know my team and show people I want to listen to them too. Some of these people will be the same person on smaller projects, and on larger projects there may be multiple of them. The important thing is getting these answers to get a clear picture, so ask around!

###Find out who the users are
Start here, with the people who need and who will benefit from the system. Ideally on the project there will be some clearly documented personas, describing the type of person they are and their needs from the system, along with some detail on the kind of attitudes they have about it. The rest of your work should in some way be able to be tied towards meeting the users' needs, so find out who they are and what they want. If there aren't any public personas printed up on a wall, ask if they can be so that others can benefit from the shared context too.

###The product owner
Get a demo of what has currently been created from a product owner, along with their views on what the system is for and what decisions are being made based on the user needs. Find out where features come from - results of user research, existing backlog, iteration suggestions, new ideas etc - and how these features make their way to the teams. If your teams have a dedicated user researcher or UX expert then talk to them too about how often user research happens, where the results go and how they interact with the team.

###The tech lead
The project I'm joining has multiple teams and each team has a tech lead, responsible for working with the team on low level designs and implementation. I'll be talking to more than one of them, but for starters I asked one of the tech leads to sketch up the application architecture for me (more on that later) and to describe how the technologies used fit into the system. I also got some pointers on checking out the source code and running the application, which will help me get deeper into the codebase soon. I asked the tech lead where their current pain points are in terms of the design, the techs, the choices made and how the teams work on them. Getting an idea as to where any tech debt lies or low hanging fruit for improvement is a good opportunity. I also asked the tech lead to summarise the path the code takes from being written by developers to as close as possible to production - ask what the merging, integration, build and release process looks like.

###The delivery manager
Your project manager, delivery manager, or whoever - the person who runs the administrative side of the project, the one who deals with the commercials - is the person from whom to get an idea of the business constraints and pressures. Get a context of how the project fits in to the organisation's plans and why it is being run. Get an idea as to their view of what your role is and where boundaries are.

###The ops lead
What does production look like? How does code get there? Getting an idea of the infrastructure architecture and the systems that support development is best done from someone who has ops responsibilities. Find out which parts of the documented processes are real, and which are aspirational. Which parts are automated and which parts are [for now] manual. How is configuration managed, how is monitoring of applications done, how is security and the likes assured and to what extent do the development teams have an involvement in that?

###The solution architect
Ideally, start with something like the [C4 documentation](https://leanpub.com/software-architecture-for-developers/read#c4) as per [Simon Brown](https://twitter.com/simonbrown) to get views of the system with varying levels of abstraction. Context, container, component and class - these should give you a good idea of the intention of the system, the interaction points and the structures within it. The solution architect is also the person to talk to about the technical constraints (e.g. "Why did we choose memcached instead of Redis?") and the vision of the future of the system both in terms of what it needs to look like when it first goes live, and how that will change with the needs of the programme of work. Find out the non-functional requirements for the system and what testing is being done to help meet them. The solution architect should also be able to describe or point you towards the design principles for the project that guide people at all levels in the design decisions they make and how the implement the technologies used.

###The developers
Ideally, talk to more than one, as each person may have a different perspective based on the specific type of work they've taken on and the skills that they have and the others they interact with. Find out how a feature gets developed from user story or requirement to actual code, and what their responsibilities are until they finish the work on that feature (and what 'finished' means to them). Find out what tools they use to fix defects and create features and what the code review, merge and CI process is like - because you should be doing some of that too. Find out what bothers them or what wastes their time or what they'd love to have time to fix. Take notes!

###The tester
If the project has dedicated testers, talk to one of them to understand what the relationship is with the developers, what their own responsibilities are and how they perceive the project. Identify handovers to see if there are silos or hidden phased work, and where testing efforts are focused in the project (particularly manual vs automation, high level UI based or lower level code based). Find out what their interactions with the product owner or business analysts are, and what their view of quality is across the project. Ask what involvement they've had in non-functional testing such as accessibility, performance testing, usability and the likes.

###The scrum master
Find out how work flows through the system. Look for a board that shows the work in progress - are there WIP limits? Are policies for work changing states made explicit? Starting with the (ideally explicit and publicly viewable) definition of ready and definition of done for development work, talk to the scrum master to find out where features and defects come from and what is necessary to see them through. Ask about the team dynamics, how people work with each other and where the handoffs are and what pain points, common blockers and bottlenecks exist.

###Identify the Brents
If you've [read The Phoenix Project](http://willhamill.com/2014/01/15/the-phoenix-project), no doubt the description of Brent struck a chord with you. You probably have worked on a project with a Brent before; maybe you've even been the Brent. Find out who the Brents are on the project for various types of work and what kind of bottlenecks are caused by these people being overloaded - this will give you a good idea as to what kind of capabilities are not as well shared across the team(s) and should also indicate that you should try and protect these people from interruptions and ensure they are able to share knowledge with others. 

###Identify the working culture
Ask people about the smaller or more subtle things, like the dress code, the working hours, the social activities and the camaraderie within the teams. Find out if there are regular meetings that it might benefit you to be in (and avoid the ones that will not be beneficial)

###Get involved
As a technical architect, what exactly you do will depend on the project - the size of the project, the roles of your colleagues and what needs to be done will influence this. The odds are good however that you're going to be involved both in higher level design and architectural discussions but will also need a reasonable lower level understanding of how the implementation actually hangs together. The technical architect in Kainos is probably the person who stretches the most in vertical involvement, changing level of abstraction depending on where they are needed and bridging the gap between higher level business/enterprise issues and the coal face of writing and testing the code. To that end - get the code checked out, get your IDE set up and get the application built. Don't be afraid to pair with someone on a defect or a smaller story to get your feet wet and find out what the reality is beyond the architecture diagrams and the formal definition of done.


