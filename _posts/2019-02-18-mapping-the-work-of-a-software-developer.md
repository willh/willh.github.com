---
layout: post
title: "Mapping the work of a Software Developer"
description: "The technology landscape constantly evolves and yesterday's good practice becomes today's legacy approach. Using Wardley Maps we break up the activities involved in software development and identify patterns in changing practices. Using the maps, you can make decisions about where to grow your career or in which areas to focus learning in-demand skills."
category: 
tags: ["wardley maps"]
---
{% include JB/setup %}

developer career wardley map
  - Tweet length-summary of purpose and goal
  >> headline image of Wardley Map showing some dev skill stuff

## Why

Some of these thoughts about how to use [Wardley Maps](https://www.slideshare.net/swardley/an-introduction-to-wardley-maps) have been kicking around in my head for some time, crystallising after reading [Forrest Brazeal's great post](https://forrestbrazeal.com/2019/01/16/cloud-irregular-the-creeping-it-apocalypse/) about the changing roles in an ever evolving IT landscape.

Evolution of technology and practices continues but what of the people who make their living building with, advising about, maintaining and operating that technology? What proportion, for example, of average IT sysadmin work now involves plugging in servers vs keeping an eye on AWS Cloudwatch alarms and Grafana dashboards?

This evolution means a general move of previously custom work to managing of products to service abstraction removing almost all work entirely. Building on the previous example, we can see over the years that this has resulted in the role considered to be low-leve detailed technical work has radically changed in nature, e.g. installing a database system by purchasing and installing a custom server and configuring a database engine on top, to installing a DB product bundle on a VM, to using a tool to virtually provision a whole load-balanced database cluster and backup (such as Amazon RDS) or as far as setting up permissions for an application to communicate with a 'serverless DB' (such as Azure Cosmos DB) with no actual server instances or database engine patches or anything of the sort.

What does this mean for people with skills in managing hardware racks and installing OS patches? Well, if you work with any people in 'devops' at the moment, just ask them - quite a lot of people with AWS and Azure infrastructure automation skills have backgrounds in systems administration and IT operations and they gradually or abruptly learned new skills and gained experience in new practices reflecting the 'new normal' of the ever-raising level of abstraction.

### Nobody is safe

This isn't something limited to IT operations. It may be a little slower in areas but it will generally be the same for software developers who write POJOs to implement a WSDL and configure WAR files in a servlet container, waking up one day to find that they can now generate POJO interface classes and use embedded servlets in their jars so they're spending more time externalising global state instead so a cloud-friendly caching product can be used and their apps can become stateless. The next week they come in to find they're now using a PaaS system that simply runs a jar with little additional intervention, adding a caching provider via configuration.

Each one of these changes can be either gradual or abrupt but in order for you to be a highly valued software engineer in the marketplace, you will want to understand the landscape of technology to see how your skills and practices might change over time rather than slipping behind.

### Staying valuable

If you ignore the evolution trends in tech then generally speaking you'll be at risk of having your work cannibalised by others offering products to do the things you do by hand, or services that appear to do away with the thing you're an expert in altogether. Practices and tecnologies are commoditised in increasing amounts, so to stay ahead you need to move up the value chain, like the sysadmins who picked up the tools of virtualisation automation.

To do this, it will help you to understand which parts of the technology landscape are being commoditised, or might already be outside your org that you haven't yet had a chance to see.

It will also help you to understand what areas are useful to be learning or pushing yourself towards to stay relevant and valuable so you can try and get training, gain knowledge and practice, which will improve your worth to the organisation.

To try and make sense of these things systematically, I will try and break this down using examples on a Wardley Map to illustrate a chain of valuable activities and where they might lie on an axis of technology evolution, so that we can discuss future changes, blockers and accelerators.


### What's a Wardley Map?

For those of you who are unfamiliar with Wardley Maps, I have a recording of a [talk I gave at BelTech 2018 on Wardley Maps](https://www.youtube.com/watch?v=5qglzdCHesw) and also I wrote a blog post last year on [using Wardley Maps to understand AWS re:Invent](https://willhamill.com/2018/01/21/making-sense-of-aws-reinvent) which gives an introduction into what maps are and how to create one.


## Mapping the activities of a developer

  >> high level generic map
  - solve user problem, meet a need, so they keep you employed [discounting perverse incentive] or engage your business
  - all other activities are subservient to this fundamental purpose
  - part of meeting user's need is computer system or application
  - breaking down application into components, understanding business domain and tech landscape
  - implementing work which is needed for custom parts - new dev
  - implementing work which is needed for for product parts - configuration and integration 
  - implementing work which is needed for integrating commodity parts - orchestration, selection
  - identify work we do which we have to do, and work we do which we want to do
  - for purposes of making things simpler, we will look at _development_ activities and not _operational_ activities
  - testing activities are similar (writing test code, deciding which parts to test, which parts to use libraries, etc) so planning to leave these out of the scope of the current exercise
  - by all means, do the same thing for operational or test-oriented activities and responsibilities
  - you might find similar trends, with operational work experiencing heavy pressure on productising/commoditising in particular
  
### The Value Chain
- value chain: new features, new products
    - breaking problem into components
      - understanding business domain
        - understanding business vertical & customer context
      - build vs buy decisions
        - understanding products and services available
    - developing the system
      - writing new code for custom parts
        - app frameworks
          - OSS libraries
        - domain specific code
          - OSS libraries
            - package manager
            - discoverability
            - dependency checking
          - custom libraries
            - as above
      - writing glue code for integrating products
        - defining interfaces
          - problem-specific constraints
          - open standards
        - writing clients for standard interfaces
          - open standards
          - client library
            - OSS libraries
        - scheduling, transforming data
          - data format transformation
          - scheduled task management
      - managing use of commodity parts
        - configuration of services
          - configuration management
        - orchestration of commodity parts
          - ???
    - execute code
      - compute platform
      >> intentionally abbreviated chain here, not focusing on operation as much as development
    - testing
      - test scenarios
      - test runner
      >> intentionally abbreviated chain here, not focusing on testing which is similar to development

## The Map

- Overlaying the chain of activities and dependencies onto the map, and moving the components into the areas that I think best suit the level of innovation versus commodity effort, we can then create the basic map.

- Describe each part and why it lives where it lives on the evolution axis

## Using the Map

- Getting this far means we can start to have debates about the placement of components, what it means that they are in that position and what it would mean if they moved. Generally speaking, most things move to the right as over time they become commoditised, so how might that impact the practices and skills of our software developer?

### Undifferentiated heavy lifting being reduced
  >> examples of map for sentiment analysis before AWS Comprehend and after
  - parts we have to do but which are low value are often more commoditisable
    - people build generic service from other generic services and solve generic problems

### Glue code being reduced to configuration
  - Custom effort which exists lower down between commodity/product parts will be eaten by platforms
      - AWS, Azure etc will eat these parts, especially product integration/configuration/management
  - innovate, leverage, commoditise being done by platform providers not just on products to managed services

### Similar patterns can be observed with the code execution sub-chain
  - code execution depends on packaging, state management, scaling, operational metrics etc etc
  - all of these things are becoming more commoditised at varying levels
  - k8s managed services taking a lot of infra with it, though creates its own additional work
  - AWS Lambda takes a great deal more things off to the right
  - can use same patterns for identifying and reacting to this if you are in the operations space
  - move up the chain towards observability of existing platforms, more in configuration and integration

### Deconstruction of problem into solved problems and unsolved problems
  - There is lots of value in having involvement in breaking down problem into one of composition. Making sense of the things needed to meet the user need will make parts of the decision-making easier so you can take advantage of existing services and commodities to avoid wasting time and money.
  - Understanding which parts exist already and what would make them feasible or infeasible to adopt is very useful. Part of this is understanding you gain from experience of building systems, and part of it you get from doing analysis and investigation into what are the new 'hot' languages or practices or tools; into actively considering alternatives to the solutions you already know. Keeping up to date with the tech landscape is more than a full time job.
  - In fact being able to use Wardley Maps to help directly identify the types of components needed to meet a user need and to then be able to show which parts are custom vs commodity can help with the business cases for future work.

### Increased dependency on composition of solved parts
  - I expect this will shift in weight from writing a custom made application and pulling two libraries into it and co-ordinating the calls and marshalling data into the different formats, to something more like configuring the plugin for one product to make it export data to the other product's API.
  - With increased commoditisation, proportionally more work will be in integration and building on top. However changing from owning the execution context of that integration within your application to having to deal with it being externalised means an increase in demand for skills in things like undertanding integration patterns, in building tolerant clients with retry logic, in creating resilient server endpoints which produce data streams from multiple regions, and figuring out the correct way to determine if the integrations have failed and how to monitor/alert on that.

### No-code, Low-code, Form Builders
  - increased productisation of custom work which is very generic
  - 'form builder' might eat up some of the work you were hand coding for 'capture 5 fields to DB' and 'upload a file'
  - not likely to have a drop down menu to select 'combine blah blah financial factors with compound interest'
  - things that promise business people to configure and not need 'coders'
  - misses the valuable cases, the domain specific cases
  - also means that building one of these for your business needs to be super highly justifiable
    - especially when balancing cost of making a product that's sufficiently generic to be useful against making a thing that has so many low-reused functions
    - can likewise be easier to decompose into reuse/service based parts and custom work
  - so if you've got skills in higher up areas then not much to worry about when basic things commoditised

### Business domain knowledge still remains mostly on the left
  - Translating someone's problems into a definition we can agree on that can be expressed either with code or with composition of components, and deciding which parts to solve ourselves is actually very hard.
  - The parts that are unique to your problem domain are least appetising for other people to try and commoditise, unless they are a direct competitor in your exact target market. Even so, specificity to your approach or customer is going to stymie any attempt at external parties competing on this. If you're working out what kind of documentation requirements to tell a user to supply in support of their first passport application, based on the current governmental policy and the current state of the user's application and the circumstances in which they are applying, this is not likely to be something that is suitable for others to attempt to commoditise. Amazon Elastic Intelligent Passport Documentation Service seems pretty unlikely.
  - If however you're spending a large amount of time writing logic (and unit tests, right?) for a component in an insurance quoting system that calculates compound interest on a recurring missed premium payment then you're in 'there's a library on npm for that' territory.
  - Every so often we hear the threats of the 'low code' or 'no code' platforms, offering business users "configurability" without developers. These systems work for overly generic use cases, for the 'form builder' type of applications and going off the beaten track tends to result in pain and suffering. Some businesses, especially as these things improve in complexity and configurability, will take advantage of these but the more complex they get then the closer they become to simply a DSL over another programming language. A wise man once said 'DSL means write code in one language and read stack traces in another'. Writing code isn't going to go away, but writing code to turn an XML object into a JSON object and other equally low-customer-value type stuff certainly should.

if you get it wrong, someone else will figure out how to compose it better and replace your custom work
  - reassess where the parts you've built really are on evolution scale
    - if you are building custom something which is widely productised/service based, you are generating waste
    - and you are also being less competitive; other people can solve the problem faster

### Moving up the chain

  - ILC happens and then similar patterns repeat themselves
  - e.g. writing code and dependency management
    - moves up chain and some generic code gone
    - due to changes in execution platform, rebuiding of similar existing components further up
    - e.g. sharing code between lambdas, discovering previously created lambda apps
    - as these start as custom work on top of new lambda platform they too get commoditised as ecosystem tooling catches up
    - lambda layers, Serverless Application Repository same as maven/Gitlab/npm
    - through composability more things become possible with generic components
    - previously unlikely for all permutations of components X,Y,Z to be created as a product
    - but now all three sub-components are available and you can build that 'product' yourself
    - dependency checking easier with OWASP DC, npm audit, Github built-in
    - for lambda functions you can do some of this as part of the build process
    - might Serverless Application Repository be extended soon to do the same to SAR apps?
  - when adopting new things, expect some additional glue necessary while rest of landscape adjusts to new baseline

### Adapting to change
  - identify blockers & accelerators such as FUD, resistance to change, NIH
  - accelerators are demands from business, improved ease of use of tools, more demand due to something popular built on top
  - for the parts that you do see as potentially custom, identify are they custom *here* or custom everywhere?
  - map out parts that are custom in the industry, not in your org (lead the target, shoot where it is now)
  - the parts which are your business' differentiator will probably be truly genesis/custom
  - the other parts are maybe not really custom
    - decompose the problem to identify which parts really really are custom
    - [example of postcode lookup from CO recently]
  - if those parts are going to change what kind of barriers would there be to that change or adoption?
    - not everyone wants to constantly rebuild all their currently running systems
    - but also lots of inertia, blockers, decelerators
      - FUD, NIH, etc
  - focus on how demands from business and efficiency vs competitors are likely to remain as accelerators
  - also use of new tools and platforms are able to accelerate previously difficult adoption

### Beware of optimising for local maxima
  - what are the bottlenecks on getting value to the customer
  - if you improve something that's not really the bottleneck it's not an improvement
  - doing faster something that can be avoided entirely is still waste
  - sometimes the wasteful things are really technically _interesting_ 
    - (e.g. creating your own FaaS platform with Firecracker)

### Don't take the easy way out
  - it's possible to keep on peddling the same stuff without learning new skills or practices
  - you can abuse the customer/your employer's inertia, and spread FUD to stay in your comfort zone
  - this will implicitly box the customer in to things you can already do
  - this will backfire
  - eventually they'll want to move on and they'll not think you have skills or aptitude
  - Jevons' paradox applies, if you solve their problems faster, end projects sooner, they'll have more budget to spend on more work with you and all the more reason to feel confident in doing so when they see results

### For your career as a developer what does this mean
  - you're going to be learning another set of new frameworks every few years
  - custom development won't go away, but for non-unique domain problems will definitely diminish
  - the further away from customer problems the more likely your work to be automated or replaced
  - so unless you are the people automating this or replacing this you might be in trouble
  - stay further up the value chain, don't shy away from business people or architecture decisions
  - the act of turning an architecture diagram into code will probably become more common
  - understanding why or why not to implement something is not easily inferred by a machine

### Also
  - when enjoying productivity with abstractions you should probably still understand one layer below
  - not just for finding the best time to use the abstractions, or to deal with leaks (they will leak)
  - but also to have an ear to the ground for the next shift underneath that might affect your area
  - if you're sitting pretty on containers and k8s for the last three years as a market leader but haven't heard of serverless then you're missing the next shift
  - find your own niche, with a bias towards up and to the left if you want newer problems and innovative areas
  - working dragging people to the right is where a lot of effort will remain; understand what you want

#### Caveats
  - Someone's gotta turn undifferentiated heavy lifting into services, so someone is doing custom/genesis work in turning product work into commodity and setting up automatic region-distributed multi-tenancy and all that.
  - Working on difficult engineering and ops problems _at_ Microsoft/Azure/etc no doubt is highly specialised work, but their users are not retail insurance clients; their users are the developers, IT operations and engineering directors from those retail insurance providers who are choosing to take a particular approach to technology and want to use the platform to build fastert's innovative for what top level user needs it is solving and how you stay ahead of the creeping commoditisation
  - If you're working on a product used in a container orchestration system which builds on or alongside k8s, and your core business is that you intend to release it as a product/service, and you know how to avoid being eaten by a provider or being replaced with a feature bump, all power to you.
  - However, if you're working setting up your own k8s based container orchestration system for your organisation which is in, say, retail insurance, then the odds are fairly good that you're doing work which has already been replaced by platform providers.

## Hot take 🔥
  - getting into containers right now is skating to where the puck is
  - getting into serverless right now is skating to where the puck is going... to some extent
  - depends on your desired customer and how far long tech adoption curve they are
  - there's still money to be made in managing VMs in customers slower to move
  - but more people have those skills, and those customers will eventually want to move
  - embrace the adoption of abstractions, though know a bit about where they leak to make good evaluations
  - treat NIH/sunk cost with extreme skepticism
  - keep up with industry trends and be wary of getting into a rut and rejecting change
