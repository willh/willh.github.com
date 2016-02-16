---
layout: post
title: "Application Health Checks with DropWizard"
description: "Manage microservice components and enhance monitoring by using DropWizard health checks to report on the health of your applications."
category: 
tags: ["dropwizard", "monitoring", "microservice", "service oriented architecture", "REST"]
---
{% include JB/setup %}


I’ve been using [DropWizard](https://dropwizard.github.io) for about two years now and find its small set of libraries very useful in creating small self-contained services. It contains just enough components that are intrinsic to almost all web API based services without over-egging it: HTTP servlet, HTTP client, JSON, config serialisation, basic validation, metrics, and health checks. Any time I play around looking at alternatives for small services like [Spark](http://sparkjava.com/) or [Spray](http://spray.io/), I find that I’ll end up implementing these few valuable things that DropWizard consistently gives me for free. 

Of particular interest to me is that DropWizard provides health checks and encourages all services to implement them as a means of providing HTTP endpoints that other systems can use to monitoring the status of the application that you are creating.

If you are creating a service-oriented or more distributed application (especially as [micro services](http://martinfowler.com/articles/microservices.html) becomes more popular an approach) then considering the needs of choreographing and monitoring the application, determining the health of any given component is very important. If you know the downstream system you’re going to call it’s alive then you can avoid calling it and present reduced features to caller or user, or perhaps take an alternate system flow, or trigger some alert. Knowing that parts of your system are down or not working is really helpful.

### Health check basics

DropWizard's standard health checks are implemented by extending the `HealthCheck` base class and returning `healthy` in the happy case and `unhealthy` in the sad case. The most basic example would be to just return a healthy result so long as the app is up.

    public class AppHealthCheck extends HealthCheck {

        public AppHealthCheck() {
            super("sample-app");
        }

        @Override
        protected Result check() throws Exception {        
            return Result.healthy();
        }
    }

This health check will be registered with the main application class environment inside the run method like so:

    environment.healthChecks().register(“sample-app", new AppHealthCheck());

DropWizard will kindly expose it as a HTTP resource endpoint on `/healthcheck` on the admin port (defaults to normal port++). DropWizard also includes a check for deadlocks by default along with any custom health checks you define. In this case, the health check will simply return a result of healthy when it can be called correctly:

    $ curl -i localhost:8701/healthcheck
    HTTP/1.1 200 OK
    Date: Tue, 02 Dec 2014 23:20:00 GMT
    Cache-Control: must-revalidate,no-cache,no-store
    Content-Type: text/plain;charset=ISO-8859-1
    Content-Length: 32

    * deadlocks: OK
    * sample-app: OK

This can be called by something as basic as curl, or something fancier like [Nagios](http://www.nagios.org/) or another monitoring tool. Talk to your friendly neighbourhood Ops Person to find out what monitoring and alerting is used in your system platform.

This will at least tell us that by trying to call this endpoint, if we get a 200 response then the service is running and everything in between is connected enough for us to talk to it.

### Health check yourself before you wreck yourself

However while useful to know, just returning “I’m alive” isn’t always as useful as finding out if the service you are creating can actually carry out its own main responsibilities.

Now we’ll add to our health checks to represent the service’s critical dependencies: one for a downstream system and one for the service’s database. This will allow us to extend our monitoring just a little, without trying to become too intelligent. We’ll add a new health check and also modify the original.

    public class DatabaseHealthCheck extends HealthCheck {
        private final Database database;

        public DatabaseHealthCheck(Database database) {
            super(“database”);
            this.database = database;
        }

        @Override
        protected Result check() throws Exception {
            if (database.isConnected()) {
                return Result.healthy();
            } else {
                return Result.unhealthy("Cannot connect to " + database.getUrl());
            }
        }
    }

Above example lovingly nicked from the [DropWizard docs](https://dropwizard.github.io/dropwizard/manual/core.html#health-checks)

    public class DownstreamClientHealthCheck extends HealthCheck {

        private final Client downstreamClient;
        private final DownstreamConfig config;

        public SampleHealthCheck(Client client, DownstreamConfig config) {
            super(“downstream-client");
            this.downstreamClient = downstreamClient;
            this.config = config;
        }

        @Override
        protected Result check() throws Exception {
            try {
                downstreamClient.resource(config.getStatusUrl()).get(String.class);
            } catch (UniformInterfaceException e) {
                return Result.unhealthy(e);
            }
            return Result.healthy();
        }

    }

Registering these health checks with the environment in the same way as the first one will show this result when hitting the health check endpoint:

    $ curl -i localhost:8701/healthcheck
    HTTP/1.1 200 OK
    Date: Tue, 02 Dec 2014 23:25:00 GMT
    Cache-Control: must-revalidate,no-cache,no-store
    Content-Type: text/plain;charset=ISO-8859-1
    Content-Length: 54

    * deadlocks: OK
    * downstream-client: OK
    * database: OK

### Extending the pattern

The DropWizard documentation will get you this far, but we’ve found it useful to extend this pattern a little when we’re managing a system composed of multiple DropWizard applications which call each other and expose health checks to each other.

It’s easy at this point to go a bit mad with checking other components, and build up a big chain of dependencies of health checks calling each other, but keeping it very simple will allow us to determine just that this service can communicate with its dependencies in some way: talk to the database and make calls to the downstream system.

We just call an ultra-basic “I’m alive” endpoint with `config.getStatusUrl` in the downstream client example, without calling its health check to avoid this issue.

We’ll implement this endpoint at `/status` on all of our applications like so:

    @Path("/status")
    public class AppStatusResource {

        @GET
        @Produces(MediaType.TEXT_PLAIN)
        public String getStatus() {
            return “downstream app is up";
        }
    }

Implementing this very basic resource gives us the ability to verify that the sample app or any other that relies on this component can call this endpoint (and no more), which for the sample app is enough to inform us that the downstream client can do its job. It’d maybe be nice to also return the current app version and the application name from this `/status` endpoint, but only do it if it’s actually valuable to you. Keep it simple.

Anything beyond this in complexity should be handled by health checks on those components themselves, so for that reason we don’t just call the downstream system’s health check, because that would build up the chain. We don't want our application to fail its own health check if some other application can’t call its own database, we just want to know if our configuration and connections are sufficient to call it. We can leave the handling of that the other application’s failures to the monitoring of the other application’s health checks!
