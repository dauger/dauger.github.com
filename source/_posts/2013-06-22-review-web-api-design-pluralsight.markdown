---
layout: post
title: "Review: Web API Design (Pluralsight)"
date: 2013-06-22 23:24
comments: true
categories: development 
---
Apigee's [API Design](http://apigee.com/about/api-best-practices/api-design-third-edition) webinar may have just become my second choice as the go-to resource for bootstrapping developers new to HTTP/REST/Web API design. Shawn Wildermuth's new [Web API Design](http://wildermuth.com/2013/6/19/Designing_APIs_for_the_Web) Pluralsight course is probably the most complete and non-biased resource for beginners on the topic. Shawn does a great job of distilling in 2.5 hours what took me countless hours to glean via scouring through blog posts and RFCs. He also carefully discusses the trade-offs of several design choices without falling into the RESTafarian vs. Pragmatic REST trap. The course also provides one of the best explanations of the most common OAuth flow (Facebook, Twitter, etc...) that I can remember.

My only minor gripe with the course is this: HATEOAS is mostly framed as a way to be friendly to humans (meaning: a way to make an API discoverable for developers). The possibilities of facilitating discoverable machine-to-machine communications isn't really explored (vocabularies, API DNAs, etc...). However, I share his assertion that HATEOAS is still in the academic state. I will say that he does a good job of covering HAL and Collection+JSON in regards to this topic.

Bottom line: point developers who are new to Web APIs to this course.
