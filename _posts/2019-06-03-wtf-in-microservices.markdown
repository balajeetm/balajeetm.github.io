---
layout: post
title: WTF in Microservices
date: 2019-06-03 08:00
comments: true
external-url:
categories: Microservices
---


>In our earlier [post](/blog/2017/03/14/wtf-in-agile/), we saw how and why organizations are taking the stride to Agile methodologies. However, what does it take to thrive in an Agile chaotic environment?<br>
Let's peek into the architectural paradigm shifts that give us the answer.<br>


## The Way Around Chaos
<hr>

Agile in simple terms is a means to improve the cultural velocity of the organization.

<img src="/assets/2019-06-03/velocity-process.png">

It is the only way to succeed in the competitive & unpredictable software economy.<br>
However, it is imperative to cash in on the [two glorious features](/blog/2017/03/14/wtf-in-agile/#the-uniqueness-of-software-engineering) of software engineering, in order to succeed in this sea of change.
*   Low Cost to Change
*   Low Cost to Distribute

But most organizations find it difficult to achieve low cost to change, and why is that so?

## The Problems of the Monolith
<hr>

Enterprises build software, constantly reacting to customer demands. As the software gains popularity, catering to customer expectations turns a beast in itself. With enterprises playing the cat & mouse of innovating quickly to deliver to customer needs, the software in picture continues to grow inorganically as more developer hands are added to keep up the pace.

Unsurprisingly, too many developer cooks soon spoil the broth, and the software gets stuck, mired in the complexity of competing directions, miscommunications, inconsistency & conflict.

This is in the nutshell, the problems of the **"Monolith"**

When we live in that world, instead of software engineering being a rapid cycle of feedback, innovation & delivery, it turns out to be a painfully slow development process sunk in a tug of war of competing concerns.

<img src="/assets/2019-06-03/slow-development.png">

Thus, though the software has grown in size & features overtime, it tends to become extremely brittle which makes it hard to top it up with more features. And so, the cumulative functionality of the software plateaus overtime. And instead of living in the world of express iteration, we live in the world of painfully slow iteration, with limited scope for course correction and thus generating very little value

<img src="/assets/2019-06-03/slow-iteration.png">


## Emergence of Structures
<hr>

Organizations device different ways to overcome these impediments. One such way is to follow standard practices & architectural patterns during development.<br>
This approach gave rise to the era of "Design Pattern" driven development, where in software was architectured to fit in various architectural patterns rather than the other way round. Though the use of these patterns eased communications across different teams, it resulted in some indurated software structures to emerge.

Preferential architecture was prevalent in the industry, thanks to a more subtle yet impactful modus operandi - **Conway's Law**

### <u>Conway's Law</u>

[Conway's Law](https://en.wikipedia.org/wiki/Conway%27s_law) is an adage which states
```
Organizations which design systems are constrained to produce designs 
which are copies of the communication structures of these organizations.
```

Organizations that are spread across regions would have software modules with authors around the globe.
Since these authors/teams must communicate frequently with one another, the software interfaces of these systems would reflect the social boundaries of the organization(s), across which communication is more difficult.

<img src="/assets/2019-06-03/conways.png">

These boundaries operate in silos with self induced software structures.

## Catering to scale
<hr>

As the software caters to more & more users, these siloed software modules scale in isolation.<br>
There is a limit however to how much these softwares can scale up. They must start scaling out now.

These distributed modules tend to interact with one another over yester-defined contracts, not suited for the distributed world. Moreover the module segregation influenced by org protocols cause strong cohesion that cause structures to emerge within. What transpires is a **"Distributed Monolith"** in disguise.

These self inflicted structures reduce the software's flexibility to change & induce a domino effect, causing the software to collapse. 

<img src="/assets/2019-06-03/domino.png">

## Isolation
<hr>

This is a tough nut to crack. The need of hour is isolation. Isolation in Thought, Design & Implementation. Such a thought process gave rise to evolutionary architecture in the form Domain Driven Design (DDD)

### <u>Domain Driven Design</u>

[DDD](https://en.wikipedia.org/wiki/Domain-driven_design) is a software development approach that advocates architecting a system with primary focus on the core domain.

The key aspect of DDD, is using an ubiquitous language to promote isolation of thought. DDD perceives a software system as a set of interacting [bounded contexts](https://martinfowler.com/bliki/BoundedContext.html) over well defined domain boundaries.

Since the system is designed over domain remits, rather than org constraints, every decision is driven by domain benefits, right from data store to technology choices. As change begets change, the isolation in thought process begets isolation in design & implementation. This gives rise to a set of heterogenous systems exchanging domain entities over loosely coupled protocols.

The culmination of this domain driven design is the advent of an architectural style that includes a collection of independently deployable loosely coupled services organized around business capabilities, fondly called [microservices](https://microservices.io/).

The microservice architecture enables the continuous delivery/deployment of large, complex applications. It also enables an organization to evolve its technology stack. Such an isolation ensures faster time to market (TTM) as features can be developed & deployed quickly.

<img src="/assets/2019-06-03/microservices.png">

### <u>Word of Caution</u>

The microservice architecture is not a silver bullet. Thought it is extremely beneficial by promoting faster delivery, it poses several challenges to engineering.

Since the pros outweigh the cons by soundly, in our further posts, we will see how to go about the same. Cya soon.













