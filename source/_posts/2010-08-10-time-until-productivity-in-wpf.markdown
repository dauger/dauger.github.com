---
layout: post
title: "Time Until Productivity in WPF"
date: 2010-08-10 23:58
comments: false
categories: development
---
{% img left /images/postimages/kingkongtorso_thumb.jpg %}
One of the things I see over-and-over-again when reading about teams that are deciding if they should adopt WPF or not is the fear of the learning curve, and the worry that they will not be productive for a huge period of time. Given that I’ve recently become productive in WPF myself, I thought I would talk about my experience in this area. <!-- more -->

A little background about myself: I would consider myself to be your average mid-30 year old ALT.NET developer. I got my start programming BASIC and 65xx assembly as a kid in the early 80s on a Commodore 64, got my first programming job doing Java in the late 90s, and started using ASP.NET in the late 1.0 beta days. Programming is one of my hobbies, but I am not the type that stays up all hours of the night working on my pet OSS project. I am also not a “computer scientist” or language wonk. However, I am passionately interested in software craftsmanship. [S.O.L.I.D.](http://en.wikipedia.org/wiki/Solid_(object-oriented_design) is prominent in my tool belt.

My attention was first turned to WPF in the early fall of 2008. My group was facing a large desktop project. The question came up as to if we should go with Winforms or WPF. No one on the team had any practical Winforms experience, so the initial reaction was that we should go with WPF since Microsoft had made it clear that it was the future of Windows desktop development. However, we all had heard rumblings about how difficult WPF was. That being the case, each member of the team created a very small drag-and-drop application to test the waters. The general consensus was that if you ignored the more advanced features of WPF, it was just as easy as Winforms drag-and-drop + code behind development. Mind you, we did not want to do that sort of development, but it became apparent that that style of development would be equally painful using either framework. Note that at this time, I really had no idea how to make a real application using WPF, but I did understand the very basic concept of how XAML markup changed the game from Winforms development.

**Estimated time spent learning WPF during this period: 8 hours.**

After the initial decision making process, I returned to ASP.NET and WCF development. The WPF project didn’t really get started until spring 2009. I was not slated to work on the project, but I was enlisted to help decide the preliminary architecture. Once I was given that task, I began to look around for application frameworks, or at the very least, some patterns that had momentum behind them. At this time, I learned about the MVVM pattern via the still insightful [Jason Dolinger video](http://www.lab49.com/wp-content/uploads/2011/12/Jason_Dolinger_MVVM.wmv). It really seemed to click in my mind so I began looking for an application framework to support this pattern. I did not find a mature application framework per say, but I did come across PRISM. There were a few other budding frameworks at the time, but [PRISM](http://compositewpf.codeplex.com/) was way ahead of the game. Therefore, we decided to go with PRISM using the MVVM presentation pattern on the client side of the application. Once that decision was made, I was back off the project and doing other things. I did however start following a few WPF blogs at this time, but I did not do any WPF coding.

**Estimated time spent learning WPF during this period: 8 hours.**   
**- Total estimated time: 16 hours.**

This July, my schedule freed up and I was put on the project 50% of my time. I was tasked with a reporting interface that had to show a list of available reports and then dynamically show parameter UI elements depending on which report was selected.

As soon as I was assigned to the project, I got a copy of [WPF in Action with Visual Studio 2008](http://www.manning.com/feldman2/). I read the book half the day during my work week, and then a few hours each night at home. As someone who learned programming through [type-in](http://en.wikipedia.org/wiki/Type-in_program) programming, I made sure that I recreated all of the samples myself. Also at this time, I grabbed the latest version of PRISM and took a peek at the examples.

**Estimated time spent learning WPF during this period: 30 hours.**   
**- Total estimated time: 46 hours.**

The first week of actual development was pretty brutal. MVVM was not the problem. PRISM was not the problem. XAML and databinding is where I was banging my head against the wall. It kind of worked like HTML, and it kind of didn’t. That first week was pretty aggravating, but pretty much every problem I encountered was just an internet search away.

**Estimated time spent learning WPF during this period: 30 hours.**  
**- Total estimated time: 76 hours.**

I became productive after that first week. I’ll be the first to admit that I don’t intimately know how WPF works behind the scenes (like I do with ASP.NET). However, I do think that I became productive within a reasonable amount of time.

Looking back, I can safely say it took me about **80 hours** to go from expert ASP.NET programmer to productive WPF programmer.  That being said, I do not know how long it would have taken me to go from expert ASP.NET programmer to productive Winforms developer. Something tells me it wouldn’t have been a number that would have made us use Winforms instead of WPF.
