---
layout: post
title: "Taking a look at Cloudflare Workers"
description: "Cloudflare Workers is a new serverless code execution platform based on the open source V8 Javascript engine, running Javascript functions with very precise billing and automating global distribution."
category: 
tags: ["serverless"]
---
{% include JB/setup %}


Towards the end of last year, [Cloudflare announced a new platform](https://blog.cloudflare.com/introducing-cloudflare-workers/) for serverless computing they're calling Workers based on running Javascript functions in V8 isolates. You can have a play about with the request/response model in a [sandbox environment](https://cloudflareworkers.com).

[V8 isolates](https://v8docs.nodesource.com/node-10.6/d5/dda/classv8_1_1_isolate.html) are instances of the open source V8 JavaScript engine (featured in Google Chrome) used as the execution platform for Cloudflare workers. Your Javascript function code is injected into a V8 isolate, executed using the Service Worker API, and then halts after returning its result. Only the Javascript language is supported, though anything that compiles to Javascript could be used if the unit of deployment is still the resulting JS code.

Like many other serverless computing platforms, Cloudflare workers are oriented around providing an event-based trigger in the form of a HTTP request, manipulating the data in the request and returning an HTTP response based on that data. During the execution your JS code can do more or less anything that a standard Service Worker can do, including making additional HTTP requests to other resources, or perform some calculations and return the response itself.

Compared to the three main cloud providers serverless platforms- [Azure Cloud Functions](https://azure.microsoft.com/en-gb/services/functions/), [Google Cloud Platform Functions](https://cloud.google.com/functions/) and function-as-a-service pioneers [AWS Lambda](https://aws.amazon.com/lambda/), Cloudflare workers has some subtle and some significant differences:
<br />
<br />

|Platform|Language Support|Max runtime|Event sources|Free allowance|Cost|Regional/Global|
|-------------|------------------||--------------|-----------------------|----|--------------------------|
|AWS|Javascript, Java, Go, Python, .Net Core, Ruby, [BYO Language](https://aws.amazon.com/blogs/aws/new-for-aws-lambda-use-any-programming-language-and-share-common-components/)|15 mins|HTTP request, storage event, [etc](https://docs.aws.amazon.com/lambda/latest/dg/invoking-lambda-function.html)|1M reqs, 400,000 GB-s per month| $0.20 per 1M reqs, $0.00001667 per GB-s|Single-region zone-agnostic*|
|Azure|Javascript, Java, Python, .Net Core|5 mins|HTTP request, storage event, [etc](https://azure.microsoft.com/en-gb/services/functions/) |1M reqs, 400,000 GB-s per month|$0.20 per 1M reqs, $0.000016 per GB-s|single-region|
|GCP|Javascript, Python, Go|5 mins|HTTP request, storage event, [etc](https://cloud.google.com/functions/features/)|2M reqs, 400,000 GB-s per month|$ 0.40 per 1M reqs, $0.0000025 per GB-s|single-region|
|Cloudflare|Javascript only|15 seconds|HTTP request|10M reqs|$0.50 per 1M reqs, ["from $5/month"](https://www.cloudflare.com/en-gb/plans/)|automatic global deployment|

<br />

*AWS Lambda@Edge also enables execution of Lambda functions at AWS' 45+ points of presence via the Cloudfront edge network, but has additional costs and a slightly different deployment model.  
<br />

At a broad stroke, Cloudflare Workers seems like a cut down version of the other platforms available today, but the main differentiators that I can see are in the details:

- Lower cost due to precise billing
  - Workers costs are only incurred while they are executing and consuming CPU resources - if they are waiting on network I/O then they do not incur cost. This is likely because while your worker function is in this wait state it can be pre-empted and the resources used by other functions. You pay, as a result, only for the time you're using up CPU cycles and not for the lifetime of the container that runs your function. Worker max execution time being so low is then less of an issue if you're not actually billed or running while waiting on async calls.
- Automatic global distribution
  - Cloudflare run a homogenous network infrastructure with each server in their 150+ global network running the same set of applications and hosting the same content. This means that your function is deployed once to each one of the edge nodes, rather than having to pick a region or zone in which to localise your execution power. The obvious advantage here is that customers in New Zealand will hit the NZ-hosted version of your function while customers in Ireland hit the Ireland-hosted version, vastly improving latency.
- No 'cold start' penalty
  - Due to the lightweight size of the Worker, and using the V8 isolate model rather than having to instantiate a new container to execute your function, your function is in the worst case just loaded from package definition on disk into an execution thread in V8, which takes around 50ms. Cold start times for serverless functions on the other main platforms are [an order of magnitude (or two!) higher](https://mikhail.io/2018/08/serverless-cold-start-war/) than this, meaning first user and modulo-Nth users will hit a cold start delay when scaling up under load (where N is the number of requests that the platform decides is sufficient to saturate a single function-executing container and creates a new one for the next concurrent request).

<br />

#### Security Model

Cloudflare admit that they are necessarily relying quite heavily on the security features of the V8 engine to ensure isolates are, well, isolated from each other and can't interfere with execution or inappropriately share memory with other functions executing in other threads in the same process. This obviously means you don't have the same depth in defence of the layers of isolation that come with running your function in a different process in a different container, like cgroups, namespaces and the various other operating system level protections that apply in a hypervised or container-based environment. These protections apply to the V8 engine running on Cloudflare's infrastructure, but not between threads within it.

Some mitigations that Cloudflare have in place against Spectre-like vulnerabilities between isolates in V8 which rely on timing and side-channel attacks are:

- No rendering or shared resources
  - No image or DOM rendering means there are fewer ways to implicitly time execution of other parts of the system.
  Your function cannot spawn threads of its own or access shared memory between functions.
- Time stops at the start of the function
  - Calling the Date API to get the current time will always return the same result, so for the duration of your maximum 50ms of execution then time has stopped. This obviously prevents people creating a start and stop timestamp and checking the elapsed duration. For people who want to create timestamps in their functions, as being 50ms out is probably not a dealbreaker.

Cloudflare also benefit from the fact that the V8 engine is subject to Google's own testing, and community interest as a popular open source project, and this which improves the transparency and mitigation of defects that are caught and fixed after the fact. One point made at the recent Serverless London meetup was that anyone using a 0-day vulnerability to exploit Cloudflare's Workers infrastructure and gets caught essentially gives up their 0-day in V8 and their [potential $15k bug bounty](https://www.google.com/about/appsecurity/chrome-rewards/index.html#rewards).

 I would argue, however, that a 0-day bug in V8 is now more valuable than also pwning a lot of desktops given it can be potentially used for targeting adversaries who run in the cloud - even if Cloudflare catches you and reports the bug themselves afterwards. Perhaps they should offer a bug bounty on top of that now that V8 is the basis of their execution platform.

<br />

#### Final Thoughts

For me, Cloudflare workers are a very interesting implementation of a serverless code execution platform. It will be good to see how Cloudflare progress in making local I/O type extensions to their platform so that people can use it for almost everything else a Lambda or Function can do. Additionally, with support for WebAssembly this will allow other languages to be transpiled and executed inside the V8 isolates to bring wider language support to Cloudflare workers.

The cost difference in focusing on very precise billing is attractive, but I don't think that for many people this yet would be enough to drive them from any of the other platforms - it feels like splitting hairs on a handful of dollars per month vs a smaller handful of dollars per month, compared to self-managed virtual infrastructure at many times this amount. However, as the idea of financial accounting objectives for function development grows this may start to become more of a big deal, and I imagine that this will in turn pressure other providers to move to a similar very precise billing model.

Security is still something you'll need to put a bit of trust in Cloudflare to completely assuage your fears, with their sandboxing secret sauce, though it will be interesting to see how this evolves over the next year.

If Cloudflare can invest a bit more in extending the dev tools/patterns side of things to make Cloudflare workers as easy to develop, emulate locally, deploy and version etc as we have with competing platforms then they could start to gain some traction.
