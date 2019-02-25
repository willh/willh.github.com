---
layout: post
title: "Mapping Technical Decisions"
description: "Using Wardley Maps to help make better technical decisions, and decomposing the problem to make better use of maps"
category: 
tags: ["wardley maps"]
---
{% include JB/setup %}


Using Wardley Maps helps focus decision making on sources of differentiation and value, enabling identification of commodity and general-purpose components

Breaking up problems into composable sub-problems is one of the core skills of the software engineer or architect, and doing this can help identify where to make different decisions

### Example

As part of developing a service you realise users are going to have to register for an account with your service
This involves providing an email address and some personal details and an address (perhaps for shipping)
You need to build a web application to capture this data, which user research suggests should use a postcode -> address lookup
>>> Value chain of components to meet this need
_Normally_ you would correctly identify the solution to this problem is a highly commoditised one (almost every single customer facing system seems to solve it) and you would seek to make use of that commodity component. Having heard that you're going to have to build and operate your own postcode -> address lookup service you of course pushed back on the validity of this requirement and ascertained the reason was because of having identified a _legitimate_ and _verified_ use case that means the commodity component doesn't quite meet your needs:
> Previous user research in the organisation has also identified that the organisation needs a way to supply override addresses that aren't available in commodity address lookup services you need to let users self-report newly developed premises and you can't afford to wait the 3 months for the commodity services to receive updates
Now because your need isn't met by the commodity services, you know you're going to have to build your own
>>> Value chain overlaid onto map axes
Building and maintaining the whole address lookup service is a lot of effort and most if it isn't related to your problem domain

#### Turtles all the way down

So split up the components to dig further and identify which sub-components are the custom parts and which are commodity
Let's dive into the custom postcode lookup service
>>> Value chain of components to meet need of postcode lookup
So if we're going to write the whole thing ourselves we need to manage all of these parts
Despite quite a few of them being commodity parts by nature
>>> Map with value chain showing lots of commodity work
Let's isolate the custom components from the commodity components
Write a wrapper service which will hit custom override entries first then farm out to generic service
>>> Map with value chain showing commodity work outsourceable, custom work related to wrapper service and override data

#### General principle

Dig into the components you think you need and for those you think you have to build yourself, consider if you can break up the problem into further problems that you can have another build/buy type decision, so you don't build more non business domain specific work. Yes, you could have built the whole postcode lookup service yourself, no doubt, but you don't _want_ to do that because of the increased operational burden and the time invested in low-value work.

### Future

Werner Vogels stated that the future of development is when you write _only_ business logic [link to YouTube video of re:Invent 2017 keynote]
For each part of the service under development we can use a Wardley Map to help identify when we're writing something that might be already solved elsewhere, even in parts
The smaller, more finely grained the area of design decision, the more likely that someone has already created something for this
We already take this approach when finding third party libraries and services to handle very low-level or specialist pieces of functionality, like HTTP servers or barcode-generation or encryption libraries, but there's an opportunity to be even more skeptical about which parts of the application that we really have to write ourselves - maybe someone else has written a small application that will store images in Amazon S3 and write path and metadata into DynamoDB in a way that saves you the effort in your application which handles photo uploads.
The Serverless Application Repository will help improve discoverability and make more finely-grained applications reusable, taking away more of the leg work for more areas and accelerating development of the valuable components built on top.
Aim is not to just outsource or productise everything; the aim is to spend time and money doing the things we _want to_ do (as a business) and not the things that we _have to_ do just to get those other things done

