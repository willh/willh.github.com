---
layout: post
title: "The Phoenix Project"
description: "A novel about IT operations, devops and business transformation."
category: 
tags: ["agile", "business", "devops"]
---
{% include JB/setup %}

Last year, a [number](http://twitter.com/petersouter) of [my](http://twitter.com/moomzni) [colleagues](http://twitter.com/kylethompson86) attended the [DevOps Days](http://devopsdays.org/events/2013-london/) conference in London. They were lucky enough to receive free copies of a new book on DevOps, IT operations and business transformation called [The Phoenix Project](http://www.amazon.co.uk/Phoenix-Project-DevOps-Helping-Business-ebook/dp/B00AZRBLHO/) by [Gene Kim](http://twitter.com/realgenekim), [Kevin Behr](http://twitter.com/kevinbehr) and [George Spafford](http://twitter.com/gspaff). After their recommendations and eventually making my way through the to-read list, I picked up a copy on Kindle knowing little else about it than that it was written in the style of a novel.

After I found [The Goal](http://www.amazon.co.uk/The-Goal-Process-Ongoing-Improvement-ebook/dp/B002LHRM2O/) very easy to read in novel style and also having enjoyed [Commitment](http://willhamill.com/2013/06/12/fear-of-commitment-you-need-options), I was interested. The format is very similar - the business problems and context are revealed through the eyes of the main character 'Bill' who suddenly has responsibility for improving how the IT organisation produces valuable change for the business, and the approaches to identifying and implementing solutions are hinted at by the Advisor Character 'Erik' and discovered by Bill as he endeavours to transform the way work is done.

Many of the other characters follow tropes that will be predictable to some and grimly familiar to others - the manager who cares only about his own deadlines, the egocentric executive, the irreplaceable tech genius omni-required bottleneck engineer, the eccentric and frustratingly vague advisor. The strong, admirable male characters: Protagonist, CEO and Advisor are all inexplicably ex-military too.

### Surprisingly Up-to-date

Perhaps it's because I've read The Goal somewhat recently and I'm joining the W. Edwards Deming party late that I'm surprised that this book is full of up-to-the-minute reference to other modern books on good IT management and development practices. It feels like I'm somehow in on it when Erik quotes [Kanban](http://www.amazon.co.uk/Kanban-David-J-Anderson/dp/0984521402/) by [David J Anderson](http://twitter.com/lkuceo) and I've read the book. 

For example, in order to visualise work-in-progress and track the flow of work to one of the constraints of the system (a lead developer with a very low [Bus Factor](http://en.wikipedia.org/wiki/Bus_factor)), Bill [implements a Kanban system](http://willhamill.com/2013/11/21/implementing-kanban) to manage his tasks. 

Interestingly the word 'agile' is used in only one place in the entire book and I wonder if that's to imply that an agile software development process is so obvious as to go unsaid, though it is clear from terminology such as 'two week sprint' that the teams are using some kind of agile method! 

I've put together at the end of this blog post a list of references to other books that I can find the characters discussing. They're all definitely worth checking out.

### Knowledge Work Isn't Unknowable

I keep reading in places that some people consider the application of flow-management techniques or other abstract methods to the detailed knowledge and discovery based work of Software Engineering to be inappropriate. I can't help feeling that while on the micro level they'd be right, on the macro level it seems to 'average out' and become a useful abstraction again. It's not useful to have people arguing over the exact hours-spent difference between two 2 point user stories but the notion of managing the flow of work items into a team using typical lean approaches does work in practice.

Personally I think that it's acceptable to treat the flow of work similarly between Dev and Ops as it is in managing a traditional work centre based plant so long as this does not distract from the reality that the people involved in each step of the process are still people. Go ahead, map value streams and abstract over the low level details but fundamentally when you need to change things you still have to illustrate the need and inspire people to action rather than treating them as bothersome machines that refuse to be changed. 

When difficulties happen or things go wrong and we have variation within the process and things don't fit into our graphs, we have to remember that inside the system are talented professionals doing their best with what they are given and we need to eschew the abstract approach for the humanistic. Individuals and interactions over processes and tools, [as it were](http://agilemanifesto.org).

### The Three Ways

In The Phoenix Project, Bill discovers The Three Ways - a trio of principles used to improve the relationship between Dev and Ops, and to improve the processes used to control the throughput of work throughout the organisation. The First Way describes Systems Thinking: Bill grows to realise that in order to meet the business' objectives and produce valuable change faster, local optimisation of the operations group or development group may come at the expense of optimisation of the whole system. The best way to have positive impact is to take a whole-system view. 

This in my mind ties back into avoiding optimising for local maxima as described by Deming, Anderson, the Poppendiecks and others. Competition between departments kills co-operation and it is absurd to accept a situation where one group can 'win' when the other group 'fails' - the entire business must either win or fail and responsibility for considering how your process affects others must expand upwards to take this into account.

The Second Way as used by Bill is to implement feedback loops. Bill fairly rapidly starts having retrospective meetings after deployment issues, sets up deployment and incident drills to learn from practiced responses and solicits feedback from both the developers and operations staff on the ground as well as the managers of the business departments his work impacts upon. This is a core agile principle and the [fifth core practice in Kanban](http://willhamill.com/2013/11/20/kanban-beyond-the-board/) and also corresponds to the Plan-Do-Check-Adjust cycle described by Deming/Shewart for continuous improvement.

The Third Way is creating a culture that promotes both mastery of the current process through repetition (for example, repeatedly doing and documenting deployments until they become less unknown and risky) and continual experimentation (taking small risks in an attempt to learn new things to improve the process). In Bill's case, pushing the IT organisation from quarterly releases to multiple releases per day focuses on the repetition and also ties in to the concepts mentioned by Jez Humble & David Farley in their book Continuous Delivery when they say that the best way to become good at something that is risky and painful is to embrace the pain and reduce the risk by doing it more often and forcing yourself to learn how to do that more effectively - through automation.

### Summary

Overall I found that The Phoenix Project was an enjoyable and interesting read and I'm glad that it coherently brings together the many associated facets of modern management and IT practices. In my head it seems more clearly that fundamentally all of the things I've read on agile development, lean, Kanban, Theory of Constraints, Deming's System of Profound Knowledge and even [motivation](http://www.amazon.co.uk/Drive-Surprising-Truth-About-Motivates/dp/184767769X/) are all facets of the same concept of making people work more effectively. A good start to my 2014 to-read list!

#### Materials Referenced in The Phoenix Project

[The Goal:](http://www.amazon.co.uk/The-Goal-Process-Ongoing-Improvement-ebook/dp/B002LHRM2O/) A Process of Ongoing Improvement by Eliyahu Goldratt  
[The Five Dysfunctions of a Team](http://www.amazon.co.uk/The-Five-Dysfunctions-Team-Leadership/dp/0787960756/) by Patrick Lencioni  
[Continuous Delivery](http://www.amazon.co.uk/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912/) by Jes Humble and David Farley  
[Kanban](http://www.amazon.co.uk/Kanban-David-J-Anderson/dp/0984521402/) by David J Anderson  
[10 Deploys Per Day at Flickr](http://www.slideshare.net/jallspaw/10-deploys-per-day-dev-and-ops-cooperation-at-flickr) by John Allspaw  
[Toyota Kata:](http://www.amazon.com/Toyota-Kata-Managing-Improvement-Adaptiveness/dp/0071635238) Managing People for Improvement, Adaptiveness and Superior Results by Mike Rother  
