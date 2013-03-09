---
layout: post
title: "Your ASP.NET.* Project is Not Just Your UI Layer"
date: 2011-11-30 12:54
comments: false
categories: development
---
In [this](http://lostechies.com/jimmybogard/2011/11/28/dealing-with-transactions/) post by Jimmy Bogard about “dealing with non-transactional operations that must happen if some transaction succeeds,” the often embraced, but sometimes criticized, [Session Per Request](https://www.google.com/search?gcx=c&sourceid=chrome&ie=UTF-8&q=session+per+request) pattern (aka Transaction Per Request), came under fire in the comments.

<!-- more -->

{% img /images/postimages/infrastructure_transactions_comments.png %}

I’ve had this conversation with other developers who have raised similar concerns before, and the reason brought up against going with this pattern is based off of the notion that the “Web” project must not orchestrate or indirectly know about the other layers of the application because it is the “UI” layer.

The fact is, that the web project houses two conceptual layers:

1. It houses the UI layer for the application.  
2. It houses the entry point / bootstrapping for the infrastructure of the application. It is the application.

I am perfectly fine with the plumbing of the web project directly managing transactions. Some part of the application must manage this, and I a believe that the it should be pushed as far out to the seams of the application platform as possible.