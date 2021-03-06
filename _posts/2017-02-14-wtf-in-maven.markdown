---
layout: post
title: WTF in Maven?
date: 2017-02-14 18:16
comments: true
external-url:
categories: Technology
---

>Any software project is bound to have dependencies. By dependencies, I mean libraries that expose certain features that you want to reuse in your application.<br>
>We of course don't want to reinvent the wheel, do we? (psss… Are you sure you don't want to? We'll discuss that later)

<img style="text-align: center" class="img-responsive" src="/assets/2017-02-14/WhyYouNeedMaven.jpg">

Now that we know our projects have dependencies, how does one manage these dependencies.<br>
Let's consider a Java/JVM based project as a prototype, to understand the challenges with [status quo](https://www.vocabulary.com/dictionary/status%20quo)
	
* **Getting the library**<br>
This is a seemingly trivial task<br>
First, we need to get to the "right location" and download the library<br>
Next, place the library in your classpath before using it in the application<br>
* **Download jinx**<br>
All that glitters is not gold. Be careful of what you download<br>
<u>Authenticity</u> - You need to make sure the library is from an authentic source<br>
<u>Right version</u> -Be sure to download the right variant of the lib with all expected features<br>
<u>Single repo</u> - Wouldn't it be great if all libraries and their versions are available in a single place?<br>
* **Versioning**<br>
Versioning is a Pandora box in itself<br>
If, the library updates itself to the next version, or rather provides more features, redo the above steps for the new version<br>
And if you are the one writing a library, then maintaining different variants is a necessity<br>
* **Dependency**<br>
More often than not, dependencies themselves depend on other libraries. So one needs to repeat the above steps to download the dependencies of dependencies.
This is called "Transitive Dependency". Transitive dependency as we see, can go deeper and deeper
* **Conflicts**<br>
Now transitive dependencies is another Pandora box<br>
Two dependent libs can transitively fetch different versions of a library<br>
Now which one do you choose?<br>
If you are wondering why you should choose only one - Well the classloader does not care about from which jar classes come from. So if two versions of the same lib is in the classpath, only one will be loaded (assuming package structure between libs is the same).<br>
So its best to include just one version to prevent ambiguity
*  **Pre Release dependencies**<br>
This is a classical problem. How does one, version the library during an ongoing change?<br>
We wouldn’t want to keep incrementing the version for every small change but we would still want to differentiate between ongoing changes

## <b>How does one get around this?</b>
We can address these in multiple ways. Let's go in a chronological order of thoughts
* **Manual Exercise**<br>
We can follow a manual process to address all of the above<br>
* **Be an engineer**<br>
Either develop a comprehensive solution for the problem and pave way for others to follow or<br>
Reuse whatever is available out of the box from an existing solution.<br>
	
The problems described above was faced by many organizations across the globe.<br>
So maven in short is the one stop solution to address all these dependency and build management issues.<br>
It’s a flexible solution that follows convention over configuration.<br>
So if you follow a convention, there is very little to configure. But if you claim to be a rebel, well then you are welcome to maven's haven as well. Just that you would need to keep yourself busy with a lot of custom configurations. That's however not an issue.<br>
Like they say - For each one, their way!

Now that we know the enemy we are up against, let's see how maven tackles these for us. Join me in my next [post](/blog/2017/02/17/maven-safe-haven/)
