---
layout: post
title: Cracking a T-Nut
date: 2017-03-08 18:42
comments: true
external-url:
categories: -What's-The-Fun-
---

>In my earlier post, we saw what a [T-Nut] is. We also said, moving along, we are gonna be cracking a lot of those.<br>
But how does one go about it? What follows, is a step by step guideline, to cracking a T-Nut.<br>

## The Thought Train<br>
Any problem solving is like cracking a nut. So, we are gonna use the analogy of literally chewing on an unknown fruit and careen our way to the seed/t-nut at the centre.<br>
Remember, just like in a fruit, the T-Nut as a seed, is shrouded in edible pericarps and non-edible epicarps.<br>
As we march towards the T-Nut, we need to cull the epicarp and swallow the pericarp.<br>

Let's begin then<br>

## Step 1 - Isolate the epicarp<br>

This is an unknown fruit. Before we begin cracking the nut in it, let's make sure we understand or atleast roughly gauge the nut.<br>
Is it a groundnut, peanut or a walnut?<br>
And what about the fruit concealing it?<br>
What's its size, texture, and so on…<br>

Basically, ask yourself, if you truly understand the problem.<br>
Once we know the kind of fruit and get to the nut, cracking it is just one hammer away.<br>
Now, why don't we understand the problem?<br>
What's stopping us? Its our distance from the problem, from the T-Nut, that's making it harder, isn't it?<br>
Let's take a closer look.<br>
To do that, let's first set aside the epicarp veiling the fruit.<br>

The epicarp typically, is a seemingly useless, unrelated information, masking the problem.<br>
As you wander into the real world, be it in your corporate environment, or your personal life, rarely is someone going to hand us the problem - like, [reverse a linked list].<br>
Almost Never.<br>
It is up to us to identify the problem which is more often than not in hiding.<br>

Isolating the epicarp is the process of isolating and understanding the problem statement we are trying to address<br>
Sometimes, just isolating the epicarp can almost get you to the solution.<br>

For eg. Consider the problem statement below<br>
Two mirrors 150 miles apart are traveling towards each other along a straight line. The first mirror is travelling at 60 miles per hour, while the second rushes along at 90 miles per hour. A butterfly is fluttering on top of the first mirror. It bustles from one mirror to the other. On reaching a mirror, it turns around immediately, scurries back towards the other, and on reaching it turns around again. It goes on flying back and forth between the two mirrors until they collide. The butterfly is moving at a speed of 120 miles per hour, much faster than the two mirrors.
Assume, for all practical purposes, the butterfly does not lose any time or speed when turning around.
Also assume the change of direction while turning around is spontaneous.<br>
The coefficient of friction (µ) on both mirrors is assumed to be 0 and the coefficient of reflection on both mirrors is 1.<br>
What is the velocity of the butterfly?<br>

So how did you feel reading that?<br>
If you are not from a physics background and did not understand quite a few terms there, well, nothing to worry.<br>

The only thing you ever need to know is what is velocity? Velocity is defined as total displacement over time<br>
V = D/t<br>
Displacement is the total distance moved relative to the point where we started. So in round trip, the displacement is 0, distance however is not. You travelled to and fro, so we did cover some distance.<br>
At the end of it all, though the butterfly did move around a lot, from one mirror to another, it actually didn't quite displace much. That’s the crux of the problem.<br>
So everything else you see - the long verbose description, the coefficient of friction and reflections are all epicarps. Let's cull it.<br>

All you need to do is now find the total distance moved by mirror1 before colliding with mirror2. This is simple relative velocity problem.<br>
Time taken to collide is 150 kms / (90+60 miles/hr) = 1 hr.<br>
So distance travelled by mirror1 is 1 * 60 miles/hr = 60 miles<br>

The butterfly also travels the same since it started from mirror1. So total velocity is 60/1 = 60 60 miles/hr<br>
Awesome right?<br>

The approach I would follow to cull the epicarp is as below<br>
* Jot down the naïve problem statement that you can atleast vaguely comprehend
* Extract the buzz words that hit on you


Step 2 - Take the first bite<br>
It's not often that culling the epicarp will give us the solution. It does better the visibility of the fruit and nut though.<br>
So what do we do next? We don't know the nature of the fruit yet.<br>
Hunger knows no obstacle. Lets proceed and take a first bite.<br>

Our first bites are always calculative right. We prefer to bite the juicy side, at least what we think is juicy.<br>
Juicy here is a problem area which we know to address with ease. Umm… tasty huh.<br>

So for the next bite, we will look at the fruit from an angle where it seems palatable and then take that out. Make the problem more colorful and excite the right brain<br>

So taking the first bite is the process of looking at the problem statement through the lens of something that we already know.<br>
Basically, try to convert it to a problem that you already know or at least approach it like you already know how to get around it.<br>
Apart from the invaluable psychological edge that it boosts, it gives you a path to start walking towards a goal.<br>
* To do so, create a visual representation of the problem.
* Ensure you take relatable examples. If you have never seen such a problem, try to draw parallels with the real world.<br>
If you have seen similar problems, try to keep it as close to your earlier problem as possible and so on.
* Let your "pristine brain" solve it. We can later converting it into logic for the "computational brain"
	

## Step 3 - Swallow the initial bite<br>

Next, start to chew on what you bit.<br>
When we chew on a tasty fruit, we generally focus on the aspects of the fruit that we like.<br>
Its sweetness, juice, color, etc<br>
On similar lines, focus on the aspects of the problem, that you can take away.<br>
Let the bite flow through your esophagus and smoothly into the bowels.<br>
Let some logic to flow through and help connect the dots.<br>

Swallowing is thus synonymous to analysis, logic gathering and retrospection.<br>
You can do this mentally, scribble on paper or start hacking some code.<br>
Do a lot of retrospect and see if the dots connects and check if you are going the right direction.<br>
Try not to force a solution, let it be smooth<br>
The way you swallow greatly influences the next bites we would take. Try to not make it hard for ourselves to take subsequent bites<br>

* Begin by analysing the input and output samples and see if we can catch some rhythm. Catch some logic.
* Identify the edge cases if any through the input output samples
* Begin with naïve "pristine brain" approach and see if you can convert that to a programming logic
* More often, you will be unable to do that, since the "pristine brain" works very differently than the "logical brain".<br>
Just because you solved something mentally, doesn't always mean you can write a program for it. We get stuck most of times when we try to pen something down for this reason. This is why interviewers insist us to write code. This is not to test your syntax strength but to identify some pitfalls in your reasoning.
	
But our pristine brain is extremely adaptable. The more of such problems we solve, the more efficient it will become in working with these types of constraints. And for this reason, we will be cracking a lot of such T-Nuts.
	
While, the logical brain always looks for constraints, the pristine brain always ignores it, if it isn't explicit. "Pristine Brain" only cares about getting to the goal, however that is. So it is important we present the problem with all constraints emphasized, through the "Logical Counterpart"
	

## Step 4 - Take more bites<br>

Alright, we've kind of got the flavour of fruit as we chewed it. We seem to like it.<br>
If you liked what you bit, take similar bites and stride towards the goal.<br>
If you didn't like the taste of the bite, pick the next juicy spot. Look at the problem from a different angle.<br>
Sometimes, our initial approaches may not be the right one.<br>
What we thought was the juicy side, may not turn out to be so.<br>
Change the approach and look for another juicy side until we find the sweet spot.<br>
We may need to change our visual representation to suit the newer approach, and so be it.<br>

This is the crux of problem solving.<br>
Never [hold on] to a solution. We should be able to learn from our approach and [let it go] when situation demands. Don't hold on too tight onto anything<br>

Believe in law of conservation of thought<br>
"You thinking and effort cannot be destroyed. It will manifest itself some way or the other and turn out fruitful"<br>

## Step 5 - Swallow the next bite<br>
As you move along, you can either choose to take similar bites and narrow down on the solution or take a divergent path.<br>
Each time, tried to get some logic flow through and digest the approach. Retrospect and ask yourself if this is taking you towards the goal. Feedback is extremely important<br>
	
## Step 6 - Optimize the final Bites<br>
As you keep gnawing you way through, you are nibbling away the fruit that you have got to work with.<br>
On one hand, you are getting closer to the nut and have probably even discerned the weak links.<br>
Once you get to the nut, all it needs is that one shot and the nut will crack open.<br>

On the other hand, we need to now focus on the areas we ignored. The functional core might be in place or it may seem so, now it is time for litmus test.<br>
Try out the edge cases, empty input and invalid input scenarios and ensure all of these are handled gracefully.<br>
Sometimes, the edge cases can highlight a major flaw in our logic and guess what, we may need to start all over again.<br>
Empty your tummy, pick up a new fruit and start gnawing your way through<br>


