---
layout: post
title: Maven's safe Haven
date: 2017-02-17 22:43
comments: true
external-url:
categories: Technology
---

>In my earlier [post](), we saw the typical dependency issues faced while building an enterprise application.<br>
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
There are many ways to configure custom repo. You can do it via the [pom](local reference to POM) or settings.xml<br>
			
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
			
Multiple repositories can be defined. Refers [maven docs](https://maven.apache.org/pom.html#Repositories) for more info<br>
			
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
	
Eg. Json Mystique will be uniquely identified as<br>
```xml
<groupId>com.balajeetm.mystique</groupId>
<artifactId>json-mystique</artifactId>
<version>2.0.4-SNAPSHOT</version>
```
	Maven's versioning scheme uses the following standards:
		○ MajorVersion
		Eg. In the above "2" is the major version
		○ MinorVersion
		Eg.In the above "0" is the minor version
		○ IncrementalVersion
		Eg.In the above "SNAPSHOT" is the incremenal version
		○ BuildNumber
		Eg. In an artifact version represented as "x.x.x-y-z", y and z are build number
		Y is the patch set number and Z is the bundle patch
		○ Qualifier
		Eg. 2.0-beta-3
		
	Version Comparison Rules
	All versions with a qualifier are older than the same version without a qualifier (release version).
	For example:
	2.0-beta-2 is older than 2.0.
	Identical versions with different qualifier fields are compared by using basic string comparison.
	For example:
	2.0-beta-3 is newer than 2.0-alpha-7
	
	For more details grind [here](https://docs.oracle.com/middleware/1212/core/MAVEN/maven_version.htm#MAVEN8855)
	
	• Dependency
	Dependency management is one of the features of Maven that is best known to users and is one of the areas where Maven excels. There is not much difficulty in managing dependencies for a single a project, but when you start getting into dealing with multi-module projects and applications that consist of tens or hundreds of modules this is where Maven can help you a great deal in maintaining a high degree of control and stability.
	
	Transitive dependencies are a new feature since Maven 2.0. This allows you to avoid needing to discover and specify the libraries that your own dependencies require explicitly. Once you specify a library, maven will automatically include all the dependencies of your dependency.
	This feature is facilitated by reading the project files of your dependencies from the remote repositories specified. In general, all dependencies of those projects are used in your project, as are any that the project inherits from its parents, or from its dependencies, and so on.
	
	For details hop [here](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html)
	
	• Resolving Conflicts
	Maven resolves conflicts by constructing a dependency tree.
	By default Maven resolves version conflicts with a nearest-wins strategy. If two versions of the same library are at equal distance, then maven picks the one with the higher version
	
	For details peek [here](https://maven.apache.org/plugins/maven-dependency-plugin/examples/resolving-conflicts-using-the-dependency-tree.html)
	
	• Pre-Release Versioning
	Maven has a special versioning scheme to deal with ongoing changes, namely the SNAPSHOT qualifier
	Maven treats the SNAPSHOT qualifier differently from all others. If a version number is followed by -SNAPSHOT, then Maven considers it the "as-yet-unreleased" version of the associated MajorVersion, MinorVersion, or IncrementalVersion.
	
	In a continuous integration environment, the SNAPSHOT version plays a vital role in keeping the integration build up-to-date while minimizing the amount of rebuilding that is required for each integration step.
	
	SNAPSHOT version references enable Maven to fetch the most recently deployed instance of the SNAPSHOT dependency at a dependent project build time. Note that the SNAPSHOT changes constantly. Whenever an agent deploys the artifact, it is updated in the shared repository. The SNAPSHOT dependency is refetched, on a developer's machine or it is updated in every build. This ensures that dependencies are updated and integrated with the latest changes without the need for changes to the project dependency reference configuration.
	
	How it manages to achieve this , is by simply converting the SNAPSHOT qualifier into long timestamp denoting when the artifact was build. Thus, it really easy to compare snapshot versions and fetch the latest.
	
	Smart huh? For details look [here](https://docs.oracle.com/middleware/1212/core/MAVEN/maven_version.htm#MAVEN401)
	
	• Maven Configurations
	Maven executions can be configured to suit your needs. This can be done in multiple ways.
		○ POM
		https://maven.apache.org/pom.html
		
		○ Settings.xml
		The settings.xml basically is a file that contains elements used to define values which configure Maven execution in various ways, just like the pom.xml. The difference however is that pom is project specific setting and settings in settings.xml are common for all projects.
		For more details - jump [here](https://maven.apache.org/settings.html#Quick_Overview)
	

That's great
You seem to know so much more about maven now.
I've written a sample project explaining the dependency tree here. Do have a look.

	• Simple jar project, build using archetype
	• Include json mystique dependency
	• Run dependency tree and show guava coming in
