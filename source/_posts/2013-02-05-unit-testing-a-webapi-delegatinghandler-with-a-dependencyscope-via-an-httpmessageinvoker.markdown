---
layout: post
title: "Unit Testing a WebAPI DelegatingHandler with a DependencyScope via an HttpMessageInvoker"
date: 2013-02-05 20:49
comments: true
categories: 
---
 I've been working with ASP.NET WebAPI on a day-to-day basis for about seven months now, and I have to say that I really appreciate how testable it is. Although the self-hosting capability of WebAPI seems like an obvious way to facilitate a test-first workflow, I personally favor two other methodologies.

* Testing DelegatingHandlers in isolation via HttpMessageInvoker as outlined here: [Unit Testing Message Handler in Asp.net WebAPI](http://restoncode.azurewebsites.net/blog/2012/10/16/unit-testing-message-handler-in-asp-dot-net-webapi/)

* Testing "everything" via an in-memory HttpServer as outlined here: [ASP.NET Web API integration testing with in-memory hosting](http://www.strathweb.com/2012/06/asp-net-web-api-integration-testing-with-in-memory-hosting/)

Testing with dependencies is straightforward with in-memory hosting because it is obvious that you can provide the HttpServer instance with an HttpConfiguration object containing an IDependencyResolver. However, when it comes to testing handlers via an HttpMessageInvoker, it is not entirely obvious or discoverable as to how you can wire up an HttpConfiguration (and therefore an IDependencyResolver).

Here is the secret sauce: you can add an HttpConfiguration to a request object via a "stringly typed" *"MS_HttpConfiguration"* property on the HttpRequestMessage object.

``` csharp  
[TestMethod]
public void SomeHandlerTest()
{
   // ... other test setup
   // ... set up handlerUnderTest including inner test handler

   request = new HttpRequestMessage(HttpMethod.Get, serverUrl + "/resource/1?someParam=foo");
   request.Properties["MS_HttpConfiguration"] = MethodThatReturnsAnHttpConfigWithDepResolver();
            
   invoker = new HttpMessageInvoker(handlerUnderTest);

   var response = invoker.SendAsync(request, new CancellationToken())
                                  .Result;
   // ... asserts
}
```