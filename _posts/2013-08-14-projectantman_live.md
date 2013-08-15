---
title: "projectantman.com is online!"
layout: post
tags: 
 - programming
 - jekyll
 - ruby 
 - codeschool
---

So after fiddling with the CSS and trying to get the archive page to display the dates organized by year, I finally figured out a work around. This is the first actual post I am writing in Markdown format. All the previous ones were already written and were just copied and pasted onto a page. Going forward, these posts will have more logical sense since I know people are going to read it!

There were a couple things I really struggled with:

1.  the css to indent the month and date [on the archive page](www.projectantman.com/archive/)

2.  getting the archive page to organize by year using the a ruby extension [here](https://gist.github.com/jdaihl/1200663)

For problem 1, I tried to add css <code>padding-left:</code> to the code to the class 'this' as shown below because I ran my site on a local server and clicked 'inspect element.' It showed that the class 'this' was created for the specific archive posts. So I added this code below:

    ul .this {
        padding-left: 5em;
        }


But it wouldn't change anything so I just took out the <code>padding-left: 0px;</code> declared on the ul css. This put an automatic indentation on all unordered lists by default, which is the current state it's in now. 

For problem 2, I couldn't understand how the ruby extension worked. I tried to look at some of the other blogs using jekyll engine [here](https://github.com/mojombo/jekyll/wiki/Sites). It was taking too long to figure it out so I found another workaround that didn't use any kind of ruby extensions. I found an alternate solution on another site, but I forgot the reference. For the life of me, I couldn't get the first header to post the current year, so it was manually entered. 
  
    <section id="archive">
    <h2>2013</h2>
      {.% for post in site.posts %}
      {.% unless post.next %}
    <ul class="this">
      {.% else %}
      {.% capture year %}{.{ post.date | date: '%Y' }}{.% endcapture %}
      {.% capture nyear %}{.{ post.next.date | date: '%Y' }}{.% endcapture %}
      {.% if year != nyear %}
    </ul>
    <h2>{.{ post.date | date: '%Y' }}</h2>
    <ul class="past">
      {.% endif %}
      {.% endunless %}
        <li><time>{.{ post.date | date:"%d %b" }}</time>&nbsp;&nbsp;<a href="{.{ post.url }}">{.{ post.title }}</a></li>
      {.% endfor %}
    </ul>
    </section>
 
Oh well, I am happy to have it up and running at the least. It's time to add some features as time goes on and work on some other projects!
  