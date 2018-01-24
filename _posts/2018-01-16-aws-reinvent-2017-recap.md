---
layout: post
title: "AWS reInvent 2017 Recap"
description: "A summary of the new product and service announcements I think were most relevant at the AWS re:Invent conference in 2017. EKS and Fargate are revealed, serverless and IoT services get a big boost, and machine learning becomes much more accessible."
category: 
tags: ["aws"]
---
{% include JB/setup %}


##### tl;dr for busy people, this one is a big one
* AWS finally release a managed kubernetes service 🎉 
* Serverless and IoT get a big boost in functionality and usability
* New Machine Learning services make ML much more accessible
* Various other upgrades make stuff nicer across the board, like M5 instances and cross-region VPC peering


<br />

### The Conference

The [re:Invent conference](https://reinvent.awsevents.com) was held as usual in Las Vegas in the US, from 27th Nov to 1st Dec, attracting an incredible 43,000 attendees and sprawling out now across three [main](https://www.venetian.com) [conference](https://www.aria.com) [venues](https://www.mgmgrand.com/). Being lucky enough to be sent to attend by [Kainos](https://www.kainos.com) I was there for the keynotes, many product launches, a small proportion of the ~1300 sessions from intro to expert level, and also benefited from the chance to do hands-on workshops and breakout/Q&A sessions with AWS engineers and architects. This was the biggest conference I've been to and it was pretty exciting, and talking to many other people who are at different stages in their AWS adoption was really interesting.

There were lots of different product launches at various states of readiness from announcing 'upcoming preview' to general availability across all AWS regions today, so there was definitely something for everyone. If your tastes run in the IoT, machine learning, container management or serverless flavours then you may have been particularly satisfied. I'm going to cover in this post the majority of what I see as the big announcements in these areas, leaving a few other things off the menu for you to catch up on [at the source](https://aws.amazon.com/new/reinvent) if you'd like.

<br />

## Managed Services


<br />

### Elastic Container Service for Kubernetes (EKS)

Hip hip hooray - many customers have been asking Amazon for something like this, to lower the barrier to entry for learning and subsequently deploying Kubernetes in production. Google and Microsoft have had Kubernetes-flavoured container management systems for a while now but Amazon appear to have finally finished betting only on their own proprietary ECS service and are adopting EKS. The [EKS service](https://aws.amazon.com/eks/) is a means of having AWS manage your Kubernetes master as if it was an API endpoint and without you having to provision EC2 nodes or handle the internal infrastructure needs for k8s.

The Kubernetes master provided to you in EKS is provisioned by the ECS system with a 3-node high availability setup (1 per AZ), with all management of the cluster master taken away from you and replaced with a service endpoint and API based off the latest stable upstream Kubernetes from source. Scaling, failover, upgrades and maintenance of the cluster master is handled, so you need to bring a set of worker nodes to the cluster party to have the containers distributed across them. EKS is currently in 'preview' with no definitive launch dates aside from 'early 2018'.


<br />

### Amazon Fargate

This service is something I've been hoping for, for a while. Bring a container along and define a set of tasks based on how much resources you want to allocate to the container instances, and [Fargate](https://aws.amazon.com/blogs/aws/aws-fargate/) will handle the rest. Fargate will deploy your container app onto ECS (and EKS in the near future) and not just provision a cluster master for you, but will also automatically create and scale a set of worker nodes for you, register them with load balancers, and distribute your containers across them. 

This service is a level of abstraction up above the direct cluster management that we've been having to handle to run containers in production. I think in the next few years services like this will start to let people deal with containerising production workloads at a much lighter touch: define your service and encapsulate its dependencies, define how much resource you want to throw at it, and who it can talk to. Everything else will be taken care of for you. Kubernetes & Docker may well win the container wars, but Kubernetes being the container orchestrator will become simply an interesting detail of the platform you take for granted and not something you deal with directly.


<br />

### EC2 instance improvements

[M5 instances](https://aws.amazon.com/blogs/aws/m5-the-next-generation-of-general-purpose-ec2-instances/) are out, with approx 14% better price/performance than the equivalent M4 instances. Moore's Law marches onwards and the consumer benefits from it. Similar to the C5 instance type's use of the Nitro hypervisor, moving the network stack into hardware virtualisation, overheads compared to bear metal are minimal. [Check out this interesting talk about the C5/M5 instances](https://www.youtube.com/watch?v=LabltEXk0VQ) if you're into the low level details. 

In other EC2 news, it's now much easier to create spot instances to run interruptible workloads on spare EC2 capacity at a very low cost by setting [simplified preferences for spot availability](https://aws.amazon.com/about-aws/whats-new/2017/11/amazon-ec2-spot-introduces-new-pricing-model-and-the-ability-to-launch-new-spot-instances-via-runinstances-api/) when you're defining your EC2 nodes.

EC2 spot instances can now benefit from [hibernation](https://aws.amazon.com/about-aws/whats-new/2017/11/amazon-ec2-spot-lets-you-pause-and-resume-your-workloads/), much in the same way as how your laptop flushes RAM to disk when you close the lid in order to save the state of your running apps, then resumes when you open it again.

[Placement groups](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html) are a way of deploying a number of EC2 nodes in AWS in close proximity and are analogous to having them deployed on the same underlying host to benefit from really low latencies between nodes. [Spread placement groups](https://aws.amazon.com/about-aws/whats-new/2017/11/introducing-spread-placement-groups-for-amazon-ec2/) are almost the opposite - analogous to having the EC2 nodes distributed across distinct hardware such that you won't lose the whole set if a host goes down. A spread placement group can also be spread across multiple Availability Zones.


<br />

### EC2 Bare Metal

For customers who want direct access to physical hardware to take advantage of certain CPU hardware features, or maybe to run software that isn't licensed for virtualisation (boooo!!), EC2 Bare Metal instances make getting at the actual underlying hardware possible. This uses the same tools used to manage EC2 instances that are virtualised, and integrates with ELBs, auto-scaling, etc the same as 'regular' EC2 machines. This move has been made possible partially by the move to the Nitro hypervisor, taking software network virtualisation out of the picture - see the video link in the M5 section above for more.


<br />

### EC2 T2 Unlimited

EC2 T2 nodetypes are cheaper, low-power nodes that run on a 'CPU Credit' balance, with credits spent bursting up to stated CPU performance and accrued when idle. Now you can [utilise low-price T2 instances without being throttled](https://aws.amazon.com/blogs/aws/new-t2-unlimited-going-beyond-the-burst-with-high-performance/) when running out of CPU credits. This could be useful for T2 instances you have for low impact work but where you want just a bit more stability/predictability, e.g. Jenkins worker nodes, Selenium grid nodes, or early-environment databases.


<br />

### Amazon Time Sync

This to me is one of the "how did this not already exist?" type of product launches. [Amazon Time Sync](https://aws.amazon.com/blogs/aws/keeping-time-with-amazon-time-sync-service/) is a service intended to replace NTP servers, and can be used as an NTP source on your EC2 nodes. Configure your node to use [chrony](https://chrony.tuxfamily.org/) instead of ntpd and you're done. The link local IP of 169.254.169.123 can be accessed by any node from within your VPC for time syncing. This service also does leap second smearing, which is a cool way of handling the problems caused by introduction a 61st second into a minute.


<br />

### Inter-region VPC peering

With this much-requested feature you can now connect to other AWS regions (e.g. from Dublin to London) [via Amazon's private backbone](https://aws.amazon.com/about-aws/whats-new/2017/11/announcing-support-for-inter-region-vpc-peering/) links instead of the internet. Previously, the only other options available involved using either a pre-existing corporate backbone or a custom VPN setup. Now AWS has done the work for you, so you can simply enable VPC peering between VPCs in available regions. Currently this is available between N. Virginia/Ohio/Dublin and other regions are "coming soon".

This feature is likely to be of particular interest for customers in the UK currently operating their public cloud workloads from eu-west-1 in Dublin - this may be useful for a transition from Dublin into the London region, or use of the London region as DR site.


<br />

### Amazon MQ

If you like Apache ActiveMQ, and you like not having to actually provision EC2 nodes and enjoy simply treating data stores as services, then Amazon MQ is for you. Amazon MQ is to ActiveMQ what AWS RDS is to setting up and managing your own database server - i.e. it rapidly feels like a mug's game when Amazon will do it for you. Amazon MQ is intended as a drop-in replacement for the self-managed ActiveMQ exchange; provision a queue and provide your AMQP 1.0 compliant apps with the new endpoint and you're done. It supports all the usual things that ActiveMQ supports because it is ActiveMQ, just you don't get to ssh into the host box any more.

Amazon still recommend using SQS for cloud-native apps (and I'd be inclined to agree unless you're wedded to one of the protocols that ActiveMQ supports) so this is intended to make migrating legacy systems simpler, and to take away some of that heavy lifting that ops teams have to do. The managed service nature of Amazon MQ means you don't need to handle queue server upgrades, configuring the service, clustering, failover, backups, etc.

When I heard 'AMQP compliant' I had a brief spark of excitement for the potential to replace RabbitMQ which we've used quite a bit in work, though this ship was dashed on the rocks of _standards_ as RabbitMQ is an AMQP 0-9-1 broker, which is unfortunately very different from AMQP 1.0 (why they didn't just rename the standard is anyone's guess) so sadly there's no easy drop-in replacement option for Rabbit users.


<br />

### Amazon GuardDuty

GuardDuty is a threat detection system designed to run on AWS hardware (i.e. you don't pay for its CPU cycles or suffer the overhead) that will scan your environments and attempt to identify malicious activity. This service combines anomaly detection, known-bad IP addresses and machine learning of account usage patterns. As a result it can be triggered by attackers scanning web apps for vulnerabilities, a compromised EC2 instance starting to run bitcoin mining code, or flag up a set of machines suddenly launched in the night by a user whose geographic location was suddenly different.

GuardDuty can take automatic responses to threats raised (e.g. quarantine offending EC2 node, disable user account with suspicious activity) or simply to alert based on the issues for more manual resolution. This service has a great potential to make ongoing security checking less of an arduous task and more of a background chore that happens continuously - bridging the gap between the world of the seasonal penetration test and the world of the weekly/daily/more frequently deployments from a continuous delivery pipeline of work.


<br />

### Amazon Neptune

Amazon Neptune is a new [graph database as a service](https://aws.amazon.com/blogs/aws/amazon-neptune-a-fully-managed-graph-database-service/) supporting both RDF & SPARQL and TinkerPop3 & Gremlin. Similar to DynamoDB / RDS, multi-AZ deployments, backups, failover, encryption is managed for you. Hooray.

Graph databases have long been a bit of a niche interest, but with a managed service taking the heavy lifting out of the equation it may make it easier for people to consider whether this type of database and access mechanism better suits their highly connected data than just defaulting to an RDBMS.


<br />

### Amazon Aurora

Aurora gets two new major features in the re:Invent announcements. Firstly, for the MySQL-compatibile flavour the ability to run [multi-master deployments](https://aws.amazon.com/about-aws/whats-new/2017/11/sign-up-for-the-preview-of-amazon-aurora-multi-master/) enabling write-accepting master nodes to be deployed in multiple availability zones for even better high availability setups. Multi-master is currently in preview, so you'll need to [sign up](https://pages.awscloud.com/amazon-aurora-multimaster-preview.html) and hold tight for an invite to take advantage for now.

The second new feature is [Aurora Serverless](https://aws.amazon.com/blogs/aws/in-the-works-amazon-aurora-serverless/) for the MySQL-compatible flavour, enabling users to provision an auto-scaling Aurora database without having to specify instance size and only scaling via additional read-replicas. The new serverless model uses a fleet of instances behind a proxy endpoint you treat as the database endpoint, requesting a minimum and maximum capacity. You pay for as much resources as you use, billed per-second. 

In my opinion, this is really the dream of the managed service - instead of concerning yourself with instances and handling scaling yourself, you just press a button and receive database. Aurora Serverless is [currently in preview](https://pages.awscloud.com/amazon-aurora-serverless-preview.html) with MySQL flavour intended for general availability in H1 2018 and Postgres flavour later in the year.


<br />

### Amazon DynamoDB

Amazon DynamoDB is a highly available, high performing managed service for a key store based database. [On-demand backup]() was announced enabling point in time snapshots and restores of running DynamoDB tables without any performance impact. [DynamoDB global tables]() were also announced, a pretty powerful feature for people running in more than one region - automatically managed multi-master multi-region synchronisation and replication allowing a DynamoDB setup to span regions and accept writes in both. If you've got customers in more than one region and are using DynamoDB heavily then this might help you avoid sharding data and dealing with moving people from other to the other if they move.


<br />

### API Gateway

API Gateway is a pretty nifty combination of load balancer, reverse proxy, authentication filter and rate limiter. The major use case so far has been to expose APIs to the internet to the public or other third parties, but with the [announcement of VPC integration for API Gateway](https://aws.amazon.com/about-aws/whats-new/2017/11/amazon-api-gateway-supports-endpoint-integrations-with-private-vpcs/), you can now attach an API Gateway to a VPC instead of just as an internet gateway. This opens the potential use to broker APIs between groups/projects within an organisation, or if connecting via VPC peering to another organisation in AWS, to do so without routing your traffic out via the big bad internet.

Another feature for API Gateway is the ability to do [canary releases](https://aws.amazon.com/about-aws/whats-new/2017/11/amazon-api-gateway-supports-canary-release-deployments/), i.e. deploy changed APIs to a portion of the traffic and monitor the results before rolling out to a greater/full portion when you're happy. This may be useful for people using API Gateway to face services which don't have good support for this themselves.


<br />

### AWS Lambda

Lambda gets a small handful of new features at re:Invent with a [doubling of the maximum memory available](https://aws.amazon.com/about-aws/whats-new/2017/11/aws-lambda-doubles-maximum-memory-capacity-for-lambda-functions/) to individual lambda functions (and therefore a doubling of the allocated CPU behind the scenes) so running lambdas to do particularly beefy computational work should become a bit easier where parallelising the load isn't enough to solve your problems.

[Per-Lambda concurrency limits](https://aws.amazon.com/about-aws/whats-new/2017/11/set-concurrency-limits-on-individual-aws-lambda-functions/) is a small feature but useful to stop individual busy lambdas affecting other parts of the same AWS account when hitting execution limits.

[Traffic shifting deployments](https://aws.amazon.com/about-aws/whats-new/2017/11/aws-lambda-supports-traffic-shifting-and-phased-deployments-with-aws-codedeploy/) also arrive in AWS Lambda (your guess is as good as mine why they didn't name it canary deployments like the API Gateway feature) giving people the ability to do blue/green or canary deploys - but seemingly only if using CodeDeploy for deployments. I suspect this feature is integrated into CodeDeploy partially to help drive adoption of the Code-* tools.

The new feature that I think will be a slow burner is the [Serverless Application Repository](https://aws.amazon.com/blogs/aws/aws-serverless-app-repo/) - a new service that allows you to package and present lambda functions for reuse for others in your organisation, or the public. This one, if the industry pays it the attention I think it deserves, may prove to be pivotal in reducing the waste inherent in developing many software systems when writing code that someone else has already written to solve a low level problem not specific to your domain. It also puts me in mind of [a post](https://hackernoon.com/building-a-business-from-a-great-idea-some-future-monday-42ba794fdae5) from [Simon Wardley](https://twitter.com/swardley) along these lines.

Potentially lower level than github libraries, you could then share small bundles that define API Gateway interfaces, DynamoDB tables, and Lambda functions that are triggered by API actions or S3 uploads, so long as they conform to the [Serverless Application Model](https://github.com/awslabs/serverless-application-model) (SAM). There's no mention [yet] of how this could be monetised but that would be an interesting angle to go in the future if Amazon would give you a tiny slice of the run cost charged to those bundles as a developer fee.


<br />

### AWS AppSync

AWS [AppSync is a new service](https://aws.amazon.com/appsync/) designed to make it easy to create GraphQL APIs and have them run as a managed service, with a client library provided to handle backend connection, authorisation, caching for offline operation and synchronising when online. The GraphQL API will then back onto a DynamoDB table, ElasticSearch database or an AWS Lambda function. There are client libaries provided for iOS, React JS and React Native and also [sample applications](https://aws.amazon.com/appsync/resources/) for each flavour. This one may prove very popular with mobile devs, taking the heavy lifting out of creating your backend services and especially in enabling the offline use and handling conflict resolution.


<br />

### AWS Cloud9

Cloud9 was an in-browser IDE that got bought by AWS about in 2015 and has since [relaunched as a tightly integrated AWS feature](https://aws.amazon.com/about-aws/whats-new/2017/11/introducing-aws-cloud9/). I had a Cloud9 account a few years ago but didn't really use it much, so it'll be interesting to see how it has changed after being brought into the Amazon stable. It has multi-language support, various themes, code completion, all the normal things you'd expect from an IDE. Where it shines is the integration to AWS features, like being able to debug running Lambda functions. Having the ability to live collaborate with others, stepping from source control/pull request into a file and sharing with someone else in your AWS organisation seems like it would really help remote pair programming and discussion of code in code reviews.


<br />

### Internet of Things

We all love the Internet of Things, don't we? _remotely turns all lights in the house blue to annoy wife_ Inevitably it has moved from buzzword material to generally accepted term for "devices that aren't computers but are on the internet". The [cynical amongst us](http://willhamill.com/2016/02/16/internet-of-things-or-your-property-as-a-service) might prefix that sentence with "insecure" too, and indeed avoiding fridges, cameras, baby monitors and friends from being unwitting botnet participants is going to be a bigger and bigger deal. Many more applications are emerging with the maturity of the devices, the additional services for management and monitoring, the tighter integration with cloud services and critically the application of security to the devices and to their interaction with fleets.

A large number of IoT services were announced at 2017's re:Invent, to help people roll out, manage and learn from their fleets of connected devices and to take yet more of the undifferentiated heavy lifting away for you. I'll only touch on these briefly as I've not much experience with the AWS IoT platform:

* [IoT Device Management](https://aws.amazon.com/blogs/aws/aws-iot-device-management/) - register, search through, update and remotely manage your fleets of IoT devices.
* [IoT Analytics](https://aws.amazon.com/blogs/aws/launch-presenting-aws-iot-analytics/) - this preview managed service collects stats from your IoT fleet in a time-series DB allowing you to transform and query on the data.
* [IoT Device Defender](https://aws.amazon.com/blogs/aws/in-the-works-aws-sepio-secure-your-iot-fleet/) - similar to AWS GuardDuty, this service monitors your fleet of devices and alerts on suspicious activity. Especially useful given that IoT devices are usually deployed outside the safety of the Enterprise's physical perimeter.
* [IoT 1-click](https://aws.amazon.com/about-aws/whats-new/2017/11/aws-iot-one-click-now-in-preview/) - remember those Amazon Dash buttons? Now you can treat your IoT devices the same way, having them easily invoke AWS lambda functions remotely.
* [Greengrass ML inference](https://aws.amazon.com/about-aws/whats-new/2017/11/aws-greengrass-adds-feature-for-machine-learning-inference/) - this preview service is implemented in the impressive demo device [DeepLens](https://aws.amazon.com/deeplens/) as a means for executing machine learning inferences directly on edge devices running Greengrass rather than having to send the data back to the cloud. Great potential here in enabling easier fast, local data processing.
* [Greengrass new features](https://aws.amazon.com/about-aws/whats-new/2017/11/over-the-air-updates-access-to-local-resources-and-opc-ua-industrial-protocol-adapter-now-available-on-aws-greengrass/) - Greengrass gets a couple of new features, including access to host hardware, OPC-UA messaging support and remote update capability.
* [Amazon RTOS](https://aws.amazon.com/freertos/) - this FreeRTOS-based microcontroller operating system is to FreeRTOS as Amazon Linux is to other distros: it's based on the FreeRTOS kernel and includes a few helpful libraries for connecting to IoT services, encryption, updates and running Greengrass applications.


<br />

### Amazon Sagemaker

One of the biggest announcements at re:Invent is this [managed service designed to bring machine learning to the masses](https://aws.amazon.com/blogs/aws/sagemaker/) rather than those with the money and resources to hire data scientists and build big compute clusters to do training and processing. Amazon Sagemaker takes an incredible amount of undifferentiated heavy lifting away from you so you can focus on tweaking your machine learning model and integrating it into your application.

With Sagemaker, Amazon's managed service provides model hosting, Jupyter notebooks, distributed training, hyperparameter optimisation, and a deployment platform. You can use common pre-tuned algorithms or bring your own custom algorithm. You can run your model on Apache MXNet, TensorFlow or bring your own framework. Sagemaker will scale up a fleet of EC2 nodes to distribute your training. Sagemaker will also deploy your model for inference on auto-scaled EC2 nodes and you pay only for what you use when it is invoked. Taking the massive operations burden away and enabling developers/analysts to get started much more easily with a set of starter projects and predefined training datasets, there is great potential for project oriented R&D work applying custom facial recognition, or fraud detection algorithms, or more, given the lower barrier to entry.

In addition to this, there are a few new machine-learning based services that take every detail concern away and just offer a very high level based service - see below.


<br />

### Amazon Translate

This preview product provides [text translation as a service](https://aws.amazon.com/blogs/aws/introducing-amazon-translate-real-time-text-language-translation/), using machine learning models to better infer context and pick correct translations than simple translation schemes. Currently available to translate to and from English and Arabic, Simplified Chinese, French, German, Spanish, and Portuguese, this service integrates with other AWS services such as Polly, AWS Lambda, S3 or Lex. It could be potentially useful for automatically translating website or guidance content into additional languages if content designers for each target language are not available.


<br />

### Amazon Comprehend

[Natural Language Processing as a service](https://aws.amazon.com/blogs/aws/amazon-comprehend-continuously-trained-natural-language-processing/), Amazon Comprehend aims to take the heavy lifting out of processing text for key topics or sentiment analysis. It can work in realtime for sentiment analysis, and on a batch basis for topic detection.


<br />

### Amazon Rekognition Video and Kinesis Video Streams

Making a logical extension to the existing image based Rekognition service, Rekognition video is a realtime video stream based content processing service capable of custom facial recognition, object detection, pre-trained facial recognition of celebrities and content classification. [Kinesis video streams](https://aws.amazon.com/blogs/aws/amazon-kinesis-video-streams-serverless-video-ingestion-and-storage-for-vision-enabled-apps/) are similar to the now-renamed Kinesis data streams, in that they process a constant stream of video frames, encrypt the content, store it in S3, enabling analytics or machine learning or other custom logic to operate on the data streams. Video streams can also be processed in real-time by Rekognition Video.


<br />

### Amazon Transcribe

This managed service is for speech-to-text processing; feed it an audio file of someone talking and it will return the transcribed text. This one service could be especially useful in conjunction with the other ML services - indeed it's now technically feasible to build your own multi-lingual Alexa. Transcribe to turn the audio into text, Translate to turn the input language into English for processing or another output language, NLP done with Comprehend to pick out key phrases, AWS Lambda to execute functions based on those phrases, and Polly to perform text-to-speech to communicate back to the user in their language.


<br />

### Alexa for Business

Speaking of Alexa (heh, see what I did there?), Amazon also announced a preview of [Alexa for Business](https://aws.amazon.com/blogs/aws/launch-announcing-alexa-for-business-using-amazon-alexas-voice-enabled-devices-for-workplaces/). At last, a personal assistant for those of us who have not yet ascended to the top floor corner offices. Alexa for business promises to be able to start video conferencing calls, add calendar entries, book meetings, look up data in connected systems such as Salesforce or perhaps even shout about monitoring alerts with Splunk. 

Personally I think if Alexa can get the printer to work first time and tell me where the appropriate video dongle is for the presentation screen it'd be worth a zillion gigabucks, but that's why I'm not a CFO. I think this service has great potential and while no doubt there'll be a big delay while traditional enterprises overcome their fears of integration and data security, as we've seen with people's willingness to adopt the Amazon Echo at home, those fears will eventually fall by the wayside as they accept the tradeoff for all the little conveniences that add up to making things better.


<br />

### Amazon DeepLens

Less of a service and more of a device that utilises a number of IoT and machine learning services (Greengrass ML, IoT device manager and Sagemaker are the most obvious candidates), the DeepLens is intended to be a [hardware exemplar and platform for educating developers](https://aws.amazon.com/deeplens/) about serverless IoT machine learning. DeepLens is a small, powerful video camera with dedicated GPU and image processor designed to run machine learning models on video streams in real time locally. Tutorials are created to help you pick from sample projects, train your model with SageMaker, run the resulting ML inference as a lambdas on the device, and send detected events to the cloud. 

DeepLens devices are available to [pre-order from Amazon.com](https://www.amazon.com/AWS-DeepLens-learning-enabled-developers/dp/B075Y3CK37) - though if you're going to order one I recommend picking up a micro HDMI cable too, as their chosen monitor port is a bit esoteric!


<br />

### Amazon S3 Select and Glacier Select

Coming towards the end of the announcements, there's a nifty new feature for S3 object storage and Glacier archive storage that lets you [select subsets of data from S3](https://aws.amazon.com/blogs/aws/s3-glacier-select/) by writing SQL to address the bucket contents and pick out sub-properties of objects instead of retrieving only whole objects. For people using S3 as their data lake, pushing this filtering to the S3 side will undoubtedly speed up and reduce the costs of traversing big datasets and picking out the parts of interest.

It's not really clear to me how this differs from a cut-down version of [Amazon Athena](https://aws.amazon.com/athena) except that it extends as far as querying datasets archived in Glacier, with options to get data back in either minutes or hours (you pay to determine the speed of the person running down to the blu-ray safe and digging out your discs to have them scanned by the query, presumably 😉) and having an SNS notification sent to you when your query results have been dumped into an S3 bucket once they're done. The Glacier Select section of the announcement blog post however mentions that Athena support for Glacier Select is coming in 2018, so when that happens I couldn't really tell you the distinguishing feature this has over Athena, or if it's becoming just an incidental detail of how Athena works.


<br />

### Amazon Sumerian

Finally, Amazon Sumerian is a new service comprising an in-browser IDE, test framework and development toolkit for creating [AR, VR and 3D experiences](https://aws.amazon.com/blogs/aws/launch-presenting-amazon-sumerian/) with Unity-compatible assets. Sumerian is aimed at WebKit for browser, WebVR supporting Oculus Rift, HTC Vive, and ARKit on iOS (ARCore for Android coming soon). Some interesting potential use cases were described, such as VR for training someone on heavy machinery repair before letting them loose in the manufacturing plant, or perhaps AR on phones providing a guide overlay for people who are performing machine repairs. There are many potential uses of this technology outside of gaming, and with this service, Amazon wants to make creating AR/VR content much easier and more prolific and will no doubt help with this genre's push towards mainstream by making the tools a bit more accessible.

<br />

## Wrap-up

If you've gotten this far, come tell me and I'll buy you a drink. Other than that, I would totally recommend re:Invent to anyone with interest in cloud services, technology, or software development. It was a fantastic conference with loads of really interesting tech and really interesting stories from other people at different points in their journey with tech. It's also a small world and I bumped into two different people I knew without planning to meet them, which in a different country and at a conference of that size was uncanny. Thanks again to my employer [Kainos](https://www.kainos.com/careers) who sent me over for both the workshops and main conference.

The content from re:Invent is also all recorded and available for viewing on the [AWS YouTube channel](https://www.youtube.com/user/AmazonWebServices/) so you haven't entirely missed out if you didn't get a chance to go. The sessions cover intro, intermediate and deep-dive levels so there's something for everyone there.



