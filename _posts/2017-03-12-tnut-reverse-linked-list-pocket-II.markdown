---
layout: post
title: Linked List Reversal in Pockets - II
date: 2017-03-12 23:20
comments: true
external-url:
categories: T-Nut
---


>Welcome to another stint of [T-Nut](/blog/2017/02/21/technical-nuts/).<br>
This time around, we are gathering to add a few end notes to the [orchestra we began earlier](/blog/2017/02/26/tnut-reverse-linked-list-pocket/).<br>
The formal problem statement of the [T-Nut](/blog/2017/02/21/technical-nuts/) we were cracking was as below.<br>

```
Given a singly linked list, reverse its every 'n' nodes
```
```
The sample input and respective outputs expected are as below

Input:	1 -> 2 -> 3 -> 4 -> 5 -> 6 -> NULL and n = 2
Output:	2 -> 1 -> 4 -> 3 -> 6 -> 5 -> NULL.

Input:	1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> NULL and n = 3
Output:	3 -> 2 -> 1 -> 6 -> 5 -> 4 -> 8 -> 7 -> NULL.
```
Sticking to the [allegory we devised](/blog/2017/03/08/cracking-a-tnut/) earlier, we used the analogy of chewing on an unknown fruit to careen towards the [T-Nut](/blog/2017/02/21/technical-nuts) at the centre and guess what? We cracked it as well.<br>

We were on the last leg, retrospecting our solution and winding up, when we chose to evaluate the [Time Complexity](https://en.wikipedia.org/wiki/Time_complexity) of our solution.<br>
This is how our [last retrospect](/blog/2017/02/26/tnut-reverse-linked-list-pocket/#retrospect2) turned out.<br>
```
At the best case, we traverse every node twice.
```
That's not nice, is it?<br>
We can argue that the [time complexity](https://en.wikipedia.org/wiki/Time_complexity) is still O(n) but time complexity is just one side of the story. It does give you the proportionality of time taken wrt to input size but does not shed light onto the rate of increase of time taken wrt to input size.<br>
We'll look at time complexity in detail in a later blog post but its clear that traversing the list twice is any day worse than traversing it once. So there is room for improvement.<br>

I know what you might be thinking now..<br>
**What? That solution seems like the best given the constraints.**<br>
We even optimized the [initial solution](/blog/2017/02/26/tnut-reverse-linked-list-pocket/#step3---chew-and-swallow-the-bite).<br>
How can I do better than that?<br>

Agreed, that we optimized. But what we are asked to do better than that?<br>
Can we? Do you think there is a possibility?<br>

<img src="/assets/2017-03-12/firstWorldProblem.jpg">

## Pick yourself up
<hr>

Well, the chips are down isn't it?<br>
That seems like the best effort, given the constraints huh?<br>

Take it from me... you will be in similar situations, many a times in real life.<br>
It would seem like you gave the best you could, but it's just not good enough.<br>
Think about it…<br>
* A Performance optimization that you spent sleepless nights brooding over, but still not up to the mark.<br>
* A cricket chase which almost gets your team home but ends up just short of the finish line.<br>
How many of you remember Sachin's epics in [Chennai](http://www.espncricinfo.com/ci/engine/current/match/63828.html) and [Hyderabad](http://www.espncricinfo.com/ci/engine/current/match/416240.html)?<br>
* Losing the qualifiers by milliseconds in a 100m sprint?<br>
* Being turned down by your crush<br>
	
Many many different scenarios, but the same same feeling.<br>
<b><i>"That seemed like the best I could ever do... but it just wasn't good enough."</i></b><br>

It would soon get pretty dense, and bring down the morale.<br>
Those are times when I love to remember this awesome quote from [Christopher Nolan's](https://en.wikipedia.org/wiki/Christopher_Nolan) [Batman Trilogy](https://en.wikipedia.org/wiki/The_Dark_Knight_Trilogy)

<img id="why-do-we-fall" src="/assets/2017-03-12/WhyDoWeFall.jpg">

When things get dense and it feels like you have hit a dead end, that is when we need to pivot.<br>
These are times, to let go and look at the problem from a completely different perspective.<br>
And I do understand, letting go is hard.<br>
But there are scenarios out there, where you will not get another chance. [T-Nuts](/blog/2017/02/21/technical-nuts/ certainly don't fall in that category. So harden yourself though these little failures on irrelevant [T-Nuts](/blog/2017/02/21/technical-nuts/).<br>
Frankly, I would take these failures any day compared to some bigger ones out there.

## Redefined Problem Statement
<hr>

Remember what I said [earlier](/blog/2017/03/08/cracking-a-tnut/#necessity-is-the-mother-of-invention) about doing just what is needed?<br>
Never over engineer. Our [earlier solution](/blog/2017/03/08/cracking-a-tnut/#necessity-is-the-mother-of-invention) works perfectly given the constraints.<br>
So when we are asked to optimize the solution, let's first understand the need.<br>
The needs could be similar to the ones stated in my [earlier post](/blog/2017/03/08/cracking-a-tnut/#necessity-is-the-mother-of-invention), i.e the solution does not meet the NFRs. May be the nodes in the list represent tasks to be executed on a customer request. Now if there is a requirement to reverse the order of execution of these tasks, the lesser time we take to reverse the list, the better. Because any delay could manifest into an observable lag for the end user. More so, if the size of the list is enormous.

So given the justification, how do we enhance our solution?

## The Pitfalls
<hr>

To do so, let's forage for any weak-links or pitfalls in our current solution.

Remember our [bookmar alert](/blog/2017/02/26/tnut-reverse-linked-list-pocket/#bookmark1) earlier? Where in, our visual representation, helped identify inefficiencies?<br>
On further introspection, we'll realise that the visual representation is a cause of inefficiency.<br>

Since, we had never seen a similar problem before, the train analogy seemed the best fit.<br>
However, there is big constraint introduced by the train analogy.<br>
Look at both our solutions, [optimized](/blog/2017/02/26/tnut-reverse-linked-list-pocket/#step-5---swallow-the-next-bite) and [non-optimized](/blog/2017/02/26/tnut-reverse-linked-list-pocket/#step3---chew-and-swallow-the-bite).<br>
The bogies are fixed while we keep moving passengers around.<br>
Why did we choose to do so?<br>

_**Why didn't we try moving the bogies or modifying the links?**_<br>
Well because, sticking to the train analogy, the bogie is bulky and moving it around isn't trivial.<br>
And wrt the links, when was the last time we have ever seen someone attaching a bogie to the train or for that matter, detaching it?<br>
<b>Almost never</b><br>

I've seen it in some movies, but that's more like the climax or a critical inflection point in the movie.<br>
So the train analogy forces us to keep bogies fixed because the bogies feel bulky and fixed.

Remember the [bookmark](/blog/2017/02/26/tnut-reverse-linked-list-pocket/#bookmark1) again, we said copying a bogie is bulky but in our solution, we pushed data/passangers to the stack.<br>

Once we take the train analogy out of the way, is there anything apart from the data, that is heavy in the node?<br>
So if you are copying the data, aren't you actually copying the heavyweight of the node... which is literally, the bogie?<br>
Whooo! That's heavy... And also against our fundamental presumption, that copying data is ok because it isn't as heavy as the bogie.<br>

**Important Lesson to learn here**
```
Analogy is not actual
```
An analogy might help us understand a problem better but once we get comfortable, we need to see the problem the way it is, the actual way it really is.<br>
```
Learn to grow out of the analogy.
Spread your wings and fly.
```

## Arise, Awake and Stop not till the goal is reached
<hr>

* <b>A better analogy</b><br>
Guess it's time for us to let go.<br>
I know, we worked so hard on our current solution and strode our way to the goal, but the inefficiencies are apparent now.<br>
It's neither optimal wrt time nor space. We can improvise both [Time](https://en.wikipedia.org/wiki/Time_complexity) and [Space Complexities](http://www.geeksforgeeks.org/g-fact-86/) here.
 
So let's start over. Let's try something different this time to understand a linked list.<br>
Have you heard of the [human dominoes](https://www.youtube.com/watch?v=TE5RdFFgW0w) or the human train like the one below?<br>

<img src="/assets/2017-03-12/humanTrain.png">

This is no different from a singly linked list isn't it? It's in fact more closer to its unidirectional constraint, with no need of additional guards to impose the restriction.<br>
Let's assume, the human train of a large number of humans, say 100, is going in one direction.<br>
Now if I suddenly ask it to move in the opposite direction, what do you think they would do?<br>
Would the first person, move to last position, vice versa and so on...? Will they keep moving around to their designated position?<br>
Just imagine, with 100 people running around, wouldn't it turn out to be a mess?<br>

That would also take really long, won't it?<br>
Instead...<br>
wouldn't it be easier for each person, to flip direction individually? What do you think?<br>

So, what exactly does flipping directions mean?<br>
**It means flipping the link between nodes.**<br>

In this case, we do not make unnecessary copies so the space utilisation is efficient.<br>
That's it. See, with a better analogy, the links turn flexible now.<br>
But remember

```
A train is as valid a linked list as a human dominoes.
So based on the problem statement use the right one.
Learn to grow beyond the analogies.
Spread thy wings! 
```

What more? If you think about it, this is exactly our problem statement as well.<br>

* <b>Time optimisation & the implicit use of stack</b><br>
Next, we need to better the [time complexity](https://en.wikipedia.org/wiki/Time_complexity).<br>
In our optimized version, why did we have to traverse the list twice?<br>
That's because we used a stack. So we had traverse the list once to populate the stack, and again, to relocate the items by popping the stack.<br>

Whenever we use stacks as a core tool in your logic rather than a data structure (like we have done here), remember this

```
There is an implicit stack for use in our programming model.
The "call stack".
```

One efficient way of using the call stack is recursion.<br>
We'll delve into the details of recursion is some other post, but keep this in your mind.<br>

<u>Typical cases of recursion</u><br>
* Usage of stacks as core logic rather than data structures
* Ability to break a problem to the same problem of smaller magnitudes
	
We can satisfy both constraints here. So let's begin and start hacking code.

First let's see, how we can reverse the list by changing links.<br>
Since its a singly linked list, we would need the previous, current and next nodes to reverse the links.

```java
SNode prev = null;
SNode curr = null;
SNode next = null;

curr = root;
/* Until we reach the end of list */
while (null != curr) {
	next = curr.getNext();
	curr.setNext(prev);
	prev = curr;
	curr = next;
}
return prev;
```

Ok, now I can divide the list into sub-lists of size n.<br>
I can reverse each sub-list and attach the original root of the sub-list to the new root of the next sub-list like below.<br>

<img src="/assets/2017-03-12/train.png">

Programmatically,

```java
Integer count = 0;
SNode prev = null;
SNode curr = null;
SNode next = null;

curr = root;
/* Until end of sublist or end of list */
while (count < pocketSize && null != curr) {
	next = curr.getNext();
	curr.setNext(prev);
	prev = curr;
	curr = next;
	count++;
}

/* attach to the root of next sublist */
root.setNext(null == curr ? curr : pocketReverse(curr, pocketSize));
return prev;
```

> All the above tricks and solutions are available in my [tnut github page](http://github.balajeetm.com/t-nut/)<br>
For details refer [tnut controller](http://github.balajeetm.com/t-nut/blob/master/src/main/java/com/balajeetm/tnut/controller/ReverseSinglyLinkedList.java)<br>
Feel free to fork/clone the same and run it on your local.<br>
Refer [t-nut repo](http://github.balajeetm.com/t-nut/) for instructions to run.

So, there is you see...<br>
We did it. A more efficient solution.<br>
With a single traversal.<br>

Let's do a litmus test again.<br>
Empty input pass,<br>
Edge case pass,<br>
And of course better space and time complexity.<br>
Feel free to try them out yourself via the swagger UI. Refer to the [tnut repo](http://github.balajeetm.com/t-nut/) for details.

All it needed was a change in perspective...<br>
A change in the way we have been looking at things for so long.<br>
I wonder how many real world issues would be solved, if people around the globe start doing that.<br>
<b>#Trust... #Faith</b>

## Footnote
<hr>

So we see that our [allegorical strategy](/blog/2017/03/08/cracking-a-tnut/) of chewing on an unknown fruit to crack a [T-Nut](/blog/2017/02/21/technical-nuts/) works perfectly. However, there seems to be too many steps involved.<br>
If we find ourselves in no man's land, cracking a obscure [T-Nut](/blog/2017/02/21/technical-nuts/), with no idea as to how to strike blows, the above [step by step guideline](/blog/2017/03/08/cracking-a-tnut/), makes complete sense. But memorising so many steps is hard and we also want the approach to be free flowing.<br>

One way of doing that, is to have lesser steps in our design. So, like we always do, let's retrospect our current design and simplify our strategy of cracking a T-Nut.

See you soo, via a [simplified guide](/blog/2017/03/09/cracking-tnut-simplified/).<br>
Have fun unjargoning!
