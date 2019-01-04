---
layout: post
title: "Thoughts on AWS re:Invent 2018"
description: "A summary of the AWS re:Invent conference 2018 featuring plenty of new announcements about serverless, machine learning, managed services and more."
category: 
tags: ["aws", "serverless"]
---
{% include JB/setup %}

### Even bigger than last year

Once again re:Invent was a massive conference, bigger than last year at around 53,000 people, across half a dozen venues and with approximately [nine trillion talks and sessions](https://www.youtube.com/user/AmazonWebServices/playlists?sort=dd&view=50&shelf_id=33). The logistics and organisation was really impressive, and everything went smoothly aside from the occasional over-subscribed session but this was better than the year before with more overflow areas.

I'll use this post to briefly summarise and describe my thoughts on the new services that I can remember that seem significant - so excluding probably some unknown number of things I've forgotten about in amongst [all the other announcements](https://aws.amazon.com/new/reinvent/), and deliberately omitting some things that aren't hugely relevant to me like [managed windows filesystems](https://aws.amazon.com/blogs/aws/new-amazon-fsx-for-windows-file-server-fast-fully-managed-and-secure/) or indeed the [AWS Ground Station](https://aws.amazon.com/blogs/aws/aws-ground-station-ingest-and-process-data-from-orbiting-satellites/) service which might be more interest to those of you who operate a fleet of satellites.

##### tl;dr for busy people
* Serverless gets updates for tooling and integrations, custom languages
* More Machine Learning high level services, improvements to lower level services
* AWS Outputs is the AWS gateway drug for cloud holdouts

<br />

## Broad brush

### More everything than the competition

This year in the media-friendly keynotes AWS were pushing a message about their breadth and depth of cloud services - despite being the market leader in cloud computing with greater absolute growth than their [most significant](https://azure.microsoft.com) [competitors](https://cloud.google.com/) they've seen lower proportionally relative growth which seemed to irk CEO Andy Jassey who took analysts to task in [his keynote](https://www.youtube.com/watch?v=ZOIkOnW640A) while talking up the impressive scale and array of services that AWS offers. 

There's no doubt that AWS offers the widest range of features across cloud platforms, and at one point in Jassey's keynote he made a jab at one of their nearby competitors from Seattle whose main response to new AWS features is via marketing rather than engineering (see the bit from 08:41 in the keynote). Many of this year's announcements are oriented around removing undifferentiated heavy lifting; productising custom work that people have been doing and externalising some AWS services so customers can use them as a richer platform to build their domain-specific applications upon.

### Serverless was a common theme

Probably the most overwhelming message this year was that Serverless is the way forward. From the number of sessions, the number of vendors using and assisting you with it in the expo, and the emphasis put during the announcements, it's clear that Amazon see this segment as being a really valuable part of cloud computing - both for them and also for customers who can make use of it to save money and more importantly time. More AWS services are getting integrations with Lambda (such as [Application Load Balancer](https://aws.amazon.com/about-aws/whats-new/2018/11/alb-can-now-invoke-lambda-functions-to-serve-https-requests/)) and even Dynamo DB gets better at [provisioning capacity on demand](https://aws.amazon.com/blogs/aws/amazon-dynamodb-on-demand-no-capacity-planning-and-pay-per-request-pricing/) with pay-per-usage to really get away from that manually provisioned throughput stuff that people had to use until now.

### Reducing the barrier to entry

AWS are also trying to reduce the barrier of entry for users to take on new services and adopt serverless technologies, which I suspect is part of desire to move their own customers up the value chain internally rather than resting on their laurels and being happy with everyone using EC2 VMs inside a VPC with RDS. One of the nice things to help adoption for customers who are particularly daunted by the task is [Amazon Control Tower](https://aws.amazon.com/controltower/features/) which will help people set up a set of accounts and network infrastructure with the [Landing Zone pattern](https://aws.amazon.com/answers/aws-landing-zone/) which again removes some of the undifferentiated heavy lifting for customers.

### A tool for Well-Architected reviews

A new [AWS Well-Architected Tool](https://aws.amazon.com/well-architected-tool/) was announced to help deal with the scaling bottleneck that Amazon's own Solution Architects and partner SAs have been trying to fulfil when requested to do [Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/) reviews. Checking that your architecture and design meet common good practices in the areas of cost optimisation, operation excellence, security, reliability and performance is a good thing to do yourself if you've read [the whitepaper](https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf), but with so much to learn and assess within the AWS services, and the expansion of the framework into suggesting patterns and practices for different 'lenses' such as [IoT](https://d1.awsstatic.com/whitepapers/architecture/AWS-IoT-Lens.pdf) and [Serverless](https://d1.awsstatic.com/whitepapers/architecture/AWS-Serverless-Applications-Lens.pdf) it's not surprising that the SAs are often called upon to give their view on things, so the new Well Architected Tool will help by automatically reviewing certain parts of your AWS infrastructure and also act as a point to find guidance on implementation.

### Simplifying existing patterns

Continuing the theme of making things simpler to manage and maintain, [AWS Transit Gateway](https://aws.amazon.com/transit-gateway/) takes a common pattern of the Transit VPC and encapsulates it like a managed service (as NAT Gateway is to a NAT instance) and improves cross-VPC routing and peering with cross-VPC routing tables, reducing the amount of individually defined peering and transit permission setup and improving the VPN bandwidth and resiliency. 

[VPC Sharing](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-sharing.html) and [Resource Access Manager](https://aws.amazon.com/blogs/aws/new-aws-resource-access-manager-cross-account-resource-sharing/) (announced just before re:Invent) also will help to help manage network space and resource sharing by allowing the same subnets and associated infrastructure to be accessed across accounts in an Organisation while still partitioning them so that the account owners remain capable of managing the account-specific resources in their networks. There's a [good session covering this](https://www.youtube.com/watch?v=ar6sLmJ45xs) and how it can help simplify a couple of common patterns of network architecture which you might find useful if you're working in the network space.

### Obligatory Blockchain mention

AWS also finally announced something with blockchain, which the industry has been going mad about for an awfully long time [without actually producing anything valuable](https://www.theregister.co.uk/2018/11/30/blockchain_study_finds_0_per_cent_success_rate/) other than magic internet scam coins and some overheated data centres. [Amazon Managed Blockchain](https://aws.amazon.com/managed-blockchain/) ticks that box, and from the launch announcement it seemed clear that the reason it took so long as that AWS didn't see any significant valuable use case for it. Now, however, they've decided that if you're going to throw your money away anyway then you may as well throw it to them. Fair enough. 

In news with more actual utility, Amazon also have released a piece of loosely related technology known as [Amazon Quantum Ledger DB](https://aws.amazon.com/qldb/) which provides an immutable, cryptographically verifiable, centralised transaction log which no doubt actually meets more actual real-world use cases than bastardising the blockchain into the world's slowest MS Access database. Indeed, if you're using AWS at all, you're already using QLDB behind the scenes, which was Amazon's own internally developed technology for immutable transaction log based systems such as provisioning new EC2 instances and recording the writing of messages into Kinesis streams. Sadly for those of you still searching for citable instances of blockchain technology, it is based on Merkel Trees rather than blockchain.


<br />

## "Don't call it hybrid" cloud

### AWS Outposts

[AWS Outposts](https://aws.amazon.com/outposts/) was announced allowing you to order a big rack of servers straight from Amazon (but does it come with Prime Delivery?) ready to be plugged into power and network cables at your site, creating or extending your own datacentre with the same kit Amazon uses in services like EC2, and more importantly, which can be managed using the same APIs that you use to manage in-cloud infrastructure. This can give users a first-hit of their AWS APIs for managing infrastructure before they migrate to the cloud, or for customers that specifically decide to create a hybrid setup by installing these at a site, can still use the same APIs they know and love.

Bizarrely, the CEO of VMWare was brought on stage to hug and chat with Andy Jassey about this, extolling the virtues of being able to use the VMWare tools to manage the Outpost and also talking up [RDS on VMWare](https://aws.amazon.com/rds/vmware/), providing yet another path for people to get hooked on the nice managed service stuff that might lead them towards investing more in an AWS migration.

A good discussion I had during re:Invent was in the evening after the first keynote when I was chatting with [Peter 
Campbell](https://medium.com/@petecam), the CTO of the Digital Services business unit in [Kainos](https://www.kainos.com) who made the point that AWS's biggest competitor isn't Azure or Google Cloud, but people who are running their own datacentres themselves - be it in-house or outsourced. The majority of these people may be staring a sunk cost in the face and writing off depreciation while they hold out on migrating to the cloud, though occasionally some are likely running infrastructure close to the location of large, frequently updating datasets or in remote locations (perhaps on an oil rig, or next to your large manufacturing plant where you want to make fast decisions on very large amounts of data you can't wait on uploading to the cloud). 

Both of these types of people could benefit from AWS but can't or won't migrate. The majority of these customers are indeed using VMWare to manage their own datacentres, so AWS Outposts being an ideal gateway drug to get people hooked on not just the AWS APIs but the feeling of safety in delegating more and more of the infrastructure management to AWS, which can draw more customers into the cloud. It seems like AWS Outposts is perfectly designed to eat VMWare's lunch while VMWare give people an alternative API that they already know to manage the AWS hardware.

Note to self: perhaps I should fork [my chrome plugin](https://github.com/willh/cloud-snark) and change 'Datacentre connected to Azure ActiveDirectory' to 'VMWare SAN connected to AWS Outpost' 🤔


<br />

## Serverless Sweetness

### AWS Lambda gets better tooling

Part of helping this adoption is better tooling including the [AWS CDK](https://awslabs.github.io/aws-cdk) which lets you provision infrastructure in many common languages on top of CloudFormation, which has some [nice examples here](https://awslabs.github.io/aws-cdk/examples.html), and also [better toolkits to do things like Lambda debugging in major popular IDEs PyCharm, IntelliJ and VS Code](https://aws.amazon.com/blogs/aws/new-aws-toolkits-for-pycharm-intellij-preview-and-visual-studio-code-preview/) which is a nice way of admitting that [Cloud 9](https://aws.amazon.com/cloud9/) might be nice but realistically not a lot of people are using it right now, as old coding habits die hard.

### Lambda Layers

[Lambda layers](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html) were announced as a way to resolve external libraries and function-wrappers into lambda function definitions to compose functionality together. Essentially this means "a zip file we download during lambda bootstrapping that your lambda can also use" which keeping it nice and generic can be used for a lot of different purposes like proxying functions through authentication filters, encapsulating your function in timing wrappers, implement common error handlers or whatever other shared/common code that your function needs, letting you externalise and separately version the layer from the function rather than explicitly injecting its code into your function artefact. This will make composing parts of lambda functions from reusable parts easier, and combined with [support for nested applications in the Serverless Application Repository](https://aws.amazon.com/about-aws/whats-new/2018/11/sam-supports-nested-applications-using-serverless-application-repository/) means you can bring in those common pieces of function code from places where it already exists more easily, and share layers both internally within the organisation and publicly.

### Custom Runtimes aka BYO Language

One very interesting thing that the extended lambda deployment model enables via layers is that of [Custom Runtimes for lambda](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-custom.html) which lets you bring along your own runtime environment as a layer which will be invoked by lambda, which can then set up an execution environment, get the lambda events and pass them on to your functions written in whichever language you want to support in your runtime. This immediately opens the door to AWS-supported additional languages such as [Ruby for lambda](https://aws.amazon.com/blogs/compute/announcing-ruby-support-for-aws-lambda/), [C++](https://aws.amazon.com/blogs/compute/introducing-the-c-lambda-runtime/) and [Rust](https://aws.amazon.com/blogs/opensource/rust-runtime-for-aws-lambda/) along with third-party provided open source runtimes for language such as [Erlang](https://github.com/alertlogic/erllambda) and [Elixir](https://github.com/alertlogic/mix_erllambda), [COBOL](https://www.bluage.com/news/serverless-cobol) (of all things) and [PHP](https://www.stackery.io/blog/aws-lambda-php/) (if you really have to).

### Opinions as a Service

This year Amazon presented not just a myriad of ways you can make use of their services, but in a bit of a change, got a bit opinionated and rolled out [Tim Bray](https://www.tbray.org) who gave an entertaining and spirited talk on how Amazon themselves choose to build services internally and the lessons they've learned along the way. This one was really interesting and covered lots of areas that are touched on more agnostically in other sessions like how to reduce blast radius in architecture, how to deploy services while keeping uptime and existing data sacrosanct, and how internally some 'serverless' services like SQS are managed entirely with server-ful constructs whereas some other server-ful ones such as Amazon MQ are managed with serverless constructs. Ironic? You decide. But the talk is [available here on YouTube](https://www.youtube.com/watch?v=IPOvrK3S3gQ) and Tim has also sliced and diced parts into [a small series of blog posts](https://www.tbray.org/ongoing/When/201x/2018/12/09/Serverlessness) for those who don't want to sit and watch for a full hour. 

More details on how AWS develop services themselves, talks on culture/org, reducing blast radius, internal service development
[Werner Vogels](https://twitter.com/Werner) gave a session for the European Government Delegation which I attended by way of my public sector engagement on how Amazon organise themselves internally and attempt to foster innovation. There were no recordings of the EGD sessions unfortunately but a lot of the material has been presented in other forms by Werner and others talking about two-pizza teams, empowerment and accountability, references back to the now famous Netflix culture presentation deck and other ways in how Amazon seeks to remain customer focused and build services by removing undifferentiated heavy lifting based on requests from their customers.

### Improving how you glue services together

A product announcement that triggered a bit of a "wait, didn't that always exist?" reaction was the launch of [Lambda integration with ALB](https://aws.amazon.com/blogs/networking-and-content-delivery/lambda-functions-as-targets-for-application-load-balancers/) allowing you to use a load balancer endpoint as the trigger for a lambda function without having to wrap an API Gateway around it. Should make life easier for some of the simpler, or more internal facing use cases where adding an API Gateway is overkill.

More [service integrations with Step Functions](https://aws.amazon.com/about-aws/whats-new/2018/11/aws-step-functions-adds-eight-more-service-integrations/) were announced helping compose more complex and meaningful workflows from Step Functions and their integrated services. I've not played around with Step Functions much myself but it seems to me like they are pushing workflow and complex stateful app development into the lambda space while further draining undifferentiated glue-code out of bespoke applications and into the configuration of how AWS services are composed together. This could be good for reasoning about and maintaining individual functions, but it might make the integration of the whole system a bit more complex when you need to maintain a mental model of the step function state machine and its integrations in your head as opposed to looking at a single code class responsible for orchestrating 4-5 calls.

### Firecracker burns up FUD surrounding lambda execution model and security

One of the most interesting sessions for Lambda enthusiasts was the one on [Lambda Under The Hood](https://www.youtube.com/watch?v=QdzV04T_kec) from [Holly Mesrobian](https://twitter.com/AWSreInvent/status/1068197793758494720) and [Marc Brooker](https://twitter.com/MarcJBrooker) giving us the goods on how Amazon now runs AWS Lambda on [Firecracker](https://aws.amazon.com/blogs/aws/firecracker-lightweight-virtualization-for-serverless-computing/) micro-VMs achieve the desired level of isolation between function invocations while keeping cold-start times low (VM initialisation in < 150ms!), both super desirable in environment-on-demand situations. Firecracker is an interesting technology but one that hopefully only major platform providers will be using, as anyone [building a 'serverless' platform and running it on their own infrastructure](https://www.serverlessops.io/blog/aws-firecracker-build-your-private-serverless-platform) is rather desperately missing the point.

### Lots of talks on serverless development and operation

There were [plenty of sessions](https://www.youtube.com/watch?v=bWcpmJCFhTM) about [developing applications](https://www.youtube.com/watch?v=08AjVGGQaKQ) with [serverless](https://www.youtube.com/watch?v=IPOvrK3S3gQ) [technologies](https://www.youtube.com/watch?v=YwHxvKhBQ_g), [most of which are now up on YouTube](https://www.youtube.com/playlist?list=PLhr1KZpdzukcZIPswLEcVzw8HKF_yM0r3). I'd recommend Tim Bray's one I linked earlier and [this one on Optimising Serverless Applications](https://www.youtube.com/watch?v=sSSMTSn2xmA) for some more in-depth techniques for serverless development, which was presented by [Chris Munns](https://twitter.com/chrismunns) at the particular repeat that I attended, which has a [nice summary slide](https://twitter.com/willhamill/status/1067493956131463175) that might hook you if AWS lambda is your bag.

Generally speaking there were lots of examples from across the two keynotes, to the sessions presented, of customers going serverless or even serverless-first. The missing manage-your-kubernetes-install-for-you vendors from last year's Expo appear to have been replaced with monitor-your-serverless-functions-for-you vendors this year, so there are clear trends emerging in both uptake and support in the community and marketplace. Containers seem to be getting less of a push, though there were still lots of talks on k8s and still quite a lot of vendors to sell you plugins and services around it - perhaps my perceived difference is just that the early majority are now getting along with k8s and you hear less about stuff that isn't as new.


<br />

## Machine Learning & AI services

### Special chips and oomph on demand

Machine Learning got another boost with the announcement of a [custom made AWS Inferentia chip](https://aws.amazon.com/machine-learning/inferentia/) designed to accelerate ML applications at low cost (seems to me like someone was inspired by Google's TPU). [Amazon Elastic Inference](https://aws.amazon.com/blogs/aws/amazon-elastic-inference-gpu-powered-deep-learning-inference-acceleration/) seems to be a projection of 'what if Elastic GPU but for AI?' into an actual product offering, letting you mix GPU acceleration for certain applications (if you've picked one of the supported frameworks and made the necessary tweaks) into your infrastructure giving your more flexibility to get a bit of additional inference power without having to jump up cost categories by stepping up to a bigger base instance family. 

### AI Managed Services

In terms of nicely packaged higher level AI services, [Amazon Forecast](https://aws.amazon.com/blogs/aws/amazon-forecast-time-series-forecasting-made-easy/) was announced which will help you draw your graphs up and to the right with less wildly unrealistic results compared to some common approaches, [Amazon Textract](https://aws.amazon.com/textract/) will do fairly advanced OCR on scanned images with table detection and form parsing, and also [Amazon Personalize](https://aws.amazon.com/personalize/) makes another technology developed for Amazon.com available to consumers to help make recommendations for users based on patterns of previous actions, which seems like a bold move to turn one of their retail site competitive differentiators into a platform play.

### SageMaker updates

The SageMaker service has been extended with [Amazon SageMaker Ground Truth](https://aws.amazon.com/blogs/aws/amazon-sagemaker-ground-truth-build-highly-accurate-datasets-and-reduce-labeling-costs-by-up-to-70/) to take the effort out of classification of large data sets which will be used for machine learning training, and also [Amazon SageMaker RL](https://aws.amazon.com/blogs/aws/amazon-sagemaker-rl-managed-reinforcement-learning-with-amazon-sagemaker/) for [reinforcement learning](https://en.wikipedia.org/wiki/Reinforcement_learning) and am interesting little demonstration platform (like last year's DeepLens) called [DeepRacer](https://aws.amazon.com/blogs/aws/aws-deepracer-go-hands-on-with-reinforcement-learning-at-reinvent/) which is an AI-controlled car (and racing league!) that developers can use to learn how to develop and deploy RL machine learning algorithms. This one seems quite fun but unfortunately unlike last year's DeepLens giveaway at the hands-on lab sessions there were no free DeepRacers for attendees!

### More managed services

Lost in amongst the machine learning updates was a new product called [Amazon Timestream](https://aws.amazon.com/timestream/) which sadly isn't a device allowing you to retrieve sports almanacs from the future in order to create a dystopian alternate future with yourself as President, but rather a [time series database](https://en.wikipedia.org/wiki/Time_series_database) which could help people store operational and financial metrics and which can be used in Amazon Forecast and other statistical modelling scenarios. No doubt someone will instead use it to roll their own [Prometheus](https://prometheus.io/) type setup for system monitoring, creating an interesting project and a lot of additional work for themselves.

Another example of a service developed by AWS meeting the customer where they're at, rather than just insisting they get on board with how Amazon want things to be is [Amazon Managed Streaming for Kafka](https://aws.amazon.com/msk/) which changes the usual answer for the question of "How do I run Kafka on AWS?" from "Just change your use case until it fits Kinesis" to "Use Managed Kafka" which is going to be more palatable for people working on migrating existing architectures. The same thought process, no doubt, that caused Amazon to release [Amazon MQ](https://aws.amazon.com/amazon-mq/) last year as a managed ActiveMQ setup and an alternative to the wholly proprietary SQS.


<br />

## Networking, no the other kind of networking

Attending as a member of the European Government Delegation (I guess UK public sector work won't get invited to that party next year...) was also useful to meet other people from public sector, reconnect with a few people I'd met in passing in my current engagement, and in hearing a few talks specifically from EGD members. The talk content curated for the delegation seemed fine but a significant amount of it was scheduled [inevitably] to clash with talks I wanted to attend in the main conference unfortunately. The networking event in the evening for public sector generally, with a little slightly-less-overpoweringly-loud section roped off for EGD was good and gave me a chance to see some other people I'd not seen in quite a while, and meet some others that I hadn't met before who were dealing with interesting variations of the same problems my clients deal with in our public sector work. I'd definitely recommend the industry/tech specific networking sessions, as even though the Serverless Pub Crawl was hugely oversubscribed there were one or two good conversations I'd perhaps not have had the chance to strike up elsewhere.


<br />

## Wrap-up

Again, I hugely enjoyed attending AWS re:Invent in 2018 and once again I'd highly recommend it to anyone with an interest in AWS or cloud technologies. This year because of the session sprawl it seemed a bit more daunting but with a big increase in the number of repeated sessions there were few things I wanted to attend but missed. I think next time I'd probably mix in more of the hands-on or chalk-talk sessions to get some more of the opinions of the people seated next to me, though I'm glad I struck up those conversations in the queue for talks, at lunchtime, and in the pub with people I didn't know - I recommend making use of the 'hallway track' as people call it.
