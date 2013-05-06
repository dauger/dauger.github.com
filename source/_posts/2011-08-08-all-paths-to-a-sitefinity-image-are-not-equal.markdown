---
layout: post
title: "All Paths to a Sitefinity Image are not Equal"
date: 2011-08-08 15:41
comments: true
categories: development
---
Recently, while doing a performance pass through a Sitefinity 4 application, I noticed that a public facing page had an unusually slow load time. Of course, the first thing I did was open up Firebug to see where the time was being spent. To my surprise, the majority of the time was spent waiting for the initial response from the server. After a little digging, I narrowed down the time-sink to a custom widget that pulled images from a Sitefinity image album. In particular, the query to figure out which images to display was the source of slothness. <!-- more -->

A few things to note:

* There were about 250 image albums in the CMS (all but 5 or so of them were empty at the time of discovery, however).
* There were roughly 30 images in the album we were querying against.
* When the original query was written, there were only a few images in the system, and that is why the issue wasn’t apparent right when the query was written.
Here’s an approximation of the original call to retrieve the images through the Sitefinity API:

``` csharp
var libManager = LibrariesManager.GetManager();
 
var imagesFromFoo = libManager.GetImages()
        .Where(i => 
            i.Album.Title.Equals("Foo") 
            && i.Status == ContentLifecycleStatus.Live)
        .ToList();
```

In this bit of code, we are querying for all images that belong to the image album named “Foo”. Note that the query is structured in a way where we query through the image object to determine what album it belongs to.

The above query took about 2 seconds to return roughly 30 Sitefinity Image objects. This would not do. Therefore, I took to tweaking the query. I tried several different things while maintaining the original approach, but since Sitefinity’s LINQ provider isn’t a complete implementation, I couldn’t make much headway.

I eventually decided to rethink the approach and query for the images by going in through the album instead of going through the image object.

``` csharp
var libManager = LibrariesManager.GetManager();
 
var imagesFromFoo = libManager.GetAlbums()
        .Where(a => a.Title.Equals("Foo"))
        .First()
        .Images.Where(i => i.Status == ContentLifecycleStatus.Live)
               .ToList();
```
This reduced the query time down to about .2 seconds.
