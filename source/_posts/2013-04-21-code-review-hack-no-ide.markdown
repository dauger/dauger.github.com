---
layout: post
title: "Code Review Hack: No IDE"
date: 2013-04-21 20:21
comments: true
categories: development
---
## I'm a fan of code reviews 

I've typically used code reviews for the following benefits:

1. As a code quality measure. I think that code reviews rank right up there with TDD as a code quality practice. When I'm calling the shots on a project, I like to have "code review" being a requirement of something being considered "done".
2. As a conversational learning experience (which can benefit both the reviewee and the reviewer).

When reviewing code as a quality check, I highly recommend that you use any tools at your disposal. In .NET land (at least for me) that means Visual Studio and Resharper. However, when doing more of a conversational code review for learning purposes, I've come to find that it can be handy to do the review without any tooling. To illustrate this point, I want to tell you a story about last Friday.
<!-- more -->

## Last Friday

Last Friday was my annual code review at work. At [The Nerdery](http://nerdery.com), all developers get a special code review as part of the annual review process. This code review is not about catching immediate code quality issues. Rather, it is a conversation about some code that you've written in the past. This is so strengths, areas of improvement, what you've learned since, and overall skill can be assessed. Because the code under review can be "old", the conversation about the code can be more important than evaluating the code on its own merits. 

The code review tool we use is custom built. It is not entirely unlike [Crucible](http://www.atlassian.com/software/crucible). The tool's focus is about reading code and adding comments and tasks to possible issues. It has syntax highlighting, but it has no other IDE or advanced text editor features. 

## Reviewing and talking about code without the crutch of tooling can be a humbling experience

So... back to last Friday. I'm in my annual code review with one of my trusted peers. We've both been doing .NET development since .NET was released. We're reviewing an HMAC request signing WebAPI message handler I wrote about 3 months ago. We come across this:

```csharp
 var dateUtcHeader = request
 		.Headers
 		.FirstOrDefault(x => x.Key.ToUpper() == CustomHeaders.DateUtc.ToUpper());

            try
            {
                // Prefer the use of the date-utc header over the Date header
                if (dateUtcHeader.Value != null)
                {
                    // Try to parse the date as RFC1123 date
```

The conversation then goes something like this:

Peer: "Just curious... so why don't you need to check if the return value of FirstOrDefault is null?"

Me: "Huh... Good question!"

This was followed by us spewing out a few lines of thought, only to backtrack. To be clear, he wasn't trying to ding me. The underlying context here is that FirstOrDefault often requires a null check, but Resharper would have let me know if it was needed.

Needless to say, this was a pretty humbling inquiry, and it lead to conversing about code (which was the point of the entire exercise).

## Aftermath
As any curious programmer would, I later went back to my IDE to solve the mystery. What I found makes complete sense once you take a deeper look at the types involved.

I know what some of you are thinking right now. If I would have used the full type in the declaration instead of var, things would have been much clearer. Here is what it would have looked like:

```csharp
KeyValuePair<string, IEnumerable<string>> dateUtcHeader = request
	.Headers
	.FirstOrDefault(x => x.Key.ToUpper() == CustomHeaders.DateUtc.ToUpper());
```

This might be the reveal for some people. If not, here is the rub: [KeyValuePair<TKey, TValue>](http://msdn.microsoft.com/en-us/library/5tbh8a42.aspx) is a Structure, and therefore cannot be null.

Before someone links to it: [Does Visual Studio Rot the Mind?](http://www.charlespetzold.com/etc/doesvisualstudiorotthemind.html)