---
layout: post
title: "Perception is Reality - .NET OSS is Getting Better"
date: 2013-09-23 20:31
comments: true
categories: .NET OSS 
---
This post is a response (not a rebuttal) to: 
[Perception is Reality - .Net OSS is DOA](http://amirrajan.net/meta/2013/09/19/perception-is-reality-dot-net-oss/) 
by [Amir Rajan](https://twitter.com/amirrajan)

*note: I intentionally heaven't read many of the linked blog's comments so that
I could get my own thoughts down. Therefore, I may be repeating some
things that have already been said.*

#tl;dr
In my experience, OSS usage has risen slightly among internal corporate teams over the past few years. 
However, OSS usage has really taken off among other types of teams. Additionally, there are things that Microsoft
could do to increase OSS adoption across the board.

## OSS in the Enterprise / Big Business Projects
Although there is a long way to go when it comes to getting enterprise .NET 
shops to embrace OSS, I've definitely seen an increase in acceptance over the 
past three years. This is largely due to a number of factors such as: NuGet 
being an integral part of the current Visual Studio experience, the fact that 
MS is now including OSS libraries as a part of default templates, and the fact 
that MS has open sourced many of the frameworks that are central to running .NET 
on a server.

There is a caveat here: in my experience, the items above have not automatically 
made enterprises OSS friendly. Microsoft's consulting division isn't walking 
into enterprises saying "embrace open source." (in fact I've heard a couple say 
the opposite recently) However, the above items give OSS advocates more 
evidence when trying to persuade stakeholders to use OSS packages. I've 
personally seen an organization go from "we won't use OSS" to "let's use some 
well known packages." And yes... I'm even talking about packages that aren't MS
backed. 

In the past, open source would have just been rejected as being "open source" 
in the environments I'm talking about. Now the hesitation I'm seeing revolves 
largely around knowing how to vet and choose OSS packages. People are worried 
about relying on projects that may die off suddenly - especially on larger / 
expensive projects. Obviously even the cautious know that just because something 
is from Microsoft doesn't mean it won't be abandoned either. However, I'm still 
seeing this as a significant psychological hurdle when it comes to using 
OSS in these environments. 

## OSS in Design Agencies and Direct to Business Projects
If you aren't familiar with these sectors, I'll do a probably offensive
job of explaining them below.

**Design Agencies** are entities that will pitch, design (and possibly UX and 
develop) a software solution for companies that don't have a public-end-user savvy 
development group.

*Example of an agency project: A big box retailer needs a highly
interactive mini-site for their holiday sale.*

The interesting thing about agency projects is that they can often be 
for clients that would otherwise fall into the mainstream corporate / 
enterprise category. However, agencies rarely have to follow the same technology 
rules that internal teams do. In fact, they are often hired to bypass the 
involvement of an internal team. What's also interesting is that I'm seeing an 
increase in requests to implement things that would have traditionally fallen 
under their internal dev group (APIs, data migrations, etc...). 

**Direct to Business** are typically clients that do not have a dev shop, or they have 
a dev shop that can't meet current demands by themselves. 

*Example: A medical research company needs a custom application to
manage research protocols.*

### Use of OSS in Agency and DTB projects
In my experience, stakeholders rarely balk at using OSS in these situations. The team 
decides what is the best way to deliver software on time and under budget.

## How Microsoft Could Improve on Promoting OSS
> Microsoft is trying to change the mainstream (corporate) .Net culture. They 
> are genuinely trying to promote open source software, without bias. And I can’t 
> thank people at Microsoft (like Glenn Block, Scott Hanselman, and Jon Galloway) 
> enough for busting their asses trying to push open source initiatives.

I completely sympathize with this quote. I believe that important people in DevDiv
are making a huge difference in OSS adoption, but there is still a lot
of work to do. 

> It *doesn't* have to be this way.

I think the following enhancements *could* be made at Microsoft 
to facilitate the adoption of OSS in the .NET world:

### Broaden the Audience of Evangelism and Align Evangelism Efforts with the Consulting Arm.
OSS evangelism needs to be *extended* outside of the audience that is reading blogs
like this or following Hanselman, Block, and Galloway on Twitter. One important slice of 
this audience are decision makers on corporate / enterprise teams such as 
architects, infrastructure folks, and PMs. Although I think
MS has been doing a good job of reaching these folks at events like
VSLive! and TechEd, I think there is a more direct line to these people:
a) The MS Consulting arm, and b) Patterns and Practices. Although these
people may not participate in our larger community, they undoubtedly cross paths with MS
consultants and the PnP group.

*As a related aside: you'd really be surprised how effective events like
VSLive! are for promoting open source. I've seen someone arrive at the
conference with a decidedly anti-Git attitude but leave the conference
open to it because almost all of the presenters (including Microsoft people) 
were using it in their talks.*

### Stop Handcuffing the Free Version of VS and Remove Platform Restrictions
At the very least, the express version of Visual Studio should support
plug-ins. Additionally, any new framework libraries should be [free of platform restrictions](http://haacked.com/archive/2013/06/24/platform-limitations-harm-net.aspx).

Along these lines - anything new on the server side that could work on
Mono should be made so that it works on Mono.

### Don't Reinvent the Wheel; Invest in Existing OSS Projects
Something like the [NHibernate vs EntityFramework situation](http://efvote.wufoo.com/forms/z7x3p9/) 
should never happen again (no offense to the bright EF developers). This was a really
horrible event in .NET OSS history. NH is basically dead now, and we are left with something that 
is still playing catch-up.

### Continue Backing Established Projects but Don't Leave the "Little Guys" Out of the Picture.
This may be a contriversial opinion, but I think Microsoft needs to
continue to "back" projects. I don't think anyone will argue that
throwing resources behind node.js has been anything but good for us.

As far as keeping the little guys in the picture goes, this could be a
bit trickier and I don't have a slam-dunk idea at the moment. Maybe
MS needs to open up the MVP program to be more OSS centric (instead of
boots on the ground at your local user group centric), or maybe they need to 
do an emerging technologies review every once in awhile like ThoughtWorks' 
[Technology Radar](http://www.thoughtworks.com/radar).

### Continue Extending Azure Support to Linux and Other Languages and Platforms.
You might ask yourself why Microsoft would want to make Azure less .NET
and Windows focused, but I think it is clear that the world
won't be Windows dominated again anytime soon. Additionally, making
Azure friendly to PHP, Node.js, Python, Ruby on Rails, etc... can bring
those developers at least a little bit closer to our community. This in
turn should help our community rejuvinate with new ideas.

## It Could Get Better or Worse at this Point
I think there are some significant challenges ahead for those inside of
Microsoft who wish to promote OSS. I personally think getting the
consulting arm onboard is going to be a large hurdle that could make or
break things. Also - I haven't really done enough thinking about the
recent reorg to foresee how it might affect things.
