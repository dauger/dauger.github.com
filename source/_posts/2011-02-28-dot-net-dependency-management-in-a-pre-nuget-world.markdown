---
layout: post
title: ".NET Dependency Management in a Pre-Nuget World"
date: 2011-02-28 19:57
comments: false
categories: development 
---
This post is an attempt to capture how my previous team dealt with dependency / package management. The team, at its largest point, consisted of about 15 developers. There were roughly 200 3rd party dlls, and roughly 150 internal dlls in the dependency mix. No single app needed all 350 dlls, but groups of these dlls were common to applications in the same domain space of the enterprise. 3rd party dlls were things such as the MS Enterprise Library, image conversion libraries, desktop scanner interop libraries, etc… Internal dlls were things such as common utility libraries, WCF service contracts, DTOs etc… <!-- more -->

Until the recent development of projects such as [Nuget](http://haacked.com/archive/2010/10/06/introducing-nupack-package-manager.aspx) and [OpenWrap](http://www.openwrap.org/), dependency management in .NET has been a big problem. The larger a development group’s topology is, the more of a pain point it is. Because this is the case, a lot of teams don’t even realize they are going to have issues until the pain is upon them. Additionally, I think the complexity of describing the problem has helped to keep package management as an elephant in the .NET room for a long time.

Since there has been abundant discussion on this issue lately, I’m going to skip describing the problems with dependency management and get straight into what we tried over the years, and what the final solution ended up being. It’s important to note that my team used TFS (2008) for source control because some of the steps we took were in response to TFS’ weaknesses.

## First attempt ending in Failure:

* **Manage all 3rd party dlls by putting them in a \[sln\]\\bin folder (tracked by TFS).**
* **Manage all internal dependencies as shared projects across multiple slns.**

I’m sure some of you are already cringing after reading the last bullet point, but you’ll have to admit it is the first solution that comes to mind to a lot of developers. Additionally, it is a very simple solution. The biggest issue with this solution is with sharing a project over several slns. Unfortunately, any bit of code in those shared projects is easily changeable from multiple slns; therefore it is very easy to break several slns in one fell swoop. Secondly configuration management goes out the window because every time a sln is compiled, each shared project gets a new version that bypasses any sort of change management.

## Second attempt ending in failure:

* **Manage all 3rd party and internal dlls by putting them in a \[sln\]\\bin folder.**

This solution complicates things slightly (in a positive way) by requiring each sln to use a proper release of all internal dlls; therefore you are able to have some degree of configuration management. However, this solution failed for us because of one simple fact: TFS does not track binaries well. We never ran into this weakness with the first solution because all of the 3rd party dlls were set-and-forget. They never changed after setting the initial reference. The internal dlls however, would change daily, or even hourly. At first this seemed like the perfect solution, however all sorts of strange errors started occurring. One person would get latest and everything would work, but another person would get latest and have errors. TFS simply could not tell if you needed a new version of the dlls in the /bin folder. Sadly, even a “clean all" and "get specific version" didn't fix things a lot of the time.

## Third attempt ending in Success:

* **Build a custom package management system.**

Our custom package management system worked thusly: We created a network share. For each logical release (i.g. MS EntLib, Internal.Common.Util) we created both a \[networkShare\]\\\[package\]\\LatestRelease folder and a \[networkShare\]\\\[package\]\\Release_\[version number\] folder. We then created a console EXE with a bunch of options that would: 1) go and grab all of the latest dlls for all projects and dump them into one pre-defined “latest” folder on the developer PC and 2) Recreate the “releases” tree structure on the developer PC. This way, developers have the ability to drink from the fire-hose (the latest folder) or go for set releases (from the releases folder tree). TFS is not tracking dlls at all. Rather, we are relying on an absolute path file reference. Additionally, calling this executable becomes a build task on the CI server.
This solution isn't perfect. Namely, it relies on developers to remember to run the executable from time to time. Additionally, there are potentially some versioning scenarios that could occur between packages that expect a different versions of sub dependencies. However that issue never manifested itself in our environment.

## Nuget is not the final answer for teams using TFS
<del>I've been following the Nuget dev list closely, and Nuget is considered to be a development time dependency resolver only, not a build time resolver. This means that if you use TFS to track your Nuget package folders, you could still run into dll versioning issues.</del>

### Update (4/17/2011)
Nuget team member David Ebbo has blogged that [functionality has been added to allow use of Nuget without committing the packages folder to source control.](http://blog.davidebbo.com/2011/03/using-nuget-without-committing-packages.html)

### Update (4/30/2011)
According to Phil Haack, [Nuget is going to be getting official support for non-committed packages.](http://haacked.com/archive/2011/04/27/feedback-request-for-using-nuget-without-committing-packages.aspx)

### Update (3/9/2013)
Obviously, Nuget package restore is a thing now, so this post should be considered for historical purposes only.
