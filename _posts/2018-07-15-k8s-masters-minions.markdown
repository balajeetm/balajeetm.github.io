---
layout: post
title: K8S - Masters & Minions
date: 2018-07-15 18:00
comments: true
external-url:
categories: Technology
---

>A kubernetes cluster is effectively a bunch of master & minions<br>
>Well, we need something to run these on, but it is not opinionated on what the underlying infra is. Let's delve a little deeper into them.

So the kubernetes cluster runs on any underlying infrastructure. It doesn't care. It could be bare metal, VMs, cloud instances, openstack, its just not bothered as long as it is linux.

<img src="/assets/2018-07-15/infra.png">

## Teach Me - My Master
A master is actually a bunch of moving parts & in most common set ups, they all run on a single server.<br>
But multi master HA is the way to go. We could even get into a distributed control plane in the near future. Mostly though, it is a bit of a monolith.

<img src="/assets/2018-07-15/multi-master.png">

Its also a general practice to keep the master free of user workloads. So the apps are run on the nodes & keep the master free for "baby-sitting". It just keeps things clean & simple

<img src="/assets/2018-07-15/master-minion.png">

Let's drill in a bit & start peeling the labels off

### <u>Api Server</u>
The api server is the front end into the master or the control plane. In fact it is the only master components that clients would be interacting with and the only one with a proper external facing interface.<br>
And like all good things these days, it exposes its external interface via restful apis and consumes a json.

What that means on lay man terms is that
* We send in our manifest files which declare the state of our app like a record of intent
* Master validates it & attempts to deploy it on the cluster

### <u>Cluster Store</u>
If the api serves as the brain of the cluster, then the cluster store is its memory as the state of the cluster gets persistently stored here.
K8S currently uses [etcd](https://coreos.com/etcd/) as its store which is battle hardened already.

For those who are unaware, Etcd is an opensource distributed key value store developed by CoreOS.<br>
It is distributed & consistent.

It is important to note, etcd is the source of truth for the cluster. Meaning, no etcd, no K8s cluster.

### <u>Controller Manager (kube-controller)</u>

This is the king of kings, the controller of controllers. It could very well be a bit of a monolith.<br>
Currently, this component implements a few features & functions which could very well be split out to multiple services. There are a bunch of controllers
* Node Controller
* Endpoints Controller
* Namespace Controller
* Bah, there is practically a controller for everything

They all sit in a loop & watch for changes; the aim of the game being to make sure the current state of cluster matches the desired state.

### <u>Scheduler (kube-scheduler)</u>
It watches for new pods and assigns them to minions. Might sound trivial but it has a ton of things to think about
* affinity/anti-affinity
* constraints
* resource management

### <u>Winding up</u>
In short, the master is the brains of the K8S. Commands and queries come into the api server via the kubectl utility (or other sdk libs), further to which a bit of chatter goes on between other master components & eventually commands & action items make their way to the minions

<img src="/assets/2018-07-15/components.png">

## Thou art my Minion

Kubernetes is way over on the cattle side on the pets v cattle battle. And cattle is all about worker nodes being these faceless, characterless drones that we don't really care about and that we can swap out without even noticing.<br>
That's what is a minion is. This unimportant faceless figure that does what the master says, and if the minion fails or dies, we swap it out & its business as usual.

Anyway, let's take a closer look.

They are much simpler than the master. There only 3 things that we care
* kubelet
* container runtime
* kube proxy

### <u>Kubelet</u>
The kubelet is the main kubernetes agent on the node. In fact it is synonymous to the node/minion.<br>
It performs the below
* It registers the node as a minion to the k8s cluster
* It watches the api server on the master for work assignments
* It carries out the task
* Maintains a reporting channel back to the master

### <u>Container Runtime</u>
The kubelet works with pods which are basic unit of deployment in K8S.<br>
Since the pod is made up of containers packaged together and deployed as single unit, the kubelet needs to work with the container runtime to do all the container management
* Pulling images
* Starting & stopping container

For most parts, the container runtime is docker, but [rkt](https://coreos.com/rkt/) is also very much on the scene.

### <u>Kubeproxy</u>
The last piece of the puzzle is kube-proxy. This is like the network brains of the minion.<br>
* IP Addressing<br>
  For one thing it makes sure every pod gets its own unique ip.
* Load Balancing<br>
  The proxy also does light weight load balancing via a service.<br>
  A Service is a way of hiding multiple pods behind a single network address.

<img src="/assets/2018-07-15/minion.png">

So you have made it !!! Well done !!!
You are no longer a kubernetes noob anymore. Cya until next time.<br>
Shout me out on twitter if you need anything, until then

<img src="/assets/2018-07-15/keepcalm.png">
