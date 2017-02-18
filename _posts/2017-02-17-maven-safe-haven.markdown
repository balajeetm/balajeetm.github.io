---
layout: post
title: Maven's safe Haven
date: 2017-02-17 22:43
comments: true
external-url:
categories: Technology
---

>In my earlier [post](/blog/2017/02/14/why-maven/), we saw the typical dependency issues faced while building an enterprise application.<br>
>Enter Maven, and all these issues are history<br>

<img style="text-align: center" class="img-responsive" src="/assets/2017-02-17/IDontAlwaysMaven.jpg">

How does maven address the above?
## <u><b>Getting the library/ Download jinx</b></u>
Maven needs a repository that contains different libraries , all versions implied.<br>
We can download all the dependencies we would need (once) and set up a repository.<br>
We can configure maven to use appropriate maven repositories that we have set up. We can even configure it to use multiple repositories.<br>
	
There are three categories of repositories
* **Remote**<br>
This is the repository at a remote location containing all libraries and plugins (Oopsie, what's a [plugin](https://maven.apache.org/plugins/) now)<br>
This is could either be a custom repo set up by you or a repo set up by someone else that you use<br>
		
If setting up a repo is cumbersome for you, use [Maven Central Repo](http://repo1.maven.org/maven2/).<br>
This is the repo set up by the maven community which contains all open source public libraries and plugins.<br>
For eg, all my maven libraries can be found in the public repo here - [Bala's Repo](http://repo1.maven.org/maven2/com/balajeetm/)<br>
	
If you have not configured maven to any custom repo, this is the default repo that maven will connect to get artifacts over internet<br>
		
* **Custom Repository**<br>
Custom repository is a remote repository set by you or your organization. This will typically contain your company specific artifacts which is not shared to the general public. It can optionally sync with the central maven repo to get the public artifacts and be an one stop shop for all libraries but that is an organizational choice<br>

<u><b>Configuring Maven to use custom repo</b></u><br>
There are many ways to configure custom repo. You can do it via the [pom](#maven-configurations) or [settings.xml](#maven-configurations)<br>
			
<u>Pom changes</u><br>
Within the pom file, define a repository referring to the location where artifacts can be found.<br>
For eg.<br>
Configure the below to fetch my maven libraries (including snapshots) from a non maven central repo<br>
```xml
<repositories>
	<repository>
		<id>bala_repo</id>
		<url>https://oss.sonatype.org/content/groups/public/com/balajeetm/</url>
	</repository>
</repositories>
```
			
Multiple repositories can be defined. Refer [maven docs](https://maven.apache.org/pom.html#Repositories) for more info<br>
			
<u>Settings.xml</u><br>
First configure a repository in the active profile, and set the url to the custom repo.<br>
Alternatively, you can specify the url in the mirror of the repo as shown below. The url specified in the mirror has precedence over the one specified in the repo url<br>
To configure settings.xml to refer your custom repo, first add the repository as below in your active profile<br>
```xml
<repositories>
	<repository>
		<id>bala_repo</id>
		<url>http://bogus</url>
		<releases>
			<enabled>true</enabled>
		</releases>
		<snapshots>
			<enabled>true</enabled>
			<updatePolicy>always</updatePolicy>
		</snapshots>
	</repository>
</repositories>
```
			
Then add the mirror
```xml
<mirrors>
	<mirror>
		<id>bala_mirror</id>
		<url>https://oss.sonatype.org/content/groups/public/com/balajeetm/</url>
		<mirrorOf>bala_repo</mirrorOf>
	</mirror>
</mirrors>
```
* **[Local Repository](https://maven.apache.org/guides/introduction/introduction-to-repositories.html)**<br>
The local repository refers to a copy on your own installation that is a cache of the remote downloads, and also contains the temporary build artifacts that you have not yet released.

## <u><b>Versioning</b></u>
To prevent any ambiguity in defining a version and to easily compare two versions, maven defines a standard versioning scheme.<br>
An artifact is uniquely identified with a combination of the below triple<br>
* Groupid
* Artifactid
* Version

The current implementation of DefaultArtifactVersion in the core of Maven, expects that version numbers will have a very specific format:<br>
```
<MajorVersion [> . <MinorVersion [> . <IncrementalVersion ] ] [> - <BuildNumber | Qualifier ]>
```

Where MajorVersion, MinorVersion, IncrementalVersion and BuildNumber are all numeric and Qualifier is a string. If your version number does not match this format, then the entire version number is treated as being the Qualifier.<br>
Eg. Json Mystique will be uniquely identified as<br>
```xml
<groupId>com.balajeetm.mystique</groupId>
<artifactId>json-mystique</artifactId>
<version>2.0.4-SNAPSHOT</version>
```

Maven's versioning scheme uses the following standards:
* MajorVersion<br>
Eg. In the above "2" is the major version
* MinorVersion<br>
Eg.In the above "0" is the minor version
* IncrementalVersion<br>
Eg.In the above "4" is the incremental version
* BuildNumber<br>
Eg. In an artifact version represented as "x.x.x-y-z", y and z are build number
"Y" is the patch set number and "Z" is the bundle patch
* Qualifier<br>
Eg. 2.0-beta-3
		
<u><b>Version Comparison Rules</b></u><br>
All versions with a qualifier are older than the same version without a qualifier (release version).<br>
For example:<br>
2.0-beta-2 is older than 2.0.<br>
Identical versions with different qualifier fields are compared by using basic string comparison.<br>
For example:<br>
2.0-beta-3 is newer than 2.0-alpha-7<br>

For more details grind [here](https://docs.oracle.com/middleware/1212/core/MAVEN/maven_version.htm#MAVEN8855)<br>

## <u><b>Dependency</b></u><br>
Dependency management is one of the features of Maven that is best known to users and is one of the areas where Maven excels. There is not much difficulty in managing dependencies for a single a project, but when you start getting into dealing with multi-module projects and applications that consist of tens or hundreds of modules this is where Maven can help you a great deal in maintaining a high degree of control and stability.<br>

Transitive dependencies are a new feature since Maven 2.0. This allows you to avoid needing to discover and specify the libraries that your own dependencies require explicitly. Once you specify a library, maven will automatically include all the dependencies of your dependency.<br>
This feature is facilitated by reading the project files of your dependencies from the remote repositories specified. In general, all dependencies of those projects are used in your project, as are any that the project inherits from its parents, or from its dependencies, and so on.<br>

For details hop [here](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html)<br>

## <u><b>Resolving Conflicts</b></u><br>
Maven resolves conflicts by constructing a dependency tree.<br>
It basically figures out what libraries are coming from what sources (transitive dependency my friend) and decides which version should be carried to the classpath. This process of choosing one version from many available is called conflict resolution.<br>
By default Maven resolves version conflicts with a nearest-wins strategy. If two versions of the same library are at equal distance, then maven picks the one with the higher version<br>

Let's take an example as below.<br>
<img style="text-align: center" src="/assets/2017-02-17/ConflictResolution.png">

Lib A is dependent on Lib B and Lib C. Lib C however is dependent on Lib B and Lib D. Lib B is dependent on Lib D. The versions are showb in the diagram.<br>
The libraries in the final classpath will contain Lib A (obviously), Lib B and Lib C (since Lib A transitively gets them) and Lib D since the transitive dependencies in turn get it along transitively. The final classpath shows the versions of the libraries however.<br>
But 'WTF' in that? How's maven deciding that?<br>
* Firstly, Maven constructs a dependency tree as shown in the diagram including versions at different levels.
* Lib A and its classes are through because its at the top of the hierarchy
* There are 2 versions of Lib B now available. But ver 1 at level 1 is nearer than ver 2 at level 2. So ver 1 wins.<br>
* There is only one version of Lib C. So 'C' and its classes are also through transitively.<br>
* There are 3 versions of Lib D available. As per the 'nearest-wins' strategy, ver 3 is out of picture. However, both ver 1 and ver 2 are equidistant at level 3.<br>
Maven now picks the highest version at the same distance and chooses ver 2.<br>

Simple huh? Nothing really is complex see?<br>
If you seek more details though, peek [here](https://maven.apache.org/plugins/maven-dependency-plugin/examples/resolving-conflicts-using-the-dependency-tree.html)<br>

## <u><b>Pre-Release Versioning</b></u><br>
Maven has a special versioning scheme to deal with ongoing changes, namely the SNAPSHOT qualifier<br>
Maven treats the SNAPSHOT qualifier differently from all others. If a version number is followed by -SNAPSHOT, then Maven considers it the "as-yet-unreleased" version of the associated MajorVersion, MinorVersion, or IncrementalVersion.<br>

In a continuous integration environment, the SNAPSHOT version plays a vital role in keeping the integration build up-to-date while minimizing the amount of rebuilding that is required for each integration step.<br>

SNAPSHOT versions enable Maven to fetch the most recently deployed instance of the SNAPSHOT dependency at a dependent project build time. Note that the SNAPSHOT changes constantly. Whenever an agent deploys the artifact, it is updated in the shared repository. The SNAPSHOT dependency is refetched, on a developer's machine or it is updated in every build. This ensures that dependencies are updated and integrated with the latest changes without the need for changes to the project dependency reference configuration.<br>

But 'WTF' in that? How does maven achieve that?<br>
It does this, simply by converting the SNAPSHOT qualifier into long timestamp, denoting when the artifact was built/deployed. Thus, its really easy to compare snapshot versions and fetch the latest.<br>

Simple again huh?<br>
For more details look [here](https://docs.oracle.com/middleware/1212/core/MAVEN/maven_version.htm#MAVEN401)<br>

## <u><b id='maven-configurations'>Maven Configurations</b></u><br>
Maven executions can be configured to suit your needs. This can be done in multiple ways.
* **POM**<br>
POM stands for "Project Object Model". It is an XML representation of a Maven project held in a file named pom.xml.
Wrt Maven, a project is beyond a mere collection of files containing code. A project contains configuration files, as well as the developers involved and the roles they play, the defect tracking system, the organization and licenses, the URL of where the project lives, the project's dependencies, and all of the other little pieces that come into play to give code life.<br>
It is a one-stop-shop for all things concerning the project. In fact, in the Maven world, a project need not contain any code at all, merely a pom.xml.<br>
One of the biggest perks of using maven is that <b>'maven documents the build process'</b>.<br>
There is so much to learn about the project and its build prcoess before even venturing into the code. Maven gets that crux quite right aye.<br>
If you seek more details however - [here goes](https://maven.apache.org/pom.html)
	
* **Settings.xml**<br>
The settings.xml basically is a file that contains elements used to define values which configure Maven execution in various ways, just like the pom.xml. The difference however is that pom is  a project specific setting and settings in settings.xml are common for all projects.<br>
For more details - jump [here](https://maven.apache.org/settings.html#Quick_Overview)

## <u><b>To Wrap Up</b></u><br>
That's great
You seem to know so much more about maven now.

<img style="text-align: center" src="/assets/2017-02-17/noMavenNoob.jpg">

I've written a sample project explaining the use of maven and the concepts that I've explained above [here](). Do have a look.<br>
Have fun and keep smiling until we catch up next time.
