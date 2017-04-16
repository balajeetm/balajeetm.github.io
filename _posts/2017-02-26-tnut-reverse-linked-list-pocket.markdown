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
It all started with a typical Little B conundrum, [during tea time](#the-genesis).<br>
The formal problem statement would be as below.<br>

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

## The Thought Train
<hr>

Here's a typical [T-Nut](/blog/2017/02/21/technical-nuts/), let's begin [cracking it](/blog/2017/03/08/cracking-a-tnut/), shall we?<br>
Let's use the [analogy that we just devised](/blog/2017/03/08/cracking-a-tnut/), of chewing on an unknown fruit, to crack it.<br>
Here goes.

## [Step1 - Cull the epicarp](/blog/2017/03/08/cracking-a-tnut/#step-1---cull-the-epicarp)
<hr>

First we need to isolate the problem statement.<br>
But, that's already done for us. Let's re-look at what we have.<br>

* <b><u>The Naïve Problem Statement</u></b><br>
This as I understand is to reverse a linked list with some constraints<br>

* Let me nibble on <b><u>The Buzz Words</u></b> now

<u>Singly Linked List</u><br>
What do I get out of this?<br>
i. Size is unavailable and can be tremendously huge.<br>
ii. An item cannot be accessed based on index/position. I need to get to every item.<br>
iii. The traversal is unidirectional. We cannot move back and forth.<br>

<u>Reverse in blocks of "n"</u><br>
Well, doesn't quite sit pretty in the head, but let me move on. I will let it dawn on me.

## [Step2 - Take the first bite](/blog/2017/03/08/cracking-a-tnut/#step-2---take-the-first-bite)
<hr>

Let's next devise a strategy to solve this.

* <b><u>Visual Representation</u></b><br>
Since I can't think of any similar problem I've solved, let me try something closer to real life.<br>
The first realistic thing that comes to my mind when we say linked list, is a train with bogies.<br>
Let me create a 2D train with bogies representing nodes. The values of the nodes represent the solitary passenger, commuting in them<br>

<img style="text-align: center" src="/assets/2017-02-26/train.png">
	
* <b><u>Analyze input output samples</u></b>
* <b><u>Solve it mentally</u></b><br>
Let's see if I understand the input, output samples<br>

```
Input:
1 -> 2 -> 3 -> 4 -> 5 -> 6 -> NULL, ok a list with 6 elements
And n=2
```

```
Reverse the first two elements
2 -> 1
Reverse the next two
4 -> 3
Finally, Reverse the last two
6 -> 5

Putting them together
2 -> 1 -> 4 -> 3 -> 6 -> 5 -> NULL
```

Alright, feels like now, I can easily guess the output from the input. Time to chew on the bite now.

## [Step3 - Chew and swallow the bite](/blog/2017/03/08/cracking-a-tnut/#step-3---chew-and-swallow-the-bite)
<hr>

Let's next try to transform our strategy into workable logic.

* <b id="edge-case"><u>Identify edge cases</u></b><br>
In the second sample, we have

```
Input:
1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> NULL, ok a list with 8 elements
And n=3
```

```
So let me reverse, group of three elements
3 -> 2 -> 1

6 -> 5 -> 4

8 -> 7

Putting them together
3 -> 2 -> 1 -> 6 -> 5 -> 4 -> 8 -> 7 -> NULL
```

Ok, there is an edge case. If 3 elements are not available, **it should reverse whatever is available.**
That’s a good catch.

Let me try to garnish some logic now

* <b><u>Create a logical flow</u></b><br>
Let me first see how [Mr.Pristine](/blog/2017/03/18/pristine-logical-brain/#who-is-who) went about it<br>
i. He first split the linked list in batches of "n"<br>
ii. He then reversed the sub link list<br>

Let me pen down some workable logic for the same<br>

<u>Splitting a linked list</u><br>
This should be straight forward, I keep moving across the list and pick "n" nodes

<b style="color:red">Markers</b><br>
<b>How do I work on the picked ones?</b><br>
Should I make a copy of them all, or use the existing nodes?<br>
Let me connect back to my visual representation, to try answering that.<br>
		
If I choose to copy, I may end up making a copy of the whole train. I mean that’s freaking bulky and not space effective.<br>
(See? Visualizing helps you understand the inefficiencies sometimes)<br>
<b style="color:red" id="bookmark1"><Bookmark Alert!></b><br>
Keep a bookmark of this please, we'll get back to this soon
		
<u>Reversing a linked list</u><br>
How did [Mr.Pristine](/blog/2017/03/18/pristine-logical-brain/#who-is-who) do that?<br>

Well he went to the last item in each sub-list, and then put the numbers in reverse.<br>
Hey… wait… [WTF](/blog/2017/02/13/welcome-aboard/) in that? How can he do that?<br>
I thought, you cannot traverse back in a singly linked list!!<br>

But for [Mr Pristine](/blog/2017/03/18/pristine-logical-brain/#who-is-who), there is no such thing as a singly linked list. There are no constraints. The cheater just started walking in reverse direction.

As we call out the bluff of [Mr.Pristine](/blog/2017/03/18/pristine-logical-brain/#who-is-who), let's emphasize the constraints for him.<br>
Let's present the problem through our train analogy adding an explicit constraint<br>
Even in train bogies, we can move back and forth, so,<br>
```
'Assume there is a guard standing at the door preventing you from going back.
He will only let you go forward'
```
So we have a physical separation through bogies and we've also ensured unidirectional movement<br>

### <u>Redefined problem statement</u>
With all those analogies, what does reversing now mean?<br>
We need to make sure the passengers in bogies are relocated. And the relocation constraint is reversal in blocks of 'n'.<br>
Quite clear?<br>
So we've redefined the problem, through something that we know very well - A train with bogies.<br>
Let's get moving then. We need to relocate passengers before the train starts!<br>

What would we do in such a scenario?<br>

First, get a [EV](https://en.wikipedia.org/wiki/Electric_vehicle) or a [segway](https://en.wikipedia.org/wiki/Segway_PT).<br>
Pick the 1st bogie passenger, take the EV to the nth bogie and put him there.<br>
Pick the passenger in the nth bogie and get him to the first.<br>
Now pick the passenger in the 2nd bogie and move all the way to (n-1)th bogie.<br>
Repeat the above for all passengers, and<br>
Reset the reversal schedule for every n passengers.<br>

Diagrammatically, the below:<br>
<img style="text-align: center" src="/assets/2017-02-26/brute.png">

Great, let's start hacking some code now.

### Brute Force Approach
Move items one by one, revisiting every item

```java
/* root refers to the root of the singly linked list 
and 'n' the group size of the sub linked list */

/* variable used to traverse every node, we start with the root.*/
SNode node = root;

/* variable used to keep track of the node position
to identify pockets or sublists */
Integer nodeCount = 0;

/* variables used to performing swapping within a pocket of nodes */
Integer pocket = null;
Integer count = 0;

/* Until we reach the end of list */
while (null != node) {
	// pick a pocket of nodes
	if (nodeCount % n == 0) {
		pocket = n;
	}
	if (pocket > 0) {
		count = 1;
		SNode newPos = node;
		while (count % pocket != 0 && newPos.getNext() != null) {
			newPos = newPos.getNext();
			count++;
		}
		swap(node, newPos);

		/* -2 because, 2 nodes are out of the equation
		 * one in front, and one in the end */
		pocket = pocket - 2;
	}
	node = node.getNext();
	nodeCount = nodeCount + 1;
}
```

The swap function, swaps the values of two nodes as below
```java
Integer temp = node1.getData();
node1.setData(node2.getData());
node2.setData(temp);
```

> The full code is available @ my [tnut github page](http://github.balajeetm.com/t-nut/)<br>
For details refer [tnut controller's](http://github.balajeetm.com/t-nut/blob/master/src/main/java/com/balajeetm/tnut/controller/ReverseSinglyLinkedList.java), **"brute"** api.<br>
Feel free to fork/clone the same and run it on your local.<br>
Refer [t-nut repo](http://github.balajeetm.com/t-nut/) for instructions to run.

<b id="retrospect1"><u>Time for Retrospective</u></b>

Kudos, we seem to have got a working solution.<br>
Let see, if we our current strategy is taking us on the right path and if we can optimize.<br>
As I had said [earlier](/blog/2017/03/08/cracking-a-tnut/#step-3---chew-and-swallow-the-bite), retrospection is a critical phase of chewing on our solution.<br>
Let's be critical, shall we?

First, the solution seems to be work. Feel free to try out all cases on the swagger UI.<br>
But look at the code above.<br>
_For every bogie passenger, we keep moving back and forth, and back and forth.
We keep traversing the same list, multiple times. Doesn't seem effective._<br>

Thank God, there is only one passenger per bogie. What would we do if there were more?? We would have to make more trips which is extremely inefficient<br>
Wait a second, let's pull a feather out of that idea. Why don't we pick all "n" passengers in a subgroup at once and relocate them as a whole?<br>
Let's try that next up.

## [Step 4 - Take more bites](/blog/2017/03/08/cracking-a-tnut/#step-4---take-more-bites)
<hr>

During our last retrospective, we realised that our logic wasn't very efficient and there was room for improvisation.<br>
Let's adapt then.<br>

This time, I'll get a bigger EV and keep putting passengers from each bogie, within a subgroup, into my vehicle.<br>
Once passengers from all "n" nodes in the subgroup have been accumulated, I'll start from the last bogie and relocate the passengers in reverse order, i.e, the first bogie passenger in the last and so on.<br>
Come let's try hacking code for this approach<br>

## [Step 5 - Swallow the next bite](/blog/2017/03/08/cracking-a-tnut/#step-5---swallow-the-next-bite)
<hr>

Let's devise a workable logic for the above strategy.<br>
I've to pick "n" passengers in a sub group together, but I cannot start from the last bogie as I stated earlier. That's because I cannot traverse in reverse direction in a singly linked list.<br>
So I'll start from the first bogie but place the passengers in reverse order.<br>
This seems like a typical stack. I'll add the passengers into the stack but pop them out in a [LIFO](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)) manner as in a typical stack.

```java
/* root refers to the root of the singly linked list 
and 'n' the group size of the sub linked list */

/* variable used to identify the current pocket of nodes we are dealing with */
SNode currentRoot = root;
SNode node = root;

/* variable used to keep track of the node position to identify pockets */
Integer nodeCount = 0;

/* stack used to place nodes in appropriate positions */
Stack<Integer> stack = new Stack<>();

/* Until we reach the end of list */
while (null != node) {
	// pick a subgroup
	if (nodeCount % n == 0) {
		relocate(stack, currentRoot, n);
		currentRoot = node;
	}
	stack.push(node.getData());
	node = node.getNext();
	nodeCount = nodeCount + 1;
}
```

The relocate function would be a typical stack pop as below:
```java
Integer count = 1;
while (count!=n) {
	currentRoot.setData(stack.pop());
	currentRoot = currentRoot.getNext();
	count++;
}
```

<b id="retrospect2"><u>Time for Retrospective</u></b><br>

The solution looks pretty neat. But let's critically review it once.<br>
At even the best case, we need to traverse every node in the list twice.<br>
Once, to pick the member from the bogie and again, to put the right member in place.<br>
The time complexity is still O(n) though. The stack atleast made the code neat.<br>
Guess we are getting to the end of this. Let's carefully nibble the remnants.

> The full code is available @ my [tnut github page](http://github.balajeetm.com/t-nut/)<br>
For details refer [tnut controller's](http://github.balajeetm.com/t-nut/blob/master/src/main/java/com/balajeetm/tnut/controller/ReverseSinglyLinkedList.java), **"bruteStack"** api.<br>
Feel free to fork/clone the same and run it on your local.<br>
Refer [t-nut repo](http://github.balajeetm.com/t-nut/) for instructions to run.

## [Step 6 - Optimize the final bites](/blog/2017/03/08/cracking-a-tnut/#step-6---optimize-the-final-bites)
<hr>

Time to see if we've missed something out. Let's check for some opening.<br>
Some edge case, some NPE... something<br>

Oh, the relocation function seems a little botched up.<br>
It seems to be counting till the pocket size "n", but the [typical edge case we identified](#edge-case) earlier would fail in this case.<br>
We would get a index out of bounds exception. Using the counter thus, is not so catchy. Let's try something cheesy.<br>

```java
while (!stack.empty()) {
	currentRoot.setData(stack.pop());
	currentRoot = currentRoot.getNext();
}
```

Alright, that should do. What else?<br>
What about a empty input scenario? This should return an empty array and it seems to work.<br>
What about a pocket size of 1 (n=1)? That should return the input array as is and that also seems to work as well.<br>

Hey, there's another observation.<br>
The logic seems to empty the stack filled in one cycle, only in the subsequent cycle.<br>
Observe how relocate is called, only after the stack is filled. But this means, the last set of 'n' passengers will never be put in place.<br>
Bah!!! Why you ask? That's because we would have reached the end of list. Let's fix that.<br>
We need to call relocate again after the while loop. That does it.<br>

```java
relocate(stack, currentRoot);
```

> The full code is available @ my [tnut github page](http://github.balajeetm.com/t-nut/)<br>
For details refer [tnut controller's](http://github.balajeetm.com/t-nut/blob/master/src/main/java/com/balajeetm/tnut/controller/ReverseSinglyLinkedList.java), **"bruteStack"** api.<br>
Feel free to fork/clone the same and run it on your local.<br>
Refer [t-nut repo](http://github.balajeetm.com/t-nut/) for instructions to run.

## [Step 7 - Perpetual Optimization](/blog/2017/03/08/cracking-a-tnut/#step-7---perpetual-optimization)
<hr>

We are almost done here, aren't we?<br>
But is that the best we could do though?<br>
Let's re-look at our last retrospect.<br>
```
At the best case, we traverse every node twice.
```
That's not nice, is it?<br>
Not at all...<br>

We can argue that the [time complexity](https://en.wikipedia.org/wiki/Time_complexity) is still O(n) but time complexity is just one side of the story. It does give you the proportionality of time taken wrt to input size but does not shed light onto the rate of increase in time taken wrt to input size.<br>
We'll look at time complexity in detail in a later blog post but what I mean is traversing the list twice is any day worse than traversing it once. So there is room for improvement.<br>

Really? Is there room for improvement? We did the best we could do there, didn't we?<br>

<img src="/assets/2017-02-26/dobetter.jpg">

Well, I do not want to take the fun out of the moment. That's all we live for.<br>
We have cracked the [T-Nut](/blog/2017/02/21/technical-nuts/) and we have done great.<br>
All I'm saying is we can do better.<br>

Bask in the glory, enjoy the success and when you are ready to move on and do better, [hop over](/blog/2017/03/12/tnut-reverse-linked-list-pocket-finale/).<br>

Cya [here](/blog/2017/03/12/tnut-reverse-linked-list-pocket-finale/) soon.

> Gentle reminder<br>
All the above tricks and solutions are available in my [tnut github page](http://github.balajeetm.com/t-nut/)<br>
For details refer [tnut controller](http://github.balajeetm.com/t-nut/blob/master/src/main/java/com/balajeetm/tnut/controller/ReverseSinglyLinkedList.java)<br>
Feel free to fork/clone the same and run it on your local.<br>
Refer [t-nut repo](http://github.balajeetm.com/t-nut/) for instructions to run.

## The Genesis
<hr>

>How many of you are excited by [etymology](https://en.wikipedia.org/wiki/Etymology)?<br>
It's always fun to know where things originate from, isn't it?<br>
More often than not, it will be via an expected source or scenario.<br>
Let's hear the anecdote from where this problem emerged.<br>


It was tea time, a platform for imbecile discussions.<br>
As we sat near the window, sipping hot tea and staring into the sunlight, Little B was deliberating over a domain change request, pertaining to a typical product shipment scenario.<br>
In their E-Commerce world, once the product is approved for shipment, the process flow is as below<br>

<img style="text-align: center" src="/assets/2017-02-26/chainOfResponsibility.png">

This was implemented as a [chain of responsibility](https://en.wikipedia.org/wiki/Chain-of-responsibility_pattern), with each shipment site representing a handler with two commands.<br>
Updating the status, triggers a notification on the customer's device.<br>
Quite often, the handler packaging the item, irrecoverably failed after status update. This lead to a series of corrective status updates which could have been prevented had the status been updated only after a successful item packaging to begin with.<br>

So, the execution of commands at each shipment site was decided to be reversed<br>

That’s pretty trivial. Nothing to lost your mind over.<br>
But little B was lost in thought, pondering about something...<br>
Well, if you ever knew little B, things were more than what meets the eye with him.<br>
He sat hands clasped, and looked into the distance, eyes transfixed into the unknown...<br>
As if seeing something, we could not....<br>

That's when he contrived this hypothetical nut.<br>
On slight improvisation of his given change request, he viewed the above chain as a singly linked list.<br>
And boom... he concocted a challenge... to selectively reverse nodes on the linked list. Specifically reverse every "n" node sub groups in the big list where "n" is a variable input.<br>

Interesting huh?<br>
Life's beautiful...<br>

