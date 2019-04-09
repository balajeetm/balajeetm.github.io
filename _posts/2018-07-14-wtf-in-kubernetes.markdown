---
layout: post
title: WTF in Kubernetes
date: 2018-07-14 18:16
comments: true
external-url:
categories: Technology
---

>Containers is about as hot as it can get in the IT world right now.<br>
>But containers need management & kubernetes is one of the hottest container management technologies out there. And it has got a future as bright as a million suns put together.<br>
>Not to brag or anything, but in case you didn't know, i'm a **containerholic**, who lives & breathes container. So come let's get cracking and see [WTF](/blog/2017/02/13/welcome-aboard/) in kubernetes

Sorry to be perceptive, but from this point on, I'm assuming you know what a container (aka glorified process) is and how they work. If you don't, I'll churn a blog for that soon. Until then please bear with me and do some self reading.<br>

So buckle up, the world is gonna be your oyster & you can be the batman/batwoman of the tech world.

## Kubernetes Primer - Where, What & Why
Let's start with the DNA of kubernetes (fondly called k8s for the slouches).<br>
```
Where did it come from and what's in the name?
What does it do & why do we have it?
```

### <u>The Where?</u>

Giving a celluloid ring to it,<br>
Kubernetes was spawned from the bowels of [Google](https://www.linkedin.com/company/google/), raising from the most hyper scale data centers of the world, who were doing containers even before containers became a market norm. It however came off age in 2014 when it was handed over to the [Cloud Native Computing Foundation](https://www.cncf.io/)

Google relied on proprietary solutions such as Brog & Omega for container management. Kubernetes is an organic evolutions of these technologies.
<img src="/assets/2018-07-14/brog_omega_k8s.png">

### <u>What's in the name?</u>

Kubernetes comes from the greek word called **"helmsman"**, which denotes the person who steers the ship.<br>
**Spoilers Alert!!!**<br>
Containers are derived from the shipping industry so you see why they call kubernetes as the one who steers the ship. This is no surprise since the docker & container world is littered with nautical references. Btw, kubernetes was apparently initially called the [Seven of Nine](https://en.wikipedia.org/wiki/Seven_of_Nine), which (if you are not [Star Trek](https://en.wikipedia.org/wiki/Star_Trek) ignorant) is the name of the female Borg. So you see where this is going right?

And Kubernetes is often called K8S, with the number 8 replacing the eight characters (surprise) between the K and the S; brilliant for lazy typers.

### <u>What and Why?</u>

* **Madness of Scale**<br>
Containers make our old challenges with scale pretty laughable. However, if a legacy app had hundreds of VMs, there are chances that the modernized VMs would have thousands of containers (and I'm not even starting microservices here). And if you wish to manage this madness, say hello to Kubernetes.

* **Pet vs Cattle**<br>
Gone are the days where we named our servers. In the brave new k8s world, all we need to say is - "Hi K8s, here I have an app, run it for me please.".<br>
We do not care where it runs. The servers today are faceless character less workers

* **Platform Agnostic**<br>
Its cool with baremetal, VMs, openstack, anything.<br>
K8S let's you focus on deployments


## Kubernetes Architecture

### <u>Big Picture View</u>

Let's begin with a big picture view, say 40000 feet.
At the highest level, K8S is an orchestrator for microservice apps that run on containers

Let's try an analogy. 
* Players
Any team is made up of multiple players with different skills & abilities & each player has a different role to play in the team.
* Coach
And the along comes the coach who gives every player a position and organizes them into a unit which transforms the collection of players into a beautiful formation as below.<br>
The Coach also makes sure the team is in tip top condition by subbing off injured players.

<img src="/assets/2018-07-14/team_formation.png">

Microservice Apps in the K8S world are just like this.

* App
We start out with an app made up of multiple services, each packaged as a pod (the unit) & each one got a job within the overall app. They are like the players.
<img src="/assets/2018-07-14/app.png">
* K8S
K8S is like the coach in the analogy & organizes things so that they work together on the right network, with the right secrets and what we end up with is an useful app made up of smaller moving parts
<img src="/assets/2018-07-14/orchestrated.png">

We call what K8S does as "Orchestration" - where it orchestrates all the individual pieces to work together

### <u>The Components</u>

K8S is made up of one or more "masters" & a bunch of workers or "minions"

* Masters
The masters are in charge & make the decision about which minions to run work on.<br>
The bits & bobs that run on the master make up the **"Cluster Control Plane"**. It includes all the nuances that monitors the clusters, makes the changes, schedules the work & responds to events.

* Minions
These workers run the actual work. They report back to the masters & watch for changes

<img src="/assets/2018-07-14/master_minion.png">

### <u>The Deployment</u>

Moving beyond the infrastructure, how do we packaged up the application and give it to the cluster?<br>
The simple way to do that is via a K8S deployment. Once we containerise the app, we define it in a object called deployment.<br>
Deployment is just a manifest that tells K8S how should app look like - what images, ports, replica, etc. in a file.<br>
The master looks at the file and deploys the app on the cluster and everything holds hands & sings ["Kum ba yah"](https://en.wikipedia.org/wiki/Kumbaya)

<img src="/assets/2018-07-14/deployed.png">

## <u>Are you not entertained?</u>

<img src="/assets/2018-07-14/not_entertained.png">

So, are you enlightened? Do you feel all bright?<br>
Well, don't stare for too long, or you might end up with a sunburn.

Let's go a little deeper with the [Masters & Minions](/blog/2018/07/15/k8s-masters-minions/) in our next post.
