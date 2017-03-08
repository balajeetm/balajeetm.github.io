---
layout: post
title: Cracking a T-Nut
date: 2017-03-08 18:42
comments: true
external-url:
categories: -What's-The-Fun-
---

>In my earlier post, we saw what a [T-Nut](/blog/2017/02/21/technical-nuts/) is. We also said, moving along, we are gonna be cracking a lot of those.<br>
But how does one go about it? What follows, is a step by step guideline, to cracking a T-Nut.<br>

<img src="/assets/2017-03-08/crackingTheNut.jpg">

## The Thought Train
<hr>

Any problem solving is like cracking a nut. So, we are gonna use the analogy of literally chewing on an unknown fruit and careen our way to the seed/t-nut at the centre.<br>
Remember, just like in a fruit, the T-Nut as a seed, is shrouded in edible [pericarps](https://en.wikipedia.org/wiki/Fruit_anatomy#Pericarp_layers) and non-edible [epicarps](https://en.wikipedia.org/wiki/Fruit_anatomy#Epicarp).<br>
As we march towards the [T-Nut](/blog/2017/02/21/technical-nuts/), we need to cull the epicarp and swallow the pericarp.<br>

<img src="/assets/2017-03-08/pericarp.jpg">

Let's begin then<br>

## Step 1 - Isolate the [epicarp](https://en.wikipedia.org/wiki/Fruit_anatomy#Epicarp)
<hr>

This is an unknown fruit. Before we begin cracking the nut in it, let's make sure we understand or atleast roughly gauge the nut.<br>
Is it a groundnut, peanut or a walnut?<br>
And what about the fruit concealing it?<br>
What's its size, texture, and so on…<br>

Basically, ask yourself, if you truly understand the problem.<br>
Once we know the kind of fruit and get to the nut, cracking it is just one hammer away.<br>
Now, why don't we understand the problem?<br>
What's stopping us? Its our distance from the problem, distance from the [T-Nut](/blog/2017/02/21/technical-nuts/), that's making it harder, isn't it?<br>
Let's take a closer look.<br>
To do that, let's first set aside the epicarp veiling the fruit.<br>

The epicarp typically, is a seemingly useless, unrelated information, masking the problem.<br>
As you wander into the real world, be it in your corporate environment, or your personal life, rarely is someone going to hand us the problem - like, [reverse a linked list](/blog/2017/02/26/tnut-reverse-linked-list-pocket/).<br>
Almost Never.<br>
It is up to us to identify the problem which is more often than not in hiding.<br>

Isolating the epicarp is the process of isolating and understanding the problem statement we are trying to address<br>
Sometimes, just isolating the epicarp can almost get you to the solution.<br>

For eg. Consider the problem statement below<br>
```
Two mirrors 150 miles apart are traveling towards each other along a straight line. The first mirror is travelling at 60 miles per hour, while the second rushes along at 90 miles per hour. A butterfly is fluttering on top of the first mirror. It bustles from one mirror to the other. On reaching a mirror, it turns around immediately, scurries back towards the other, and on reaching it turns around again. It goes on flying back and forth between the two mirrors until they collide. The butterfly is moving at a speed of 120 miles per hour, much faster than the two mirrors.
Assume, for all practical purposes, the butterfly does not lose any time or speed when turning around.
Also assume the change of direction while turning around is spontaneous.
The coefficient of friction (µ) on both mirrors is assumed to be 0 and the coefficient of reflection on both mirrors is 1.

What is the velocity of the butterfly?
```

So how did you feel reading that?<br>
If you are not from a physics background and did not understand quite a few terms there, well, nothing to worry.<br>

The only thing you ever need to know is what is velocity? [Velocity](https://en.wikipedia.org/wiki/Velocity) is defined as total displacement over time<br>
V = Displacement/time<br>
[Displacement](https://en.wikipedia.org/wiki/Displacement_(vector)) is the total distance moved relative to the point where we started. So in round trip, the displacement is 0, distance however is not. You travel to and fro, so we do cover some distance in a round trip.<br>
At the end of it all, though the butterfly did move around a lot, from one mirror to another, it actually didn't quite displace much. That’s the crux of the problem.<br>
So everything else you see - the long verbose description, the coefficient of friction and reflections are all epicarps. Let's cull it.<br>

All you need to do is now find the total distance moved by mirror-1 before colliding with mirror-2. This is simple relative velocity problem.<br>
Time taken to collide is calculated as below<br>
```
Distance = 150 kms
Relative speed since trains are moving towards each other = 90 + 60 = 150 miles/hour

Total time thus = 150/(90+60) = 1 hr
```

So distance travelled by mirror-1 in this 1 hour is
```
1 hr * 60 miles/hr = 60 miles
```

The butterfly also travels the same since it started from mirror-1. So total velocity of the butterfly is
```
60 miles/1 hr = 60 miles/hr
```

**60 miles per hour**. Awesome right? If only we set aside the epicarp<br>

The approach I would follow to cull the epicarp is as below<br>
* Jot down the naïve problem statement that you can atleast vaguely comprehend
* Extract the buzz words that hit on you

## Step 2 - Take the first bite
<hr>

It's not often that culling the epicarp will give us the solution. It does better the visibility of the fruit and nut though.<br>
So what do we do next? We don't know the nature of the fruit yet.<br>

Well, 'Hunger' knows no barriers. Lets proceed and take a first bite.<br>

Our first bites are always calculative right. We prefer to bite the juicy side, at least what we think is juicy.<br>
Juicy here is a problem area which we know to address with ease. Umm… tasty huh.<br>

So for the next bite, we will look at the fruit from an angle where it seems palatable and then take that out. Make the problem more colorful and excite the brain<br>

So taking the first bite is the process of looking at the problem statement through the lens of something that we already know.<br>
Basically, try to convert it to a problem that you already know or at least approach it like you already know how to get around it.<br>
Apart from the invaluable psychological edge that it boosts, it gives you a path to start walking towards a goal.<br>
To do so<br>
* Create a visual representation of the problem.
* Ensure you take relatable examples. If you have never seen such a problem, try to draw parallels with the real world.<br>
If you have seen similar problems, try to keep it as close to your earlier problem as possible and so on.
* Let your "pristine brain" solve it. We can later convert it into logic for the "computational brain"

## Step 3 - Swallow the initial bite
<hr>

Next, start to chew on what you bit.<br>
When we chew on a tasty fruit, we generally focus on the aspects of the fruit that we like.<br>
Its sweetness, juice, color, etc<br>
On similar lines, focus on the aspects of the problem, that you can take away.<br>
Let the bite flow through your esophagus and smoothly into the bowels.<br>
Let some logic to flow through the disparate dots and help connect them.<br>

Swallowing is thus synonymous to analysis, logic gathering and retrospection.<br>
You can do this mentally, scribble on paper or start hacking some code.<br>
Do a lot of retrospection and see if the dots connect and check if you are going the right direction.<br>
Try not to force a solution, let it be smooth<br>
The way we swallow greatly influences the next bites we would take. Try to not make it hard for ourselves to take subsequent bites<br>

* Begin by analysing the input and output samples and see if we can catch some rhythm. Catch some logic.
* Identify the edge cases if any through the input output samples
* Begin with naïve "pristine brain" approach and see if you can convert that to a programming logic
* More often, you will be unable to do that, since the "pristine brain" works very differently than the "logical brain".<br>
Just because you solved something mentally, doesn't always mean you can write a program for it. We get stuck most of times when we try to pen something down for this reason. This is why interviewers insist us to write code. This is not to test your syntax strength but to identify some pitfalls in your reasoning.

#### Note

But our pristine brain is extremely adaptable. The more of such problems we solve, the more efficient it will become in working with these types of constraints. And for this reason, we will be cracking a lot of such [T-Nuts](/blog/2017/02/21/technical-nuts/).
	
While, the logical brain always looks for constraints, the pristine brain always ignores it, if it isn't explicit. "Pristine Brain" only cares about getting to the goal, however that is. So it is important we present the problem with all constraints emphasized, through the "Logical Counterpart"
	

## Step 4 - Take more bites
<hr>

Alright, we've kind of got the flavour of fruit as we chewed it.<br>
If you liked what you bit, take similar bites and stride towards the goal.<br>
If you didn't like the taste of the bite, pick the next juicy spot.<br>
Sometimes, our initial approaches may not be the right one.<br>
What we thought was the juicy side, may not turn out to be so.<br>
Change the approach and look for another juicy side until we find the sweet spot.<br>
We may need to change our visual representation to suit the newer approach... So be it.<br>

This is the crux of problem solving.<br>
Never [hold on] to a solution. We should be able to learn from our approach and [let it go] when situation demands. Don't hold on too tight onto anything<br>

Believe in law of conservation of thought
```
"You thinking and effort cannot be destroyed.
It will manifest itself some way or the other and turn out fruitful"
```

## Step 5 - Swallow the next bite
<hr>

As you move along, you can either choose to take similar bites and narrow down on the solution or take a divergent path.<br>
Each time, try to get some logic flow through and digest the approach.<br>
Retrospect and ask yourself if this is taking you towards the goal. Feedback is extremely important<br>
	
## Step 6 - Optimize the final Bites
<hr>

As you keep gnawing you way through, you are nibbling away the fruit that you have got to work with.<br>
On one hand, you are getting closer to the nut and have probably even discerned the weak links. Once you get to the nut, all it needs is that one shot and the nut will crack open.<br>

On the other hand, we need to now focus on the areas we ignored. The functional core might be in place (or it may seem so), now it is time for the litmus test.<br>
Try out the edge cases, empty input and invalid input scenarios and ensure all of these are handled gracefully.<br>
Our logic shouldn't go bonkers!!!<br>
Sometimes, the edge cases can highlight a major flaw in our logic and guess what, we may need to start all over again.<br>
Empty your tummy, pick up a new fruit and start gnawing your way through<br>

Its' road to El Dorado!!


