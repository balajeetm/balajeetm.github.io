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
```
The sample input and respective outputs expected are as below

Input:	1 -> 2 -> 3 -> 4 -> 5 -> 6 -> NULL and n = 2
Output:	2 -> 1 -> 4 -> 3 -> 6 -> 5 -> NULL.

Input:	1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> NULL and n = 3
Output:	3 -> 2 -> 1 -> 6 -> 5 -> 4 -> 8 -> 7 -> NULL.
```

## The Thought Train
<hr>

Let's begin [cracking the T-Nut](/blog/2017/03/08/cracking-a-tnut/), shall we?
Like always, we are gonna use the analogy of chewing on an unknown fruit, to crack this [T-Nut](/blog/2017/02/21/technical-nuts/).<br>
Let's follow this [step by step guide](/blog/2017/03/09/thumbrules-to-crack-a-tnut/) as we do so.

## [Step1 - Isolate the epicarp](/blog/2017/03/08/cracking-a-tnut/#step-1---isolate-the-epicarp)
<hr>

The epicarp is already culled for us. Let's re-look at the problem statement<br>

* <b><u>The Naïve Problem Statement</u></b><br>
This as I understand is to reverse a linked list with some constraints<br>

* Let me nibble on <b><u>The Buzz Words</u></b> now

<u>Singly Linked List</u><br>
What do I get out of this?<br>
i. Size is unavailable and can be tremendously huge<br>
ii. An item cannot be accessed based on index/position. I need to get to every item<br>
iii. The traversal is unidirectional. We cannot move back and forth.<br>

<u>Reverse in blocks of "n"</u><br>
Well, doesn't quite sit pretty in the head, but let me move on. I will let it dawn on me.

## [Step2 - Take the first bite](/blog/2017/03/08/cracking-a-tnut/#step-2---take-the-first-bite)
<hr>

* <b><u>Visual Representation</u></b><br>
Since I can't think of any similar problem I've solved, let me try something closer to real life.<br>
The first realistic thing that comes to my mind when you say linked list, is a train with bogies.<br>
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

## [Step3 - Chew and swallow the bite](http://blog.balajeetm.com/blog/2017/03/08/cracking-a-tnut/#step-3---chew-and-swallow-the-bite)
<hr>

* <b><u>Identify edge cases</u></b><br>
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
Let me first see how Mr.Pristine went about it<br>
i. He first split the linked list in batches of "n"<br>
ii. He then reversed the sub link list<br>

Let me pen down a logic flow for the same<br>

<u>Splitting a linked list</u><br>
This should be straight forward, I keep moving across the list and pick "n" nodes

<b style="color:red">Markers</b><br>
<b>How do I work on the picked ones?</b><br>
Should I make a copy of them all, or use the existing nodes?<br>
Let me connect back to my visual representation, to try answering that.<br>
		
If I choose to copy, I may end up making a copy of the whole train. I mean that’s freaking bulky and not space effective.<br>
(See? Visualizing helps you understand the inefficiencies sometimes)<br>
<b style="color:red" id="bookmark1"><Bookmark Alert!></b> Keep a bookmark of this please, we'll get back to this soon
		
<u>Reversing a linked list</u><br>
How did Mr.Pristine do that?<br>

Well he went to the last item in each sub-list, and then put the numbers in reverse.<br>
Hey… wait… WTF in that? How can he do that?<br>
I thought, you cannot traverse back in a singly linked list!!<br>

But for Mr Pristine, there is no such thing as a singly linked list. There are no constraints. The cheater just started walking in reverse direction.

As we call out the bluff of Mr.Pristine, let's emphasize the constraints for him.<br>
Let's present the problem through our train analogy adding an explicit constraint<br>
Even in train bogies, we can move back and forth, so,<br>
'Assume there is a guard standing at the door preventing you from going back. He will only let you go forward'<br>
So we have a physical separation through bogies and we've also ensured unidirectional movement<br>

### <u>Redefined problem statement</u>
With all those analogies, what does reversing now mean?<br>
We need to make sure the passengers in bogies are relocated. And the relocation constraint is reversal in blocks of 'n'.<br>
Quite clear? Let's get moving then. We need to relocate passengers before the train starts!<br>

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

/* variable used to traverse every node */
SNode node = root;

/* variable used to keep track of the node position to identify pockets */
Integer nodeCount = 0;

/* variables used to performing swapping within a pocket of nodes */
Integer pocket = null;
Integer count = 0;

while (null != node) {
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

> For more details refer the code @ my [tnut repo](http://github.balajeetm.com/t-nut/blob/master/src/main/java/com/balajeetm/tnut/controller/ReverseSinglyLinkedList.java)<br>
Feel free to fork/clone the same and run it on your local.<br>
Refer [t-nut repo](http://github.balajeetm.com/t-nut/) for more details.

<b id="retrospect1"><u>Time for Retrospective</u></b>

I had said [earlier](http://blog.balajeetm.com/blog/2017/03/08/cracking-a-tnut/#step-3---chew-and-swallow-the-bite), that retrospection is a critical phase of chewing on our solution.<br>
Let see, if we our current strategy is taking us on the right path and if we can optimize.<br>
Let's be critical, shall we?

First, the solution seems to be work. Feel free to try out all cases on the swagger UI.<br>
But look the code above, for every bogie passenger, we keep moving back and forth, and back and forth.<br>
We keep traversing the same list, multiple times. Doesn't seem effective.<br>

Thank God, there is only one passenger per bogie. If there were more... what would we do??<br>
Wait a second, that's exactly what we would do. Why don't we pick all n passengers/bogie in a group at once?<br>
Let's try that next up.

## [Step 4 - Take more bites](http://blog.balajeetm.com/blog/2017/03/08/cracking-a-tnut/#step-4---take-more-bites)
<hr>

During our last retrospective, we realised that our logic wasn't very efficient and there was room for improvisation.<br>
Let's adapt.<br>

This time, I'll get a bigger EV and keep putting passengers from each bogie into my vehicle like in a stack.<br>
Once all 'n' passengers have been accumulated, I'll start again from the 1st bogie and place the passenger, I 'pop' out of the vehicle.<br>
Get it? Typical stack. This will ensure, the last bogie passenger is placed in the 1st bogie and so on.<br>
Come let's start hacking code<br>

## [Step 5 - Swallow the next bite](http://blog.balajeetm.com/blog/2017/03/08/cracking-a-tnut/#step-5---swallow-the-next-bite)
<hr>

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

while (null != node) {
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

The solution looks pretty neat. But let's be critical.<br>
At even the best case, we need to traverse every node in the list twice.<br>
Once, to pick the member from the bogie and again, to put the right member in place.<br>
The stack atleast made the code neat. Guess we are getting to the end of this<br>
Let's carefully nibble the remnants.

> For more details refer the code @ my [tnut repo](http://github.balajeetm.com/t-nut/blob/master/src/main/java/com/balajeetm/tnut/controller/ReverseSinglyLinkedList.java)<br>
Feel free to fork/clone the same and run it on your local.<br>
Refer [t-nut repo](http://github.balajeetm.com/t-nut/) for more details.

## [Step 6 - Optimize the final bites](http://blog.balajeetm.com/blog/2017/03/08/cracking-a-tnut/#step-6---optimize-the-final-bites)
<hr>

Let's critically evaluate the code and see if there is an opening<br>
Some edge case, some NPE... something<br>

Oh, the relocation function seems a little botched up.<br>
It seems to be counting till the pocket size "n", but the typical edge case we identified through the sample input itself would fail in this case.<br>
We would get a index out of bound. Using the counter is not so catchy. Let's try something cheesy.<br>

```java
while (!stack.empty()) {
	currentRoot.setData(stack.pop());
	currentRoot = currentRoot.getNext();
}
```

What else?<br>
What about a empty input scenario? Seems to work.<br>
What about a pocket size of 1 (n=1)? That seems to work as well.<br>

Hey, there seems to be another case.<br>
The logic seems to empty the stack filled in one cycle, only in the subsequent cycle.<br>
Which means, the last set of 'n' passengers will never be put in place.<br>
Bah!!! That's because we are done traversing the list. Let's fix that.<br>
We need to call relocate again after the while loop. That does it.<br>

> For more details refer the code @ my [tnut repo](http://github.balajeetm.com/t-nut/blob/master/src/main/java/com/balajeetm/tnut/controller/ReverseSinglyLinkedList.java)<br>
Feel free to fork/clone the same and run it on your local.<br>
Refer [t-nut repo](http://github.balajeetm.com/t-nut/) for more details.

## [Step 7 - Beware of pit falls](http://blog.balajeetm.com/blog/2017/03/08/cracking-a-tnut/#step-7---beware-of-pit-falls)
<hr>

We are almost done here, aren't we?<br>
Are we truly done though?<br>
Let's re-look at our last retrospect.<br>
```
At the best case, we traverse every node twice.
```
That's not nice, is it?<br>
Not at all...<br>
I want us to better that.<br>

<img src="/assets/2017-02-26/dobetter.jpg">

Well, I do not want to take the fun out of the moment. That's all we live for.<br>
We have cracked the [T-Nut](/blog/2017/02/21/technical-nuts/) and we have done great.<br>
All I'm saying is we can do better.<br>

Bask in the glory, enjoy the success and when you are ready to bite the bitter pill...<br>
When you are ready to let go and get better, [hop over](/blog/2017/03/12/tnut-reverse-linked-list-pocket-finale/).<br>

Cya [here](/blog/2017/03/12/tnut-reverse-linked-list-pocket-finale/) soon.

> Gentle reminder<br>
All the above tricks and solutions are available in the [tnut repo](http://github.balajeetm.com/t-nut/blob/master/src/main/java/com/balajeetm/tnut/controller/ReverseSinglyLinkedList.java)<br>
Feel free to fork/clone the same and run it on your local.<br>
Refer [t-nut repo](http://github.balajeetm.com/t-nut/) for more details.
