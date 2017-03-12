---
layout: post
title: Isolating an Epicarp
date: 2017-03-10 16:19
comments: true
external-url:
categories: Examples
---

>In my earlier post, we saw what a [T-Nut](/blog/2017/02/21/technical-nuts/) is and how we go about [cracking a T-Nut](/blog/2017/03/08/cracking-a-tnut)<br>
We realised, there are multiple stages to cracking it, and first of those stages is [isolating the epicarp](/blog/2017/03/08/cracking-a-tnut/#step-1---isolate-the-epicarp).<br>
Let's take a typical example to illustarte what that means. Remember, sometimes, that by itself, can get you almost to the solution. 

## <u>The Problem Statement</u>

Consider a scenario as below<br>
```
Two mirrors 150 kms apart are travelling towards each other along a straight line.
The first mirror is travelling at 60 kms per hour,
while the second rushes along at 90 kms per hour.
A butterfly is fluttering on top of the first mirror.
It bustles from one mirror to the other.
On reaching a mirror, it turns around immediately, and scurries back towards the other,
and on reaching it turns around again.
It goes on flying back and forth between the two mirrors until they collide.

The butterfly is moving at a constant speed but much faster than the two mirrors.
For all practical purposes, assume the below
"The butterfly does not lose any time or speed when turning around"

Also assume the change of direction while turning around is spontaneous.
The coefficient of friction (µ) on both mirrors is assumed to be 0,
while the coefficient of reflection on both mirrors is assumed to be 1.

What is the velocity of the butterfly?
```

<img src="/assets/2017-03-10/mirrors.png">

## <u>The Solution</u>

So how did you feel reading that epic?<br>
There was so much that was said, did the question feel complicated?<br>
Let's try to extract the relevant info from the eloquent barrage.<br>
If you are not from a physics background and did not understand quite a few terms there, well, not to worry.<br>
The only thing you ever need to know is what is velocity?<br>
[Velocity](https://en.wikipedia.org/wiki/Velocity) is defined as total displacement over time.<br>
```
V = Displacement/time
```

[Displacement](https://en.wikipedia.org/wiki/Displacement_(vector)) is the total distance moved relative to the point where we started. So in a round trip, the displacement is 0, distance however is not.<br>

<img src="/assets/2017-03-10/displace-distance.png">

At the end of it all, though the butterfly did move around a lot, from one mirror to another, back and forth, it actually didn't quite displace much.<br>
**Getting that is the crux of the problem.**<br>
Everything else you see - the long verbose description, the coefficient of friction and reflections are all distractions... are all [epicarps](https://en.wikipedia.org/wiki/Fruit_anatomy#Epicarp).
Let's cull it then.<br>

All you need to do is now find the total distance moved by mirror-1 before colliding with mirror-2.<br>
Because the displacement of the butterfly is how far mirror-1 has moved from the initial point.<br>
Wonder why? The butterfly started at the same point remember?<br>
Ting, Ring - Does that ring a bell?<br>

If that's understood, this is simple relative velocity problem.<br>
Time taken to collide is calculated as below<br>

```
Distance = 150 kms
Relative speed since trains are moving towards each other = 
90 + 60 = 150 kms/hr

Total time thus = 150/(90+60) = 1 hr
```

So distance travelled by mirror-1 in this 1 hour is
```
1 hr * 60 kms/hr = 60 kms
```

So total velocity of the butterfly is

```
60 kms/1 hr = 60 kms/hr
```

**60 kms per hour**. Awesome right?<br>
Pice of cake, if only we set aside the epicarp<br>

## <u>The Learning</u>

Is it loud and clear now? Do you see how much difference picking the relevant info from a problem statement makes?<br>
We tend to understand the problem so much better, when we focus on the specifics.<br>
Once, we understand the problem, solving it is a breeze.<br>
Just a hammer away !!!

If [culling the epicarp](/blog/2017/03/08/cracking-a-tnut/#step-1---isolate-the-epicarp) doesn't yet get you to the solution, try out the [subsequent steps](/blog/2017/03/08/cracking-a-tnut/#step-2---take-the-first-bite).



