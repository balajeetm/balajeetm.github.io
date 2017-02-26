---
layout: post
title: Linked List Reversal in Pockets
date: 2017-02-26 12:40
comments: true
external-url:
categories: T-Nut
---

>Welcome to another stint of [T-Nut](/blog/2017/02/21/technical-nuts/).<br>
This time the knot we are trying to untangle is the one pertaining to a singly linked-list.<br>
The formal problem statement would be as below.<br>

```
Given a singly linked list, reverse its every 'n' nodes
```

## Prelude
===

It was tea time, a platform for imbecile discussions.<br>
Little B was deliberating over a domain change request, pertaining to a typical product shipment scenario.<br>
In their E-Commerce world, once the product is approved for shipment, the process flow is as below<br>

<img style="text-align: center" src="/assets/2017-02-26/chainOfResponsibility.png">

This was implemented as a [chain of responsibility](https://en.wikipedia.org/wiki/Chain-of-responsibility_pattern), with each shipment site representing a handler with two commands.<br>
Updating the status triggers a notification on the customer's device.<br>
Quite often, the handler packaging the item, irrecoverably failed after status update. This lead to a series of corrective status updates which could have been prevented had the status been updated only after a successful item packaging to begin with.<br>

So, the execution of commands at each shipment site was decided to be reversed<br>

That’s trivial. But what was little B pondering about?. A simple swap of  commands was all it demanded.<br>
Well, if you ever knew little B, everything was always more than what meets the eye with him.<br>

He contrived a hypothetical nut which he was trying to crack - a [T-Nut](/blog/2017/02/21/technical-nuts/)<br>
On slight improvisation, he viewed the above chain as a singly linked list. Fair enough!<br>
The challenge he concocted was, to selectively reverse nodes on the linked list. Specifically reverse every "n" node sub groups in the big list where "n" is a variable input.<br>

Interesting huh?<br>
Hop on, let's join Little B in cracking the nut<br>

The sample input and respective outputs expected are below<br>

```
Example:

Input:	1->2->3->4->5->6->NULL and n = 2
Output:	2->1->4->3->6->5->NULL.

Input:	1->2->3->4->5->6->7->8->NULL and n = 3
Output:	3->2->1->6->5->4->8->7->NULL.
```

## The Thought Train
===

We are gonna use the analogy of literally chewing on an unknown nut, to crack this T-Nut.<br>
Being close to reality always helps.<br>

Let's begin<br>

### <u>Step 1 - Chew and Swallow</u>


