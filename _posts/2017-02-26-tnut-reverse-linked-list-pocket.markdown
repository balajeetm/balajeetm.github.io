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
<hr>

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
<hr>

We are gonna use the analogy of literally chewing on an unknown nut, to crack this T-Nut.<br>
Being close to reality always helps.<br>

Let's begin<br>

### <u>Step 1 - Chew and Swallow</u>

Before we begin cracking the nut, let's make sure we understand the nut.<br>
Is it a groundnut, peanut or walnut ?<br> 
What's its size, texture, and so on ?<br>
Basically, ask yourself, if you understand the problem.<br>

Before taking subsequent bites, take out a small piece and start to chew on it.<br>
When you chew the initial bite, we generally focus on the aspects of the food that we like.<br>
On the same lines, focus on the aspects of the problem, that you can take away. Mainly,<br> 
* Jot down the <u>naïve problem statement</u> that you can atleast vaguely comprehend
* Extract <u>the buzz words</u> that hit on you

Lets start chewing then, shall we?<br>

<b><u>The Naïve Problem Statement</u></b> - as I understand is to reverse a linked list with a some constraints<br>

Let me nibble on <b><u>The Buzz Words</u></b> now

<u>Singly Linked List</u><br>
What do I get out of this?
* The size is not available out of the box. 
* The size can be tremendously huge
* I cannot access an item based on index/position. I need to get to every item
* The traversal is unidirectional. We cannot move back and forth, it like driving in a one way street

So far so good

<u>Reverse in groups</u><br>
I need to reverse the order of nodes. But reverse them in blocks of "n".<br>
Well, doesn't quite sit pretty in the head, does it? But good, let me move on.

Ok, we've chewed it a bit.<br>
What next? Let's swallow what we chewed<br>
When you generally swallow, you let your relished bite flow through your esophagus, smoothly into the bowels.<br>
Similarly, let get some logic to flow through and help us connect the dots.<br>
You can do this mentally, scribble on paper or start hacking some code.<br>

Lets begin analysing the input and output samples and see if we can catch some rhythm. Catch some logic.<br>
Let your "pristine brain" solve it.<br>

Ok, let's see<br>
Do we understand the input, output samples<br>

```
Input:
1->2->3->4->5->6->NULL, ok a list with 6 elements
And n=2
```

```
Reverse the first two elements
2->1
Reverse the next two
4->3
Finally, Reverse the last two
6->5

Putting them together
6->5->4->3->2->1->NULL
```

In the second sample, we have

```
Input:  1->2->3->4->5->6->7->8->NULL, ok a list with 8 elements
And n=3
```

```
So let me reverse the first three elements
3->2->1

Then, the next three
6->5->4

And then, the last three
8->7

Putting them together
3->2->1->6->5->4->8->7->NULL
```

**Ok, there is an edge case, If 3 elements are not available, it should sort whatever is available.**
That’s a good catch. Let me now put this together

Great… We have chewed and swallowed.
Let us take the next bite.











