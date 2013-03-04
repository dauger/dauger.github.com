---
layout: post
title: "Octopress: Banishing a Category to Its Own Page"
date: 2013-03-03 18:11
comments: true
categories: [meta, octopress]
---
Because this blog is made of up "[link posts]({{ root_url }}/blog/categories/links)" and "original content" posts, I wanted to make two customizations to Octopress to keep original content from getting lost under the volume of link posts.<!-- more --> The modifications I wanted to make were:

1. Hide all link posts from the index page.
2. Create a page just for link posts and provide navigation to it via the nav bar.

I wasn't sure where to start because I am new to Octopress. My google-fu was questionable due to my lack of understanding Octopress' terminology.

## Hiding Link Posts from the Index Page
Out of the two things I wanted to do, this was the easiest to find help with. I found this post about [hiding posts from the octopress front page](http://arshad.github.com/blog/2012/05/10/recipe-hiding-posts-from-the-octopress-front-page/) almost right away.

The TLDR version of that post is: you need to assign a category to the posts you want to hide and then alter the pagination plugin to exclude that category.

## Creating a Page Just for the Hidden Category and Providing a Nav Link to It
This one tripped me up for a bit. I quickly went down a black hole searching for things like "octopress create category page".

I couldn't find quite what I was looking for so I starting searching for other Octopress based blogs to see if anyone had done such a thing. After I came across [this](http://time.to.pullthepl.ug/blog/archives/) blog, the answer was obvious. Octopress already creates category specific pages. In order to provide a nav link to the category, I simply needed to edit the _source/custom/navigation.html file like so:  
```html
<ul class="main-navigation">
  <!-- other nav links -->
  <li><a href="{{ root_url }}/blog/categories/links">10,000 Links</a></li>
  <!-- other nav links -->
</ul>
```
