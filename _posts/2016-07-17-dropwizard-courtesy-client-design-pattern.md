---
layout: post
title: "Courtesy Client design pattern for web services"
description: "Enable reuse of common client code across microservices by publishing a courtesy client for your service for other applications to use. Includes sample application for Dropwizard services written in Java."
category: 
tags: []
---
{% include JB/setup %}

Having spent the last few years developing web services mostly with [Dropwizard](http://dropwizard.github.io) I find it to be a great balance of just the right libraries I really do need to implement a decent web service without the opinions or magic of bigger frameworks.

Writing lots of services in Dropwizard often means you end up writing lots of web service clients for other applications to consume those services, and at [Kainos](https://www.kainos.com/careers/vacancies/) we have developed what we call the 'Courtesy Client' pattern for reusing client code across other services to save time writing another identical set of HTTP client methods but without being coupled to the service implementation.

This post is illustrated by a [sample-service](GITHUB-LINK-HERE) [Dropwizard 0.9.3](http://www.dropwizard.io/0.9.3/docs/getting-started.html) project which when run will give you a basic working RESTful web service demonstrating this pattern.

The sample-service is built using [Gradle](https://gradle.org/) and consists of a three subproject structure with jars produced for API, service and client:

![Sample Dropwizard service with published client pattern](../../../../assets/images/20160717_sample_service.png)

<br /><br />  

#### The API subproject

API project used to define request & response objects for the HTTP interface. The classes are Jackson-annotated and where necessary [Swagger-annotated](https://github.com/swagger-api/swagger-core/wiki/Annotations-1.5.X).  The API project produces a jar file used to share the request & response objects between the client and service, so that the client does not depend on the service.

<br />


#### The service subproject

The service project is produces the jar file used to deploy and run the application. The service project is the core of the web service, hosting the HTTP server and processing responses. The service project depends on API – it takes the request objects and serves up response objects to meet the interface. The service project hides its implementation and internal domain objects from clients. See the [sample project](LINK-TO-SAMPLE-SERVICE-SRC-FOLDER) and how the `Person` class is defined only in the service project and mapped to the `PersonResponse` class to be used in the HTTP interface.

_Only_ the service project integration tests depend on the client project – this ensures that any breaking change to the API that was made by the service but not implemented in the client would cause tests to fail, as this represents a change to the contract for downstream consumers. Outside of the integration test code, the service project does not depend on the client project to run.

<br />


#### The client subproject

The client project depends on API – it implements a HTTP client used to call the interface in the service and as creates request objects for use with service and accepts response objects defined by the API project.

The client project is used to integration test the service as a separate consumer, but is also published and versioned as an independent jar as 'courtesy client' for other Java services to reuse.

<br />


#### Downstream services using the Courtesy Client

Other Java services can reuse client methods to avoid re-implementing same HTTP client calls, but are not obligated to use the courtesy client. A responsible service should write a client to use as part of its own interface testing so why not let other teams/projects benefit from the work already invested? Any downstream service wanting to take advantage of the reusable client library can resolve the jar from a shared repository such as a Nexus, and include this in their builds.

No coupling exists to the service from the client – a downstream consumer implementing the client only needs to be updated when the API package is updated and a new version of the client is released: i.e. the HTTP interface has changed. If a new version of the service is released that does not change the interface then this version can be deployed without any downstream consumers updating their clients. This ensures the service can be iterated and deployed separately from downstream consumers which only need to change when the interface has changed, ensuring coupling remains only at the HTTP interface level.

<br />


#### Downstream services not using the Courtesy Client

What if downstream consumers of the service don't want to implement the courtesy client? Perhaps they want to use the Apache HTTP client or implement a caching client instead. No problem, just write your own client and meet the same HTTP interface. Services communicate via the HTTP interface so there is no need to use the courtesy client to talk to the service. It's created out of courtesy!

What if downstream consumers of the service aren't written in Java? Well, as the coupling between the services is just at the HTTP interface level then the service doesn't care how its clients are written. No problem, just implement a client that meets the same HTTP interface as defined in the service's Swagger API documentation.

<br />


#### Using the sample service

The sample service linked can be used as a seed project for Dropwizard web services, and implements a couple of useful aspects.

The service project is a good citizen and [hosts Swagger API documentation](http://swagger.io/) for other clients to inspect and use to test the service. I've found this very useful both for testing the service and also to help produce good quality and up-to-date documentation.

The [HTTP interface endpoints](LINK-TO-PERSON-RESOURCE-CLASS) are annotated with [Metrics](http://metrics.dropwizard.io/3.1.0/getting-started/) so that each request is timed for stats collection.

The sample service also implements a [basic healthcheck](LINK-TO-HEALTHCHECK-CLASS) to facilitate monitoring as any responsible web service should do, which I've [blogged about before](http://willhamill.com/2014/12/04/application-health-checks-with-dropwizard).
