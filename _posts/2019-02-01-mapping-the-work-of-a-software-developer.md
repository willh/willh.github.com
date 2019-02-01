---
layout: post
title: "Mapping the work of a Software Developer"
description: ""
category: 
tags: []
---
{% include JB/setup %}

developer career wardley map

reference Forrest Brazeal's post
  - https://forrestbrazeal.com/2019/01/16/cloud-irregular-the-creeping-it-apocalypse/
  - great post about changing roles in a changing IT landscape
  - what proportion of average IT sysadmin work now involves plugging in servers vs keeping an eye on cloudwatch alarms?
  - move of previously custom work to managing of products to service abstraction removing all work entirely
    - e.g. installing DB system with custom server, to installing DB product bundle on VM, to RDS or serverless DB
  - what does this mean for people with skills in managing hardware racks and installing OS patches?
  - same as it does for developers who write POJOs to implement a WSDL and configure jars in a servlet container
  - you can for generate interface classes, you can use embedded-servlet, or a PaaS to run the apps

move up value chain
  - so you'll constantly be at risk of having your work commoditised in increasing amounts
  - to stay ahead you need to move up the value chain
  - how to understand which parts are being commoditised, or might already be outside your org
  - how to understand what areas are useful to be learning or pushing yourself towards to stay relevant and valuable
  - try and break this down using wardley map to illustrate chain of valuable activities and tech evolution

map activities of a developer
  >> high level generic map
  - solve user problem, meet a need, so they keep you employed [discounting perverse incentive] or engage your business
  - all other activities are subservient to this fundamental purpose
  - part of meeting user's need is computer system or application
  - breaking down application into components, understanding business domain and tech landscape
  - implementing work which is needed for custom parts - new dev
  - implementing work which is needed for for product parts - configuration and integration 
  - implementing work which is needed for integrating commodity parts - orchestration, selection
  - identify work we do which we have to do, and work we do which we want to do
  - value chain: new features, new products
    - breaking problem into components
    - developing the system
      - writing new code for custom parts
        - OSS libraries and frameworks
        - domain specific code
      - writing glue code for integrating products
        - defining interfaces
        - writing clients for standard interfaces
        - scheduling, transporting data
      - managing use of commodity parts
        - configuration of services
        - orchestration of commodity parts
    - understanding business domain
      - understanding business vertical & customer context
    - evaluating products
      - understanding products and services available

undifferentiated heavy lifting being reduced
  >> examples of map for sentiment analysis before AWS Comprehend and after
  - parts we have to do but which are low value are often more commoditisable
    - people build generic service from other generic services and solve generic problems

glue code being reduced to configuration
  - custom effort which exists lower down between commodity/product parts will be eaten by platforms
      - AWS, Azure etc will eat these parts, especially product integration/configuration/management
  - innovate, leverage, commoditise being done by platform providers not just on products to managed services

dependency on deconstruction of problem into solved problems and unsolved problems
  - lots of value in having involvement in breaking down problem into one of composition

increased dependency on composition of solved parts
  - with increased commoditisation, proportionally more work will be in integration and building on top

business domain knowledge still remains
  - translating someone's problems into a definition we can agree on and deciding which parts to solve is very hard
  - parts that are unlikely to go away are tied closest to the problem domain
  - parts that are unique to your problem are least appetising for other people to try and commoditise
    - unless they are a direct competitor in your exact target market
  - overly generic systems and no-code works only for parts of the problem in the generic area
    - writing code isn't going away, but writing code to turn XML into JSON certainly would

if you get it wrong, someone else will figure out how to compose it better and replace your custom work
  - reassess where the parts you've built really are on evolution scale
    - if you are building custom something which is widely productised/service based, you are generating waste
    - and you are also being less competitive; other people can solve the problem faster

blockers, accelerators such as FUD, resistance to change, NIH, accelerators are demands from business, ease of tools
  - for the parts that you do see as potentially custom, identify are they custom *here* or custom everywhere?
  - the parts which are your business' differentiator will probably be truly genesis/custom
  - the other parts are maybe not really
  - but if those parts are going to change what kind of barriers would there be to that change or adoption?
    - not everyone wants to constantly rebuild all their currently running systems
    - but also lots of inertia, blockers, decelerators
      - FID, NIH, etc
  - focus on how demands from business and efficiency vs competitors are likely to remain as accelerators
  - also use of new tools and platforms are able to accelerate previously difficult adoption

beware of optimising for local maxima
  - what are the bottlenecks on getting value to the customer
  - if you improve something that's not really the bottleneck it's not an improvement
  - doing faster something that can be avoided entirely is still waste
  - sometimes the wasteful things are really technically _interesting_ 
    - (e.g. creating your own FaaS platform with Firecracker)

abusing inertia and FUD to stay in comfort zone & lock in customer will backfire
  - eventually they'll want to move on and they'll not think you have skills or aptitude
  - Jevons 'paradox applies, if you solve their problems faster, end projects sooner, they'll have more budget to spend on more work with you and all the more reason to feel confident in doing so when they see results

for your career as a developer what does this mean
  - you're going to be learning another set of new frameworks every few years
  - custom development won't go away, but for non-unique domain problems will definitely diminish
  - the further away from customer problems the more likely your work to be automated or replaced
  - so unless you are the people automating this or replacing this you might be in trouble
  - stay further up the value chain, don't shy away from business people or architecture decisions
  - the act of turning an architecture diagram into code will probably become more common
  - understanding why or why not to implement something is not easily inferred by a machine

hot take
  - getting into containers right now is skating to where the puck is
  - getting into serverless right now is skating to where the puck is going... to some extent
  - depends on your desired customer and how far long tech adoption curve they are
  - there's still money to be made in managing VMs in customers slower to move
  - but more people have those skills, and those customers will eventually want to move
  - embrace the adoption of abstractions, though know a bit about where they leak to make good evaluations
  - treat NIH/sunk cost with extreme skepticism
  - keep up with industry trends and be wary of getting into a rut and rejecting change
