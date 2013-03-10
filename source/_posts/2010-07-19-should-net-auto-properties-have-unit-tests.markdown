---
layout: post
title: "Should .NET Auto Properties Have Unit Tests?"
date: 2010-07-19 12:16
comments: false
categories: [development, tdd]
---
{% img left /images/postimages/testing_vader_scaled_thumb.jpg %}
Should .NET auto properties be unit tested? It is very easy to argue that testing auto properties falls into the “testing the .NET framework” smell and is a waste of time. However, experience has shown me otherwise. This is something that I’ve gone back and forth on many times since auto properties were introduced. For the time being, I think I’ve reached a conclusion. That conclusion is yes. <!-- more -->

I typically do two types of testing: 1) Test Driven Design, and 2) Test while/after unit testing. Let’s consider these two scenarios.

When doing test driven design, there is no question. You should write tests for your auto properties. Test driven design is not about testing; it’s about design. The rule of thumb is that you don’t write any code without a test dictating its need. Case closed (in general).

Things get trickier when doing test while/after unit testing. This type of testing is more about creating a test harness. When writing tests after the fact, I know that the property is implemented using auto properties. Therefore, if I am taking a white box approach, I know that my implementation of the encapsulated property is simply the .NET framework. Following that line of thought, testing auto properties is testing the .NET framework. However, I tend to view test while/after testing as a test harness of the public contract. This is black box testing. A public property is an encapsulation, and therefore it should be tested. It’s not uncommon for an auto property to be converted into a regular property as an application lives on. I’d have to say that I would want a test there to capture any publicly facing change in that encapsulation
