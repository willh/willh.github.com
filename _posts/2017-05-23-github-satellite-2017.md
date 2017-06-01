---
layout: post
title: "Github Satellite 2017"
description: "Keynote and presentations from the Github Satellite conference in London, the first associated conference spinning off from Github Universe bringing together Github partners, customers and developers on how they collaborate and develop software"
category: 
tags: []
---
{% include JB/setup %}

On Monday 22nd May I attended the [GitHub Satellite](https://githubuniverse.com/satellite/) conference (thanks to my gracious employer [Kainos](https://www.kainos.com)), an event intended to bring different types of GitHub users together to share how they're using GitHub to help them develop and deploy software. The event was a single day of talks followed by a day of workshops. I attended the main day of talks hoping to find some insights into how better to make use of GitHub and improve our development and delivery process.

- [How to avoid creating a Github junkyard](#junkyard)
- [The secret life of monoliths](#monolith)
- [Building interconnected workflows (panel session)](#github-workflow)
- [Modernising software architecture (panel session)](#modernising-architecture)
- [A data driven approach to leading software teams](#expect-what-you-inspect)
- [The story of a growing Women In Tech community in Nottingham](#wit)
- [Innersource to leverage best practices from the OSS community](#innersource)
- [Closing keynote - Git and Github as an educational platform](#closing-keynote)

### Keynote

[Chris Wanstrath](https://twitter.com/defunkt), the CEO and co-founder of GitHub took to the stage to talk about the incredible ecosystem in the centre of which GitHub now finds itself. Based solely on GitHub stats (and we know there are devs who don't use GitHub) there are at least 21 million developers working on 59 million projects, a massive cohort. This ranges from Windows dev using Visual Studio to Linux devs in Vim and Mac devs in Sublime Text - meaning GitHub's target audience needs different ways of using and interacting with GitHub. This has led to the releases of [GitHub for Unity](https://unity.github.com/) and GitHub integration in [Visual Studio](https://visualstudio.github.com/).

Chris talked about how with such a wide userbase, GitHub started to find themselves as a platform for others who wanted to base their work on top of what GitHub does as a code repository. Despite the old GitHub API having a single page of documentation and committing sins such as returning all responses as a HTTP 200 OK even if an error occurred, people were building on it. The REST API hasn't really evolved, and something newer is needed to meet developer needs. Nonetheless, [Travis CI](https://travis-ci.org/) entered beta in 2012 and now GitHub has more traffic to its API than browser driven traffic to its website. 5 million users use GitHub integrations and 60% of teams use more than one integration.

[Kyle Daigle](https://twitter.com/kdaigle), a Senior Engineering Manager came onstage to describe how the [GraphQL API](https://developer.github.com/v4/), originally previewed last year, was now released to full availability. Integrations are now called GitHub Apps and OAuth integration can be more finely grained (for example letting a bot join your team but only giving them certain permissions in a single repo, instead of acting as the installing user).

The big announcement was the [GitHub Marketplace](https://github.com/marketplace), a place for developers to find apps that can extend and enhance their development workflows and applications right inside GitHub. The marketplace is a one-stop shop that lets you add many different services like CI build tools, code review, task tracking and application monitoring to your code repositories and subscribe to paid versions.


### <a id="junkyard"> </a>How to avoid creating a Github junkyard

[Laurie Apple](https://twitter.com/lauritaapplez) Agile PM & OSS Evangelist at [Zalando](https://www.zalando.co.uk/) talked about their approach to open sourcing and managing their code, and their journey through growing and maturing their use of Github and how they now organise themselves better. Laurie described how Zalando was originally quite 'command and control' oriented, and how a pivot in management approach led by a desire to create autonomy, mastery and purpose (from Dan Pink's [Drive](https://www.amazon.co.uk/Drive-Daniel-H-Pink/dp/184767769X/)) shifted to autonomous teams producing their work as open-source first. 

In January 2016 they had 400 repositories of code but didn't have a good way of even finding out what they had, which meant duplication and poor maintenance, varied quality with some repositories having missing documentation and with ignore pull requests. The applications worked but they weren't getting much out of their open source approach because of the disorganisation. There was no overall vision for what they wanted to achieve by open sourcing the work other than just opening it up by default - their Github organisation had become a junkyard for code. Zalando changed this by deciding to ask themselves some questions about how they might improve: _What would we have built if Github charged per repo?, What would our community build if they built it with us?, What would our teams do differently next time?_ and _Why not make those changes now?_

Laurie tells us that it wasn't easy for them to change; managing and maintaining this stuff is hard as handling pull requests has time costs and project pressures led people to cut corners. This was an opportunity to change their working culture at scale, and some parts were faster to change than others. The fast parts were to create guidelines for open sourcing work, templates for issues and pull requests. The slower parts were to shift focus to craftsmanship and to encourage teams to understand the cost and sustainability of opening up their work and interacting with others working on it, while reorganising the actual repositories.

1.5 years on from the junkyard, Laurie reveals that they've consolidated from over 130 repos to 72, each project being more community oriented and some of their work has influenced other companies. They've still got challenges in how they want to improve, such as getting people to respond to pull requests in a timely fashion and in preventing people from thinking that 'pushed to Github' is the same as 'done', and that delivery pressure and busyness are still difficulties. Zalando have rolled out an official internal open sourcing strategy, and as part of that have ended the practice of 'open source by default', asking that teams understand the goal of open sourcing it and have management support for it. Community interaction for projects going open source is now non-negotiable (helping deal with the ignored pull request issue) and training and coaching are provided to teams to help them improve.

Laurie finished by giving some points on how to avoid creating a Github junkyard of your own: clean up now, don't wait; start doing it now if you've got something new; ask why we're doing open source; don't make cleanup your burden, create slack time for improvement and keep things simple; respond to people in the open source community to get interaction and keep the project alive.


### <a id="monolith"> </a>The secret life of monoliths

[Kir Shatrov](https://twitter.com/kirshatrov) at [Shopify](https://www.shopify.co.uk/) talked about how they handle development and deployment on what is most likely the world's oldest [Ruby on Rails](http://rubyonrails.org/) monolith. Shopify's app originated around 2005 and now contains around 500 controllers with 500+ developers working on the same codebase. One of the things they've done to improve how this works is to make investments in tooling, and as such they have a dev infrastructure team. They seek to automate and provide tools to help developers get and stay productive in this large app, such as a smooth dev setup experience for new starts. The startup script in a readme file has been replaced with a vagrant VM and automated setup, but still has high VM overheads.

To support the development teams, the dev infrastructure team set up a dev survey, revealing that the local environment was the biggest complaint from developers. The vagrant VM was replaced with a lightweight virtualised container called [Xhyve](https://github.com/mist64/xhyve) which suited the developers' Macs, and the various setup and build scripts were replaced with a single `dev up` command to take some of the pain out of build and dependency management.

One of the other problems with this big codebase was code organisation, so the application was rearranged into components, e.g. billing or auth or notifications, each component having its own root folder and contributor list in the main application repo. The dev infrastructure team also implemented a way of people subscribing to notifications for changes they were interested in within the codebase. 

With such a large application there was a large test suite, and continuous integration was a problem. 70,000 tests provided a long feedback loop during a build so this was tackled by pushing integration testing to the cloud, with 200 test runners picking tests to run from a work queue to parallelise the test load. Shipping changes to production was automated by integration with Github to adding test results to the pull requests along with a button to add the feature to a merge queue for production deployment. Prod deployment can be blocked when an issue in the live environment occurs, and chatbots integrate with Github to inform devs who merge what to keep an eye on during the time their change is under deployment (e.g. links to monitoring dashboard).

Kir described how the dependency upgrades for the monolith are particularly hard, usually following a cycle of branch -> change dependency -> run tests -> merge, which to track down and update all the uses of a dependency requiring upgrade can take as long as several months. The strategy taken to ensure code can hit production sooner than this is to wrap code in the application with checks for which version it is running under, and branch inside the codebase into an older piece of code for the older library (not dissimilar to [feature toggles](https://martinfowler.com/articles/feature-toggles.html), methinks). Despite the ugliness it causes until the old dependency has been eliminated entirely, it gives a way to progress to production with the new code, then using a gradual rollout of the application across deploy target machines in production as a way to validate the functionality with real users.


### <a id="github-workflow"> </a>Building interconnected workflows (panel session)

This panel session was used as a way for a number of SaaS vendors whose tools integrate directly with Github to describe how their tools work, how they plug in and how they can be used to improve and speed up the development process. This included [Andrew Homeyer](https://twitter.com/andrewhomeyer) from [waffle.io](https://waffle.io/) who provide automated project management based on Github Issues, [Danielle Tomlinson](https://twitter.com/dantoml) from [CircleCI](https://circleci.com/) who provide continuous integration services, [Jamie Jorge](https://twitter.com/jaimefjorge) from [Codacy](https://www.codacy.com/) who provide a code review platform integrating with Github pull requests, and [Cory Virok](https://twitter.com/coryvirok) from [Rollbar](https://rollbar.com/) a SaaS monitoring and analytics platform.

The session started with each representative getting a chance to describe why developers love their tool, then into an example application development scenario for enhancements being added to a bookshop website, using waffle.io to manage the tasks, CircleCI to do build and integration, Codacy for code reviews of the new features and Rollbar for the monitoring and client side error capture. It was a decent showcase for not only how these tools can work together, but how for simple projects and app startups it's possible to take your application idea almost entirely to production just from inside of Github.

Waffle.io used an integration to automatically update pull requests with work tracking info, the build gets kicked off in CircleCI and build status is added to the pull request, Codacy collects code review comments and static analysis feedback such as coding style, test coverage and complexity and injects these too into the pull request for the new feature, then once deployed Rollbar can detect a client side issue and automatically create a Github issue with details about the error and related info like original developers and commit dates. Once the issue is fixed by acceptance of a pull request in Github (presumably after another CircleCI build with code review from Codacy and all tracked in waffle.io) then Rollbar can automatically close the issue and even contact end users to inform them that their issue has been fixed.


### <a id="modernising-architecture"> </a>Modernising software architecture (panel session)

After lunch, a panel of Github's enterprise customers discussed how they use Github to help deliver an architecture that meets their business and user needs. The panel featured [Cyril Lakech](https://twitter.com/cyril_lakech) from [Axa France](https://www.axa.fr/), [Thomas Jansen](https://twitter.com/thojansen) from [SAP](https://www.sap.com), [Lothar Schulz](https://www.lotharschulz.info/) from [Zalando](https://www.zalando.co.uk/) and [Erik Ammerlaan](https://twitter.com/eammerlaan) from [https://www.exact.com](Exact).

My notes for this session are a bit long to rewrite in prose so I've included them here as I took them during the session.

What does Modernising Software Architecture mean to you?

* Erik - business requirements to working software, how everything works together to achieve that goal, modernisation important and speed important to get ideas to production, outcome is to validate idea with working software as quickly as possible
* Lothar - want quick feedback cycles, want to check improvement as soon as possible. Non functional and legal and operational requirements need to be included
* Cyril - interoperability important, need to be able to change which systems we integrate with, other companies need to be able to integrate into your platform and add their own business features, want to evolve quickly, need supported by C level in company 
* Thomas - processes to support cloud, to empower teams, how do we develop software fast in responsible model like devops but still meet compliance needs

How has the day job of people in your teams changed and how will it change?

* Cyril - code review for pull request is mandatory, also we want to reuse code and assets between teams, adding a lot more automation and moving to devops approach
* Lothar - app  life cycle is planning, developing, deploying, retiring. Coming from a monolith, taking steps towards micro services, we have lots of APIs so need to put effort into understanding how we design APIs consistently 
* Erik - different flows between people working on monolith and those working in microservices, formal code reviews, QA engineer tests it, another person merges it then big regression test before deploy. Looking into microservices and running one year pilot focused on Github with pull request reviews and integrations. 

You seem to need a cultural shift when modernising, how do you handle that?

* Thomas - bottom up with use of Github, identify things that work well and share lessons learned, in a big company lots of different options for ways to do something but also classical change control for major software. Measure success by talking to teams, monitor team outputs.
* Cyril - measure the customer satisfaction, with culture change start small. When you choose a tool there is a mindset behind the tool. When you adopt Github people get message we are trying to be more open and organised. Need to show people open but still secure, so include review for that.
* Erik - measure it with employee engagement using developer surveys, propose options for dev tools and see how that affects the different answers. Started small with Github then others asking when they can get in the scheme.

How do you ensure your app is secure while fostering environment of collaboration?

* Lothar - check if those guidelines are really needed, identify which ones are important and try to include in developer workflow. Automation and tooling to help comply with policies, if dev doesn't even know about it then that helps.
* Cyril - code reviews help catch security issues, more eyes. Still have manual security test.
* Erik - also use SonarQube scanning for security warnings.

How do you use Github in your company and what is the impact?

* Lothar - Github is the go to place for code but also now the place for documentation or explanations, internal projects tend to link to other Github pages. Github helps with visualisation of build status, merge status, deploy statuses.
* Erik - pull request can help document how the system was built when docs, even designs are included.
* Cyril - Github helps share assets across the global company. Beyond code can store dev guidelines and similar.

What do you see coming into your work in the future?

* Thomas - bots and chat ops, like from Github themselves.
* Lothar - serverless and cluster management solutions. Lambdas just do what you want and manage no infrastructure. Machine learning is really interesting so we're trying to see what customers want.


### <a id="expect-what-you-inspect"> </a>A data driven approach to leading software teams

[John Witchel](https://twitter.com/johnwitchel) from [GitPrime](https://www.gitprime.com/) gave a talk on how to get better insights into issues and productivity in your development team by extracting statistic from Github. The purpose of GitPrime is to find better ways of measuring developer productivity, remove interruptions from the team caused by asking for status updates, and to rank the development team in terms of coding output.

John described how GitPrime can index all of the commits in your git repository in order to extract details about the numbers of lines of code written, in which place in the app they were written, and identify not just total lines of code output by a person on the team but also things like whether they were 'churning' a lot (i.e. rewriting their own code after a short space of time) or if a committer is 'high risk' due to commiting significantly fewer lines of code than the rest of the team or working on pull requests that have been open for unduly lengthy periods of time. 

It can also be used to build a picture of a developer's contribution beyond lines of code by tracing their comments on other people's pull requests to show taking part in review, or if someone has been reworking a piece of code for a long period of time outside of R&D/investigation work that might indicate they need support or a change of approach. Work changing during development (an irritating reality for many of us) can also be tracked by compiling statistics on 'ticket jitter' which identifies when an issue in Github used for allocating work has been changed since the developer was assigned, as this would indicate rework may be caused by late changes or moving goalposts.

**Note:** Normally I don't editorialise the content from conference sessions that much but for this talk I feel obligated to point out that I think this entire exercise which is fundamentally intended to stack rank developers based on lines of code written, is hugely toxic and not only causes problems in perception of appropriate ways of valuing contribution but also acts to solve the symptom of problems that should be addressed at their root cause.

I found that the features described in this software seek to create a competitive environment by literally stacking developers up in a graph of code contributions, and supposedly allow a manager to avoid interrupting the team and asking everyone if they are okay by just focusing in on the developers who aren't performing okay, "because nobody is going to tell you they're not okay when you ask them". I personally feel like if this was being used in my work it would be a strong indicator of a culture of micromanagement and that if you need to dig into stats like this to tell where people need help then you haven't created an environment where people can be honest about their progress and when they need support. It also comes with a number of caveats about additional information you can feed into the system to account for disparities in expected work like sickness, holidays, team members joining, and even if you can add more of these things like percentages of time for senior developers to pair with junior developers (when the committer would only 'earn' the stats and the other person in the pair would not), it seems like making up for the fact that fundamentally counting lines of code for productivity is simply a measure of work and not a measure of value, and that perverse incentives can be created.

I also noticed that in the talk, a strongly male-dominated bro-culture type of environment was described, such as a senior person who spends more time commenting on reviews than other team members "usually the 'alpha dog' should be doing more heavy lifting like they were hired to do". Every example of an underperforming team member during the talk had a female name, like "Kathryn is doing a lot of rewrites and has a lot of churn" and "we've got a PR open for 5 months there. Maybe let Samantha go, I dunno, heh" and also "Erika is causing the ticket jitter and the release is going to go badly and it's probably Erika's fault". I think perhaps this goes unnoticed to most men but maybe if I was a woman in the audience I'd have been aware of the fact that all people representing my gender are being depicted as the problem in the team. Perhaps it was just a coincidence that these examples had female names but it struck me as a strange coincidence in that case. Being more aware of depicting more diverse teams and ensuring that positive representation is made would go some way towards improving the impression that our industry creates.

In summary, while GitPrime seems to be a superficially interesting way to get a better view of how your team is performing, I would not want to use this product in any team where the people in the team are to be treated as highly trained and educated professionals with complex motivations and whose value as a team member is not as easily measured as total lines of code committed.


### <a id="wit"> </a>The story of a growing Women In Tech community in Nottingham

In this talk, [Amy Dickens](https://twitter.com/redroxprojects) the lead organiser of the [Inspire Women In Tech](https://twitter.com/inspireWIT) conference spoke about the experience of creating a community for WIT in Nottingham as a way of helping improve diversity in the software industry. Amy talked about the importance of recognising our biases, both conscious and unconscious and how showing a positive bias for underrepresented people in presentations and engagement in the community can create important role models for those groups. Amy explained how the diversity that it's important we enable should be reflective of all aspects of personality: cognitive diversity as well as race, gender, ability, orientation and so on.

One of the ways that we can improve inclusivity in an industry which has around 20% females in technical roles is to remove gendered labels from job roles. I've also found it useful in the past to run the entire job description through a [service that checks for subtly gendered language](http://gender-decoder.katmatfield.com/) to help make things more accessible. Amy explained how creating the WIT Nottingham group and conference aimed to inspire women to take up careers in tech by presenting role models and giving people access to workshops on everything from git to python.

Amy suggested a few other points to make events more inclusive such as creating ambassadors, calling out negative behaviours, providing a pronoun section on conference badges and gender neutral bathrooms, telegraphing to people in advance that your event is intended to be inclusive, and little things like changing language used to avoid subtly excluding groups like saying "hi folks" instead of "hi guys". The use of 'guys' seemingly by default is a pretty pervasive one and something I think should be easy enough to change - pretending like it is gender neutral can be proven absurd when you substitute "ladies" into the same sentence instead. [Limmy](https://www.youtube.com/watch?v=Im3Zj9ZBsyU) also has an amusing take on the matter.

Five takeaways that Amy left us with were:

1. Take the [Harvard implicit bias test](https://implicit.harvard.edu/implicit/user/agg/blindspot/indexgc.htm) to identify your unconscious bias (_I highly recommend this_)
2. Encourage inclusivity by changing the way we communicate - even saying "well, basically" can imply a level of understanding everyone should have that renders a thing basic, that the audience might not yet have
3. Be an ambassador
4. Challenge negative behaviours, for example have a stated Code of Conduct (here is some [help with creating a code of conduct](http://geekfeminism.wikia.com/wiki/Anti-harassment_policy_resources))
5. Be excellent to each other


### <a id="innersource"> </a>Innersource to leverage best practices from the OSS community

[Panna Pavangadkar](https://twitter.com/pannasingh) from [Bloomberg Tech](https://www.techatbloomberg.com/) gave a talk on [Innersource](https://en.wikipedia.org/wiki/Inner_source): using open source software practices to develop software within an enterprise and opening source code up to the whole company. Panna described how Bloomberg's own journey through Innersouce has improved collaboration and reuse across the business but how it's often difficult to maintain and treat each project as if it really has an open source community that depend on it (which it might).

Bloomberg originally introduced Innersource to their organisation by explaining the concept, identifying early adopters who could help push the practices, and engaging at all levels from individual contributors up to senior management in order to get support: the CIO sponsored the activity in spirit by making a statement that this was a thing worth trying. Change in the technical organisation was difficult, and org structure and culture of pride in code made some reluctant to open up their work, so this was tackled by insisting that new work had to be public-first.

Panna described how it was difficult at times to ensure people didn't ignore pull requests, so they needed time set aside to tend to their own communities, and they would advertise in org-public repositories for 'help wanted' to find contributors who could make needed improvements, using merge acceptance criteria to make clear the 'rules of engagement' such as code review guidelines, code coverage expectations and so on. Roles and responsibilities needed clarified in the teams because time management was still a difficulty - people were not getting the time they needed to do coaching or to review pull requests in open repositories, so 10-20% of time was spent on 'skunkworks' projects.

Panna also talked about how they used tooling and integration with Github to open up repositories to expose useful things or work that needed done, and used hackathons to generate ideas that challenge the status quo and encourage collaboration on existing projects. Many of the tools used by Bloomberg internally once started life as a stretch project, started by getting funding for cross-functional work using shared infrastructure and then showing that there is value in letting people address the issues they see as causing pain. The things that Panna summarised as most important to getting started with Innersource were starting with early adopters, finding evangelists and getting senior sponsorship.


### <a id="closing-keynote"> </a>Closing keynote - Git and Github as an educational platform

[Marc Scott](https://twitter.com/coding2learn) from the [Raspberry Pi Foundation](https://www.raspberrypi.org) gave a closing talk about how Github can be used as a platform to help educate and to bring more people into technology. Marc talked a bit about his background as a teacher and then getting into education technology and his experience with helping making tech more accessible to kids (and everyone). The work done by the Raspberry Pi Foundation really is exceptional in democratising the access to technology by making something so simple yet extensible, and fundamentally so incredibly affordable.

Marc implored the audience to see how getting into tech gives kids an avenue to employment and prosperity, and that early on there are fewer preconceptions of tech being 'geeky' or 'nerdy': 90% of children speak positively about coding and 89% of parents think that learning it is worthwhile for their children but only 12% of parents know where to find resources, and also sadly only 50% of teachers do not feel confident at teaching basic computing.

Marc mentioned the [Raspberry Pi learning section](https://www.raspberrypi.org/resources/learn/) which aims to provide helpful, accessible tutorials to people who are trying to get into different aspects of tech, and which [you can contribute](https://github.com/raspberrypilearning) to by adding new sections, reviewing pull requests and addressing issues. Marc closed by talking about [Code Club](https://www.codeclub.org.uk/) and how access to these coding clubs is improving access to learning about tech for children across the country and exhorting the audience to [get involved and volunteer](https://www.codeclub.org.uk/start-a-club/volunteers).

