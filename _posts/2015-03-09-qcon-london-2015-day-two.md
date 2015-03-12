---
layout: post
title: "QCon London 2015 Day Two"
description: "Conference sessions from the second day of QCon in 2015. Talks from John Wilkes, David Pollack, Jessie Frazelle, Colin Humphreys and Paula Kennedy, Peter Lawrey, Torben Hoffman"
category: 
tags: []
---
{% include JB/setup %}

Thursday was opened by the Google keynote on managing their own server containers and set the scene for a day of container technology presentations. After hitting plenty of microservices talks at [day one of qcon](http://willhamill.com/2015/03/04/qcon-london-2015-day-one/) I decided to really up my tech hipster cred by figuring out what the deal is with Docker, obviously so I can then have endless Twitter opinions about it.

- [Keynote: Cluster management at Google](#google_cluster)
- [Securing PaaS with Docker and Weave](#securing_paas)
- [Infrastructure and Go](#docker_go)
- [Docker vs PaaS](#docker_vs_paas)
- [Docker clustering: batteries included, but removable](#docker_clustering)
- [Responding rapidly when you have 100GB+ data sets in Java](#big_java)
- [Protocols: the glue for applications](#protocols)

<br />

####<a id="google_cluster"> </a>Keynote: Cluster management at Google
*by [John Wilkes](http://research.google.com/pubs/JohnWilkes.html)*

Google, a company of which many of you will have heard, has spent the last 15 years investing in creating the world's largest and fastest cloud infrastructure in its network of data centres. Briefly showing some impressive pictures and giving an overview of scale, John Wilkes, Principal Software Engineer at Google, then got straight into the examples of starting up services on Google's internal cloud. Beginning with a simple 'hello world' service, John then created a cluster configuration request for 10,000 instances.

10,000 was the number picked because this is the default maximum in a 'cell', a unit of management of clusters. Only 9993 were actually started as some had failed, or more commonly some machines had been taken down for OS upgrades (a rolling scheduled process), or for various other reasons the exact upper limit was not reached, but closely enough to be reliable and at this scale you start to get an appreciation for how inevitable and continuous failures will be in part of the network. John gave us stats collected that indicate that on a 2000 machine cluster, you can expect to have > 10 crashes per day.

This appreciation leads to having more design discussions about reliability; about what happens if something fails while doing maintenance or upgrades, as resilience and fault tolerance are initially more desirable than focusing design effort on speed - as at these resource levels brute force can make up for speed in the short term. John also repeated the remark that we should "treat servers like cattle, not pets", as while your development laptop is likely to be treated like a precious snowflake, the machines you deploy upon can be automatically created and destroyed much more easily. When the jobs/services you are developing have to tolerate faults in this way, it means that migrating tasks from one machine to another is dead simple: kill it and start up a new one elsewhere.

When the system is allocating containers to machines, it takes into account usage levels of memory and CPU capacity. John graphed those for us and corellated the two to identify "stranded resources" - machines that were maxed for one of memory or CPU and so could not have any more services deployed, but had capacity of the other resource that they therefore couldn't use. Identifying these is one of the things Google considers when decided on machine configurations and tweaking the allocation algorithms.

Most jobs or services had their resource allocation requests overstated - devs typically overestimate the needs for their service and some level of this is necessary for [black swan events](http://en.wikipedia.org/wiki/Black_swan_theory#Coping_with_black_swan_events) such as celebrity deaths or global news events, but by and large services ask for more than they actually need. Interestingly, some devs game the system with their knowledge of the scheduler and state need 0.1 CPUs in order to get scheduled and then take advantage of the unallocated resources on machines. This works until the scheduler gets smart and combines many "0.1 CPU" of them on one machine! Lower priority batch jobs run in the space in resource allocation clawed back from production jobs that don't currently need it. Importantly, John advocated doing (safe) experiments with the production systems to find out what will actually happen.

In terms of making the deployment infrastructure available to developers, John described how Google's approach is to avoid exposing underlying mechanisms to people otherwise they will depend on it and you'll find it hard to change your service. Google rely instead upon useful abstractions, for example in the first demo of cluster configuration, the resource allocation is declarative: it tells the system to assign it a certain number of instances, instead of asking for the current number and attempting to call methods to add N thousand more. See also [Tell, Don't Ask](http://martinfowler.com/bliki/TellDontAsk.html).

'Service level objectives' are agreed with teams that depend on certain resources in production, covering the usual -ilities like availability, reliability, obtainability, freshness, accuracy, security. SLOs are a much more honest depiction of the service offerings than 'service level agreements' because SLAs are not guarantees; they exist only so that financial penalties can be levied when the targets are not hit. 

All of this deployment management, metering, reallocation, live experimentation and such is only available to the teams because Google has made such an investment in monitoring. John impressed the importance upon the audience: "If you are not monitoring it, it is out of control". One perculiar example was a rolling linux update that contained a bug where a certain main directory didn't have execute permissions so `ls`, `ps`, `top` and others could not be run. Due to this muting of reporting ability, the defect got as far as 10% of clusters before getting killed. Yet there was no measurable production impact and no users noticed so still recovering from this was successful.

As demonstrated during the keynote, everything in Google internally runs on containers. Seeing the upcoming schedule, John said of Docker "we don't use it internally, as we have our own system, but we really like it". Google have also published the [Kubernetes](http://kubernetes.io/) project, a tool for managing clusters of containerised applications that looks really interesting. Asked about when the utility of Kubernetes kicks in, John replied "If you're going to do one or two or three containers just use Docker. Kubernetes helps you manage things if you have hundreds." so this sounds like the kind of thing that'll start becoming very useful at great scales.

John ended the keynote by summarising with a call for incremental improvement, saying that the likelihood for success and building momentum is much higher than a big-bang project: "roofshot is better than moonshot". John left us with three points to finish:

1. Resilience is more important than performance
2. It's okay to use other people's stuff, don't do it all yourself
3. Do more monitoring

<br />

####<a id="securing_paas"> </a>Securing PaaS with Docker and Weave
*by [David Pollack](https://twitter.com/dpp)*

David Pollack, the creator of [Lift](http://liftweb.net), began his talk about securing PaaS stating he believe that security skills require a different mentality to most developers, and understanding of more granular responsibilities. David said that he wanted to try and hire more replaceable people rather than creating esoteric tech experts (for obvious business reasons) so he preferred more widely understood and adopted technologies for securing his platforms - Docker and IP tables being better collectively understood than JVM Security Manager, in David's example. David also praised Docker's ease of use, providing a declarative format for configuration instead of relying upong Perl scripts and raw [LxC containers](https://linuxcontainers.org/)

David listed a plethora of recent security vulnerabilities, from [Heartbleed](http://heartbleed.com/) to [Shellshock](https://shellshocker.net/) and pointed at the [OWASP Top 10](https://www.owasp.org/index.php/Top_10_2013) to remind people that we can't trust input provided by users - but the issue he encountered when creating a PaaS was that users need to be able to supply arbitrary executable code which therefore can't be sanitised. David listed the threat models that must be considered: app to host via code, app to host via network, app to app via network, app to world via network, app to shared services.

One of the problems David had was considering not only layers (a typical approach to both physical and application security) but also isolating the tenants of the PaaS from each other. Tenants' applications needed to run inside containers on virtual LANs that can talk to each other and shared backend resources but not other tenants. Shared services at the backend may be subject to potential attack, so splitting into read only or write only services can limit surface area and impact.

David addresses these issues in his platform with each tenant application deployed into a Docker container, using Weave to define the tenant-specific subnet and IP tables to secure the access to the rest of the network. Shared data services in an RDBMS use table or column level access controls managed by the RDBMS, and I/O heavy services with well understood security models can also be shared. Credentials for services are isolated to each tenant and not globally visible. 

David said that he was happy with Docker's security as LxC containers are a reasonably well understood technology and the new popularity it meant that there are many eyes looking at it both to exploit and improve it. Finishing his talk, David said that he thinks the move from VMs to containers is as big a shift in approach and utility as the shift from physical machines to VMs; that IP tables still work just fine for network level application isolation; and that a layered approach to isolating risks is still the best approach.

<br />

####<a id="docker_go"> </a>Infrastructure and Go
*by [Jessie Frazelle](https://twitter.com/frazelledazzell)*

Jessie is a core contributor at [Docker](https://www.docker.com) and gave a presentation about how Docker is built with [Go](http://golang.org). After the previous talk which was quite detailed in terms of using Docker to build a PaaS, I thought I'd benefit from a slightly higher level intro into Docker, and I haven't used Go in production before so I was interested in hearing about why they chose it.

Jessie began with giving an overview of what Docker is and what it's for: a runtime for application containers, which are a subset of Linux kernel features such as namespaces, cgroups and pivots. Docker allows you to 'containerise' your application and produce a fully static binary containing all dependencies, giving ease of installation and deployment. This can be as basic as `scp` the container to the target server and bootstrap the binary. Jessie also informed us that Docker support would be coming to Windows, which would bring the lineup to four main platforms (the others being Darwin, BSD Unix and Linux).

Jessie also described a distributed message platform in Go called [NSQ](http://nsq.io) which is used to help scale the Docker project in a number of ways. NSQ is used by the build app responsible for listening to GitHub hooks to trigger builds and deployments, used by the Docker master binary build to run on every push to the master branch, and used by the app which automates building and publishing docs from the code. The team at Docker rewrote a Python-based Jenkins plugin in Go to handle the pull requests, which also uses NSQ to perform housekeeping such as checking for signed commits, labels and documentation comments.

The Go language was chosen by the Docker team for a number of reasons: it's simple, has common useful tools such as `fmt`, `vet`, `lint`, and others for documentation and tests. Some of the issues they found when using Go were in package versioning across the teams and inconsistency in approaches to this. The Go test framework is also still basic and not as fully-featured as those in other languages (like JUnit for example) and so lacks some useful aspects such as setup and teardown step definitions. The Go community is also smaller than that of other languages and as a result is still helpful, friendly and comparatively drama-free (long may it continue for them!).

<br />

####<a id="docker_vs_paas"> </a>Docker vs PaaS
*by [Colin Humphreys](https://twitter.com/hatofmonkeys) and [Paula Kennedy](https://twitter.com/PaulaLKennedy)*

This talk by Colin Humphreys and Paula Kennedy, CEO and COO of [CloudCredo](http://www.cloudcredo.com), was given in another face off style rap-battle-esque format like the [Scala and Grails talk](http://willhamill.com/2013/03/08/qcon-london---day-three/#play-vs-grails---a-fireside-chat) I attended in 2013 so I was somewhat apprehensive. However, this talk was full of demos and specific example comparisons to back up the two sides and worked very well overall. Paula and Colin clearly get along well so the antagonistic nature of the format worked without being awkward, as they represented the 'business' side and the 'innovation/tech' side of our desires for working with software.

Paula began by describing how as COO she wants something that will 'just work' with the minimum investment of time and effort in order to get something valuable to the business as fast as possible. She was advocating PaaS to meet this need, and began with examples of running a simple Sinatra application locally and then deploying it on [CloudFoundry](http://www.cloudfoundry.org/). As anyone who has used a PaaS will expect, this was very straightforward and very fast. The application was demoed live and usable as a real live site within seconds. Paula demonstrated how easy it was to update by making some changes and pushing those to Cloud Foundry to redeploy her application in under a minute.

Colin took over at this point, rubbishing Paula's application deployment as cover while he defined a `dockerfile` definition to declare the container dependencies needed, add user permissions and specify an updated version of OpenSSL, then start the app running in a Docker container locally. This demo worked too and demonstrated how quick it was to get started with Docker - though not quite as quick as with a pre-configured Cloud Foundry account.

This talk was about discussing the difference in needs which may lead you to choose Docker over PaaS - obviously a straight comparison of one versus the other would be illogical, so the two tried to point out the areas where one approach is stronger than the other. PaaS can easily handle multiple application instances and can have autoscaling rules defined; Docker does exactly and only what you configure it to do. PaaS can feature shared services such as health checking of tenant applications, centralised log aggregation, etc; Docker does not seek to provide this and you would need to create it yourself. 

Docker is more about the basics - letting you run your application in a lightweight containerised environment and moving or creating new instances of that container rather than value-adding features like PaaS now tends to be. Docker focuses on customisability and control in ways that you cannot control on PaaS (more on that in Jessie's second talk). Docker container provisioning is much faster than instantiating a new virtual machine on IaaS.

Colin and Paula argued each other down to an agreement: PaaS is likely to be better for fast iteration of a basic application, and Docker is likely better for control and more specific needs such as database management. Colin recommended that PaaS be considered more for apps following the [12 Factor principles](http://12factor.net), and containers with storage volumes used for stateful micro-services. Personally I see no good reason why 12 Factor apps should benefit more from PaaS other than the common shared services such as process management, logging and healthchecks, which are easy enough to bake into your own applications and deploy then in Docker containers (still currently in love with [DropWizard](http://dropwizard.io/) for these common features).

I think it's hard to divide a talk into covering two things and still reach the depth at which the real nuances are exposed. Deploying just a single tiny monolith application with no particularly unusual dependencies or configuration needs is arguably not as useful an example as deploying something with multiple components and specific platform needs. Comparing PaaS and Docker to handle organising deployments of multiple communicating services would be very interesting but realistically is likely to be unable to fit inside a single presentation unless a lot of the work was pre-canned, and then you'd lose a bit of the depth of the detail due to having to summarise and retrofit context to the problem. Nonetheless, I was pleasantly surprised by this talk given my expectations of the format.

Overall I was convinced that the argument comes down again to whether you want to give up control of low level concerns in order to benefit from paying for more hands-off deployments and scalability, and if you can live with the lock-in that PaaS tends to imply. [It depends](http://willhamill.com/2015/03/02/it-depends-is-the-shortest-correct-answer/) - on your particular environment constraints :).

<br />

####<a id="docker_clustering"> </a>Docker clustering: batteries included, but removable
*by [Jessie Frazelle](https://twitter.com/frazelledazzell)*

The Docker fun train continues at full speed with Jessie's second talk about how Docker clusters can be managed using out-of-the-box (OOTB) tools, and how if you really feel strongly about it, you can use something else due to Docker's plugin approach.

Jessie began this talk too with a very brief overview of Docker to give the audience some shared context; context most people had acquired either through use of Docker themselves (lots of hands in the air with positive replies to being asked who had tried or used Docker), or Jessie's earlier talk. See two writeups up for the high level summary.

Docker supports clustering of containers OOTB with [Swarm](https://github.com/docker/swarm) which serves the standard Docker API and allows transparent scaling to multiple hosts. If Swarm isn't your bag, [LibContainer](https://github.com/docker/libcontainer) which is also written in Go can be used, and LxC containers are now supported as well.

Service discovery is also provided OOTB with Docker, though it can be configured to use [etcd](https://github.com/coreos/etcd), [consul](https://www.consul.io) or [zookeeper](http://zookeeper.apache.org/) instead. For scheduling, bin packing is provided OOTB and there is also a native option, with [Mesos](http://mesos.apache.org) currently on the way.

Jessie then gave a demo of using Docker with Swarm to define clusters of containers and manage them on the CLI. Regular Docker commands for individual container management work with Swarm, and also Swarm adds a number of commands for provisioning clusters, joining containers to clusters and the like with simplicity: `docker pull swarm`, `docker run --rm swarm create` and `docker run -r swarm join`. 

(At this point in the talk I think things started going over my head as I've had such little real life exposure to cluster management or containerisation, but it's clear there is a great set of tools here and plenty of options for customisation with existing tooling. One of my colleagues is working on a project for another client using Docker so I must go down and see how it's working for them.)

After describing some more advanced features such as setting container affinity (running containers 'next' to each other on the underlying machines, to take advantage of proximity between service container and DB container, for example.) and selecting different storage drivers. Jessie also gave a demo of running a small cluster of three containers on three different flavours of Linux using the three different storage drivers.

Wrapping up, Jessie outlined the future direction of Swarm; rescheduling policies, further backend drivers for OOTB management functionality, support for Mesos, cluster leader elections and more & faster integration with new Docker features.

<br />

####<a id="big_java"> </a>Responding rapidly when you have 100GB+ data sets in Java
*by [Peter Lawrey](https://twitter.com/peterlawrey)*

Peter's talk about managing Java applications which use vast in-memory data sets was interesting, and quite detailed at a low level compared to other talks at the conference. Some of the notes I have taken aren't very useful without the accompanying slide diagrams showing how memory spaces are mapped and constrained at different JVM versions and address space lengths, so [check out the QCon site in case the slides go up](http://qconlondon.com/presentation/responding-rapidly-when-you-have-100gb-data-sets-java) for a visual accompaniment.

Peter described how he believes that a modern system should be reactive: responsive, resilient and elastic. When your weapon of choice is the JVM, you can process data much faster when you can map your entire data set into memory (given I/O bottlenecks, I'm sure this is true for almost any language). However, what happens when you move into the realms of very large data sets - which in Java land is pretty much anything beyond 32GB?

Peter espoused resilience in the application for one main reason: rebuilding the data set in-memory after a failure is limited by memory controller and other machine bottlenecks, which takes orders of magnitude longer as the order of magnitude of the data set size increases: 10GB can be rebuilt in 2 minutes, which would seem comparatively fast against rebuilding a 10TB data set in 2 hours.

In terms of accessing more memory on the JVM, going beyond 32GB on standard compute platforms means you'll need to jump up to 64-bit address references, which though increasing available memory area also reduces the efficiency of CPU caches due to increased object size. Garbage collection of such larger memory spaces also starts to become a problem, with a concurrent collector being needed to avoid stop-the-world execution pauses.

Peter described how the [Azul Zing](http://www.azulsystems.com/products/zing/whatisit) concurrent collector was an option for tackling this issue up to a given size, as for memory sets of around ~100s GBs their garbage collector will perform with minimal execution impact. A different approach would be to use TerraCotta BigMemory as a memory management layer inside your application, allowing the application to use off-heap memory, though the disadvantage is needing to explicitly build applications against their library so it can't be injected in to existing applications as a mitigation in the same way using Azul Zing could be.

When addressing bigger data sets of up to 1TB in Java, the [NUMA](http://en.wikipedia.org/wiki/Non-uniform_memory_access) region limit kicks in at around 40 bits of physical memory (40 bits for Ivy Bridge and Sandy Bridge generation Intel CPUs, 48 bits for Haswell generation CPUs). Addressing beyond 40 bits requires using a 48-bit virtual address space, with data paged in on demand. The 48-bit limit then pushes the threshold to 256TB in CentOS, 192 TB in Windows and 128TB in Ubuntu. I can't wait for someone to be quoted at this point saying "128TB will be enough for anyone!" that we can all look back upon and laugh in 2025 :). Moving further up the orders of magnitude, a 1PB (Petabyte!) memory space can be achieved by mapping the address tables themselves into the main addressable space, in order to achieve paging of the virtual space.

A question I asked of Peter was at what point you want to make a call on the investment in understanding and managing this massive vertical memory size and consider the tradeoff against distributing the set amongst machines or application instances a better option. Peter answered this by pointing out that for certain problems like trading or other financial systems where large data sets are needed with very low latency, the time delay introduced by the network hop is actually less of a problem than the bandwidth constraint of going to I/O and over the network connection, compared to the bandwidth available in the memory controller.

<br />

####<a id="protocols"> </a>Protocols: the glue for applications
*by [Torben Hoffman](https://twitter.com/lehoff)*

The last talk of the day was by Torben Hoffman of [Erlang Solutions](https://www.erlang-solutions.com) about how Erlang encourages a different approach to designing systems; a process-oriented asynchronous style with a focus on understanding how the interactions between communicating processes should be designed - hence protocols.

Torben opened up with a look at some waste and damage created by failing computer systems and recommending to the audience that we learn more about asnychronous and distributed processing by reading Tony Hoare's book on [Communicating Sequential Processes](http://en.wikipedia.org/wiki/Communicating_sequential_processes) (this brings me back - last time I heard about CSP was discussing multiprocessing with my supervisor during my research dissertation in university!)

Torben advocates Erlang for learning how objects should solve problems by communicating with each other, rather than 'single page programming' where people learn only to develop with an understanding only of the current class. Torben proclaimed the 'golden trinity' of Erlang: fail fast, failure handling, share nothing. Including failure handling as a specific case in your protocol means you should be able to handle failure gracefully. In Java world, failures are not tolerated and unexpected exceptions cause your process to die. In Erlang world, failures are embraced as alternate scenarios and managed.

Torben gave an example of a financial application for a simple stock exchange. Buyers post purchase intentions, sellers post sale intentions, deals happen when the seller price <= buyer price. In Erlang, this will be modelled using one buyer process and one seller process per sale interaction, communicating by sending messages that form the sale protocol. [gproc](https://github.com/uwiger/gproc), a process registry, would be used as a pub/sub mechanism for buyers and sellers listen for messages of intent to sell/buy. After price conditions are met, the sale is confirmed with a three-way handshake.

Failure is handled in the message protocol such that when the buyer or seller dies after the initial message of intent (determined by response timeout or monitoring the other process) then the processes can simply restart the interaction. If a party dies after the first part of the handshake, e.g. buyer dies before getting sale complete message after seller closed sale on their side, a restart of the process will the buyer back to the previous state. A supervisor process is commonly used in Erlang to monitor worker processes and handle restarts. Other options for handling failure in the stock exchange are to keep a transaction log per-process in order to easily replay until the last state. Alternatively a central ledger process could be used which tracks completed deals and allocates buyer and seller processes deal IDs so they can link back up when they fail.

Torben demonstrated using message sequence diagrams that these failure scenarios are explicitly handled as other cases in the protocol, and using that kind of diagram can be useful to identify risky areas and complex communications.

Wrapping up, Torben spoke briefly about testing. Testing asynchronous processes is definitely hard, but he recommended using [Erlang QuickCheck](http://www.quviq.com/products/erlang-quickcheck/) for good randomised property-based checking, and also suggested focusing on the calls and interactions inside a single process, mocking out the messages being received and testing the internal behaviour.

Torben's talk was very lively and amusing and has made me want to spend some time playing around with Erlang and seeing how things are done with it. I may not use it in production (never say never) but the value in finding out about how more different languages approach problems gives you a new perspective to solving them.


