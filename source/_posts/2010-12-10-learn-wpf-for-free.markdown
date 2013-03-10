---
layout: post
title: "Learn WPF for Free"
date: 2010-12-10 00:48
comments: false
categories: development 
---
In my [last WPF related post](http://nerditorium.danielauger.com/blog/2010/08/10/time-until-productivity-in-wpf/) I spoke a bit about my WPF learning experience. I was fortunate enough to have an MSDN Universal subscription and any book I wanted via my employer as I went down the path. Unexpectedly, I recently received an email from a reader who wanted to learn WPF on a budget of $0.00. After thinking for a bit, I came to the conclusion that WPF can be learned without spending any money (assuming you have a computer that can run the tools). Below is a roadmap on how to do so.

## Get the tools for free
Visual Studio Express, which is able to create WPF apps can be found [here](http://www.microsoft.com/express/Windows/)

If you need any other tools, such as SQL Server Express, you can most likely find them via the [Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx)

## Learn the Framework
Between MSDN and the community, there is more than enough well-written documentation out there to help one become an expert on the WPF framework itself. In his book, “Advanced MVVM”, WPF expert, Josh “The Maestro” Smith, recommends the following documents to come up to speed with the WPF framework:

* [Introduction to WPF](http://msdn.microsoft.com/en-us/library/aa970268.aspx) 
* [WPF Architecture](http://msdn.microsoft.com/en-us/library/ms750441.aspx) 
* [A Guided Tour of WPF](http://joshsmithonwpf.wordpress.com/a-guided-tour-of-wpf/)
* [Customize Data Display with Data Binding and WPF](http://msdn.microsoft.com/en-us/magazine/cc700358.aspx) 
* [ItemsControl: ‘I’ is for the Item Container](http://drwpf.com/blog/2008/03/25/itemscontrol-i-is-for-item-container/)

A lot of the information in the above links is difficult to absorb, but I think it is very worthwhile to go through the material, **and work through the examples**, at least once. If some of the documents are unclear, you can always go back to them as you learn more and need more clarification.

## Learn MVVM
Many people blow off MVVM as “the latest popular design pattern”, but learning MVVM is essential to working with WPF. This is because MVVM is a natural pattern to use considering the way databinding works with WPF. Yes, you can write WPF apps using tried-and-true code-behind and click event handlers like people did with winforms, but you’ll be doing yourself a disservice.

When learning MVVM, the first place to look is [this very simple video](http://blog.lab49.com/archives/2650) by the Jason “The Enigma” Dolinger, where he explains what MVVM is, and what the pattern’s strengths are.  

The next place I would look is the [MVVM In the box](http://karlshifflett.wordpress.com/2010/11/07/in-the-box-ndash-mvvm-training/) training by Karl “The Educator” Schifflett. 
 

As a lesson summary, an in-depth overview of MVVM written by Josh Smith can be found [here](http://www.microsoft.com/express/Windows/). 

## Apply what you’ve learned
While there is no WPF “best practices” sample that I am aware of, I think the following can get one to see how WPF fits into an application architecture.

* [Building a Desktop TO-DO application with NHibernate.](http://msdn.microsoft.com/en-us/magazine/ee819139.aspx)  
* [Understanding the MVVM Pattern](http://channel9.msdn.com/Events/MIX/MIX10/EX14)
* [Build Your Own MVVM Framework](http://channel9.msdn.com/Events/MIX/MIX10/EX15)

Not strictly MVVM, but worth looking at as application and framework samples:

* [PRISM](http://compositewpf.codeplex.com/)  
* [Caliburn Micro](http://caliburnmicro.codeplex.com/)   
* [Caliburn Micro Soup To Nuts Series](http://caliburnmicro.codeplex.com/documentation)  
* [MVVM Light](http://mvvmlight.codeplex.com/)

## Keep Learning
Read Blogs! Search out WPF related blogs. There are enough out there to fill your news reader every day. Pete “6510” Brown  puts out a Windows Client roundup frequently which is a good starting point.

Read and participate in the knowledge dump at [StackOverflow](http://stackoverflow.com/questions/tagged/wpf).
At first you may find that some of the questions are the same things you are wondering about. After awhile, you will find that you can answer some of the questions. As you answer questions, you’ll reinforce what you’ve learned.

Share
Software development is still largely a folklore based discipline. It is your duty to share what you have learned in the best way you know how.
