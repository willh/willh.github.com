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

### Plus ça change

- What's changing? New frameworks, new libraries, new languages
- We're still writing code, aren't we?
- True but how has it changed?
- Moving up the stack - more splitting requests across two DBs based on staleness and less hand rolled linked lists
- Useful to look at which parts have changed and why, identify future changes, do some intentional career planning

## Why map?

Some of these thoughts about how to use [Wardley Maps](https://www.slideshare.net/swardley/an-introduction-to-wardley-maps) have been kicking around in my head for some time, crystallising after reading [Forrest Brazeal's post](https://forrestbrazeal.com/2019/01/16/cloud-irregular-the-creeping-it-apocalypse/) about the changing roles in an ever evolving IT landscape.

Evolution of technology and practices continues but what of the people who make their living building with, advising about, maintaining and operating that technology? What proportion, for example, of average IT sysadmin work now involves plugging in servers vs keeping an eye on AWS Cloudwatch alarms and Grafana dashboards?

This evolution means a general move of previously custom work to managing of products to service abstraction removing almost all work entirely. Building on the previous example, we can see over the years that this has resulted in the role considered to be low-level detailed technical work has radically changed in nature, e.g. installing a database system by purchasing and installing a custom server and configuring a database engine on top, to installing a DB product bundle on a VM, to using a tool to virtually provision a whole load-balanced database cluster and backup (such as Amazon RDS) or as far as setting up permissions for an application to communicate with a 'serverless DB' (such as Azure Cosmos DB) with no actual server instances or database engine patches or anything of the sort.

What does this mean for people with skills in managing hardware racks and installing OS patches? Well, if you work with any people in 'devops' at the moment, just ask them - quite a lot of people with AWS and Azure infrastructure automation skills have backgrounds in systems administration and IT operations and they gradually or abruptly learned new skills and gained experience in new practices reflecting the 'new normal' of the ever-raising level of abstraction.

### Nobody is safe

This isn't something limited to IT operations. It may be a little slower in areas but it will generally be the same for software developers who write POJOs to implement a WSDL and configure WAR files in a servlet container, waking up one day to find that they can now generate POJO interface classes and use embedded servlets in their jars so they're spending more time externalising global state instead so a cloud-friendly caching product can be used and their apps can become stateless. The next week they come in to find they're now using a PaaS system that simply runs a jar with little additional intervention, adding a caching provider via configuration.

Each one of these changes can be either gradual or abrupt but in order for you to be a highly valued software engineer in the marketplace, you will want to understand the landscape of technology to see how your skills and practices might change over time rather than slipping behind.

### Staying valuable

If you ignore the evolution trends in tech then generally speaking you'll be at risk of having your work cannibalised by others offering products to do the things you do by hand, or services that appear to do away with the thing you're an expert in altogether. Practices and technologies are commoditised in increasing amounts, so to stay ahead you need to move up the value chain, like the sysadmins who picked up the tools of virtualisation automation.

To do this, it will help you to understand which parts of the technology landscape are being commoditised, or might already be outside your org that you haven't yet had a chance to see.

It will also help you to understand what areas are useful to be learning or pushing yourself towards to stay relevant and valuable so you can try and get training, gain knowledge and practice, which will improve your worth to the organisation.

To try and make sense of these things systematically, I will try and break this down using examples on a Wardley Map to illustrate a chain of valuable activities and where they might lie on an axis of technology evolution, so that we can discuss future changes, blockers and accelerators.


### What's a Wardley Map?

For those of you who are unfamiliar with Wardley Maps, I have a recording of a [talk I gave at BelTech 2018 on Wardley Maps](https://www.youtube.com/watch?v=5qglzdCHesw) and also I wrote a blog post last year on [using Wardley Maps to understand AWS re:Invent](https://willhamill.com/2018/01/21/making-sense-of-aws-reinvent) which gives an introduction into what maps are and how to create one.


## Mapping the activities of a developer

  >> high level generic map
  The starting point is that we're doing what we do to solve a problem someone has: to meet a need that presumably can be fulfilled via computer systems.
  - All other activities are subservient to this fundamental purpose. The customer/employer/end user wants to use what you'll build to solve a problem they have. That's why you're employed!
  - In our domain, we're assuming that part of meeting that user's need is implementing some computer system, service or application.
  - To develop this system and meet their needs, we need to break down what is needed into components, understanding the business domain and technology landscape.
  - Broadly I've divided this up into three main sections: new work which is needed for custom parts, work which is needed for for product parts (configuration and integration), and work which is needed for integrating commodity parts (orchestration and selection). 
  - For the purposes of making things simpler, in this discussion I will look at _development_ activities and not _operational_ activities. Testing activities are similar enough to development here (writing test code, deciding which parts to test, which parts to use libraries, etc) so I'm planning to leave these out of the scope of this discussion too.
  - By all means, do the same thing for operational or test-oriented activities and explore those areas as well. You will find similar trends, with operational work experiencing heavy pressure on productising/commoditising in particular.
  
### The Value Chain
Let's begin by breaking down the chain of components and sub-components involved in this work to illustrate the activities and see how they change as technology changes.
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

- Describe significant parts and why it lives where it lives on the evolution axis

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
  - examples of glue code automatically generated e.g. AWS Glue

### The boring parts of building will be consumed
  - even the process of updating default configurations, opening a pull request, running unit tests, etc will be automated
  - all of these parts of the process are standardised at most companies and for some activities require little custom work
  - behold, this interaction recently on GitHub where a bot updated a dependency, another bot built it and another merged it
    - https://twitter.com/gabro27/status/1173547934132178944
  - this worked because it was generic, automatable, low-value work

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
  - With increased commoditisation, proportionally more work will be in integration and building on top. However changing from owning the execution context of that integration within your application to having to deal with it being externalised means an increase in demand for skills in things like undertanding integration patterns, in building tolerant clients, in creating resilient server endpoints which produce data streams from multiple regions, and figuring out the correct way to determine if the integrations have failed and how to monitor/alert on that.

### Business domain knowledge still remains mostly on the left
  - Translating someone's problems into a definition we can agree on that can be expressed either with code or with composition of components, and deciding which parts to solve ourselves is actually very hard.
  - The parts that are unique to your problem domain are least appetising for other people to try and commoditise, unless they are a direct competitor in your exact target market. Even so, specificity to your approach or customer is going to stymie any attempt at external parties competing on this. If you're working out what kind of documentation requirements to tell a user to supply in support of their first passport application, based on the current governmental policy and the current state of the user's application and the circumstances in which they are applying, this is not likely to be something that is suitable for others to attempt to commoditise. Amazon Elastic Intelligent Passport Documentation Service seems pretty unlikely.
  - If however you're spending a large amount of time writing logic (and unit tests, right?) for a component in an insurance quoting system that calculates compound interest on a recurring missed premium payment then you're in 'there's a library on npm for that' territory.
  - Every so often we hear the threats of the 'low code' or 'no code' platforms, offering business users "configurability" without developers. These systems work for overly generic use cases, for the 'form builder' type of applications and going off the beaten track tends to result in pain and suffering. Some businesses, especially as these things improve in complexity and configurability, will take advantage of these but the more complex they get then the closer they become to simply a DSL over another programming language. A wise man once said 'DSL means write code in one language and read stack traces in another'. Writing code isn't going to go away, but writing code to turn an XML object into a JSON object and other equally low-customer-value type stuff certainly should.

if you get it wrong, someone else will figure out how to compose it better and replace your custom work
  - reassess where the parts you've built really are on evolution scale
    - if you are building custom something which is widely productised/service based, you are generating waste
    - and you are also being less competitive; other people can solve the problem faster

#### No-code, Low-code, Form Builders
  - increased productisation of custom work which is very generic
  - 'form builder' might eat up some of the work you were hand coding for 'capture 5 fields to DB' and 'upload a file'
  - not likely to have a drop down menu to select 'combine blah blah financial factors with compound interest'
  - We've seen and heard of tools that promise business people to configure and not need 'coders', yet inevitably the domain specific language they use is either too generic to be valuable or so powerful that it is code (just with crappy tooling) and requires people who understand code to write and verify it. The very generic parts miss the valuable cases, the domain specific cases you need to write yourself anyway.
  - Given there are lots of things out there that'll take the very generic case and make it easier, also means that building one of these for your business needs to be super highly justifiable. The route to justifying this has to be by making it domain-specific, especially when balancing the cost of making a product that's sufficiently generic to be reusable against making a thing that has so many low-reused functions
    - can likewise be easier to decompose into reuse/service based parts and custom work
  - Generally speaking the trend for new tools and frameworks to remove the low level glue and replace it with convention/configuration isn't going to be new to most developers, and if you've got skills in higher up areas then there's not much to worry about when these basic things become yet more commoditised. Your job is to build on top.

### Moving up the chain
  - ILC (Innovate, Leverage, Commoditise) happens and then similar patterns repeat themselves
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
    - Github are doing it now for default-layout NodeJS apps - if you build a thing to do it, you're at risk
  - when adopting new things, expect some additional glue necessary while rest of landscape adjusts to new baseline

### Evolution of practices
  As practices formalise around new sets of technologies, emerging practices become 'best practices' which become uncontested standard procedures. As these practices evolve, we build inertia as the practices choke out deviation, and new practices which evolve from higher order systems build on top of these now-commoditised abstractions are treated as upstarts and usurpers. Who has a hardware testing plan when using IaaS in the cloud? Who will have a capacity plan for serverless functions when using AWS Lambda? The value changes based on how the practices change - so with serverless functions for example the focus on capacity planning shifts to surge testing and limit checking, searching for edge cases of cold starts and scaling cliffs.
  For example, the evolution of DevOps around cloud-native development and operation of distributed systems has turned from a cutting edge conference keynote to a well-accepted industry best practice peddled by product vendors and consultants alike. Everyone who's anyone is doing DevOps now! But what happens when new practices emerge by groups of people building on top of new abstractions that DevOps has made possible? Well, take a look at what happened ITIL. It's not dead, just either used in organisations with larger estates and lower change velocity that benefit from a more predictable service management approach, or used across organisations with only one tool in their toolbox that are still struggling against DevOps and other emerging practices and wondering why they can't iterate as fast as their competitors.
  What this means is that you should expect DevOps to follow the same pattern of other practices like ITIL and become the commodity approach to developing and operating cloud-native systems, but also that it will likewise suffer from its success and be resistant to change and to disruption by new practices that don't fit into its view of software development.

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
  - this will look sustainable for a while as the late majority take longer to adapt
  - this will backfire: eventually they'll want to move on and they'll not think you have skills or aptitude
  - Jevons' paradox applies, if you solve their problems faster, end projects sooner, they'll have more budget to spend on more work with you and all the more reason to feel confident in doing so when they see results

### For your career as a software engineer what does this mean
  - As you've probably picked up - you're going to be learning another set of new frameworks every few years, with increasing levels of abstraction. Custom development won't go away, but for non-unique domain problems will definitely diminish as productised solutions become more easily integrated. The further away from the customer's specific problems you are, the more likely your work to be automated or replaced entirely. Unless you are the people automating it or replacing it you might be in trouble.
  
  As a software engineer, staying further up the value chain means don't shy away from business people or architecture decisions. The promised land of turning an architecture diagram into code will probably become closer to reality in more useful cases, but this will reflect the generic or lower value parts at first. Understanding why or why not to implement something is not as easily inferred by a machine - this is better understood by someone who understands the technical details but also the nature of the problem and the context and its constraints.

  While enjoying the productivity gains from new abstractions you should probably still understand one layer below: not just for finding the best time to use the abstractions, or to deal with leaks (they will leak), but also to have an ear to the ground for the next shift underneath that might affect your area. If you're sitting pretty on containers and k8s for the last three years as a market leader but haven't heard of serverless then you're missing the next shift. Find your own niche, with a bias towards up and to the left if you want newer problems and innovative areas. Working on enabling people to move to the right is where a lot of effort will remain, so understand what you want.

#### Caveats
  Someone's gotta turn undifferentiated heavy lifting into services: while it always happens as technology evolves, it doesn't evolve by itself. Someone is doing custom/genesis work in turning product work into commodity and setting up that check-box automatic region-distributed multi-tenancy and all that. The cloud computing resources we now take for granted only exist because different sets of people worked on making those abstractions and those generic solutions, so I don't mean to imply 'innovation' only happens on the far left of the map.

  Working on difficult engineering and ops problems _at_ Microsoft/Azure/etc no doubt is highly specialised work, but their users are not retail insurance clients; their users are the developers, IT operations and engineering directors from those retail insurance providers who are choosing to take a particular approach to technology and want to use the platform to build faster. _Their_ users are people who are building on top, and they go to great pains to understand their users and their needs. They aren't kidding themselves that the customer of their interesting scheduling framework are finance industry execs; their customers are the people who work to build something of relevance on top of it. Know who your users really are and whether you're meeting their needs by what you're building. 

  [part missing] it's innovative for what top level user needs it is solving and how you stay ahead of the creeping commoditisation
  
  If you're working on a product used in a container orchestration system which builds on or alongside k8s, and your core business is that you intend to release it as a product/service, and you know how to avoid being eaten by a provider or being replaced with a feature bump - or indeed if you intend to become just attractive enough to get acquired by a provider who wants to improve the value of their service by integrating what you do - then all power to you.

## Hot takes 🔥
  Getting into containers right now is skating to where the puck is. Getting into serverless right now is skating to where the puck is going... to some extent. This depends on your desired customer and how far along the adoption curve they are. There's still money to be made in managing VMs in customers slower to move but more people have those skills, and those customers will eventually want to move so you might have a lot of competition for the type of work that has a Best Before Date attached.

  There is less competition on the left side as skills have not yet diffused to commodity, so make yourself more valuable and get more career prospects by staying on the left side of mass-market. Far too far left and you might miss: investing in skills that don't make it to adoption; but roll the dice if you want or learn how to sense the landscape of the industry and make better bets than others!

  Generally, stay abreast of industry trends and be wary of getting into a rut and rejecting change. Treat 'not invented here' and the sunk cost fallacy with extreme skepticism so you know when you're suffering from inertia that can prevent you from moving left and up the value chain. Embrace the adoption of abstractions, ensuring you know a bit about where they leak so that you can make good evaluations of options.