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
The sample input and respective outputs expected are below

Input:	1->2->3->4->5->6->NULL and n = 2
Output:	2->1->4->3->6->5->NULL.

Input:	1->2->3->4->5->6->7->8->NULL and n = 3
Output:	3->2->1->6->5->4->8->7->NULL.
```

## The Thought Train
<hr>

Let's begin [cracking the T-Nut](/blog/2017/03/08/cracking-a-tnut/), shall we?
Like always, we are gonna use the analogy of literally chewing on an unknown fruit, to crack this [T-Nut](/blog/2017/02/21/technical-nuts/).<br>
Let's follow this [step by step guide](/blog/2017/03/09/thumbrules-to-crack-a-tnut/) as we do so.

## [Step1 - Isolate the epicarp](/blog/2017/03/08/cracking-a-tnut/#step-1---isolate-the-epicarp)
<hr>

The epicarp is already culled for us. Let's re-look at the problem statement<br>

* <b><u>The Naïve Problem Statement</u></b><br>
This as I understand is to reverse a linked list with some constraints<br>

* Let me nibble on <b><u>The Buzz Words</u></b> now

<u>Singly Linked List</u><br>
What do I get out of this?
* Size is unavailable and can be tremendously huge
* Cannot access an item based on index/position. I need to get to every item
* The traversal is unidirectional. We cannot move back and forth.

<u>Reverse in blocks of "n"</u><br>
Well, doesn't quite sit pretty in the head, but let me move on. I will let it dawn on me.

## [Step2 - Take the first bite](/blog/2017/03/08/cracking-a-tnut/#step-2---take-the-first-bite)
<hr>

* <b><u>Visual Representation</u></b>
Since I can't think of any similar problem I've solved, let me try something closer to real life.<br>
The first realistic thing that comes to my mind when you say linked list, is a train with bogies.<br>
Let me create a 2D train with bogies representing nodes. The values of the nodes represent the solitary passenger, commuting in them<br>

<img style="text-align: center" src="/assets/2017-02-26/train.png">
	
* <b><u>Analyze input output samples</u></b>
* <b><u>Solve it mentally</u></b>
Let's see if I understand the input, output samples<br>

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
2->1->4->3->6->5->NULL
```

Alright, feels like I can now guess that output from the input. Time to chew on the bite now.

## [Step3 - Chew and swallow the bite]
<hr>

* <b><u>Identify edge cases</u></b>
In the second sample, we have

```
Input:
1->2->3->4->5->6->7->8->NULL, ok a list with 8 elements
And n=3
```

```
So let me reverse group of three elements
3->2->1

6->5->4

8->7

Putting them together
3->2->1->6->5->4->8->7->NULL
```

Ok, there is an edge case, If 3 elements are not available, **it should sort whatever is available.**
That’s a good catch.

Also, let's try to garnish that logic now

* <b><u>Create a logical flow</u></b><br>
Let me first see how Mr.Pristine went about it<br><br>
He first split the linked list in batches of "n"<br>
He then reversed the sub link list<br>

Penning down a logic flow for the same
* Splitting a linked list<br>
This should be straight forward, I keep moving across the list and pick "n" nodes

<b style="color:red">Markers</b><br>
<b>How do I work on the picked ones? Should I make a copy of them all, or use the existing nodes?</b><br>
To try answering these, let us connect back to our visual representation.<br>
		
I may end up making a copy of the whole train. I mean that’s freaking bulky and not space effective.<br>
(See? Visualizing helps you understand the inefficiencies sometimes)<br>
<b style="color:red">Markers<Alert!></b> Keep a bookmark of this please, we'll get back to this soon
		
* Reversing a linked list<br>
How did Mr.Pristine do that?<br>

Well he went to the last item in each sub-list. And then put the numbers in reverse.
Hey… wait… WTF in that? How can he do that?<br>
You cannot traverse back in a singly linked list, can you?<br>
But for Mr Pristine, there is no such thing as a singly linked list. There are no constraints. He just started walking in reverse direction. Cheater!

As we call out the bluff of Mr.Pristine, let's emphasize the constraints for him.<br>
Let's present the problem through our train analogy adding an explicit constraint<br>
Even in train bogies, we can move back and forth, so,<br>
'Assume there is a guard standing at the door preventing you from going back. He will only let you go forward'<br>
So we have a physical separation through bogies and we've also ensured unidirectional movement<br>

### <u>What is the problem statement now?</u>
What does reversing mean?<br>
We need to make sure the passengers in bogies are relocated. And the relocation constraint is reversal in blocks of 'n'.<br>
Crystal clear.<br>

How would we that in such a scenario?<br>

First, get a EV or a segway.<br>
Pick the 1st bogie passenger, take the EV to the nth bogie and put him there.<br>
Pick the passenger in the nth bogie and get him to the first.<br>
Now pick the passenger in the 2nd bogie and move all the way to n-1th bogie.<br>
Repeat, and redo for passengers from n+1 th bogies.<br>

Great, let's code this now.














