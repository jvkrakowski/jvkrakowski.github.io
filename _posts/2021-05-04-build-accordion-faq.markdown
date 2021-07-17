---
layout: post
title: "Building an FAQ Accordion with JQuery"
description: "Transform that long FAQ section into a condensed, consumable format with a bit of jQuery"
date: 2021-05-04
featured_image: "https://i.ibb.co/rxjYSHY/how-write-content-better-reading.png"
author: "J.V Krakowski"
tag: [jquery, html, css, coding, accordion]
excerpt_separator: <!--more-->
categories: [Coding]
---

Long, drawn-out content is a pet peeve of mine. After a decade of evaluating websites, does anyone blame me? When you imagine creating websites, endless scrolling isn't something you think will be a problem. I learned to appreciate those "back to top" buttons if nothing else.

<!--more-->

I acknowledge on a minor level that long content is sometimes unavoidable. Most help sections are among those exceptions. In those cases, there's such a thing as an accordion effect to help condense content into a consumable format. Today, we're going to learn how to build a simple one with jQuery.

## Using JQuery vs. Javascript

When we want to add interaction to a website, we use frameworks and libraries to add effects that appeal to visitors. Many people have come to expect it as a standard practice. For example, we automatically know to expand menus when we see a downward arrow.

Most interactive elements are built with jquery as a standard practice. Not only is it simpler to code, but it also saves on lines of code. However, that doesn't mean that javascript isn't worth learning before touching jquery.

Javascript is the programming language many frameworks were built on. As I've told many new developers, "Learn the basic languages first, and then you can learn the frameworks with ease." When you know javascript, learning jquery is like riding a bike.

While I encourage everyone to learn javascript, jquery has an elegance to it that javascript lacks. It helps us simplify everyday web tasks. Many people find it easier to understand than javascript, which is why we're starting with it today.

## Before We Start

If we were coding for an actual project, our first task would be determining whether we needed this effect. While it's a nice touch, too many effects are a distraction. Finding the right balance is key to good design.

The right balance depends on your client's audience. The only way to discover what they like is through research. Remember that when you're working on your next project.

## Our Tools

The tools you'll be needing are:

* jQuery 3.5.1
* Code Editor
* Dummy content

Generally speaking, choosing a code editor is a personal matter. Everyone has their preference for one reason or another. However, as a newbie, I recommend selecting a basic, stripped-down code editor that won't help you along. It encourages you to learn the code rather than depend on a program to tell you what could come next.

If you're using Windows, I recommend [Notepad++](https://notepad-plus-plus.org/) as a code editor. For everyone else, you can check out [Atom](https://atom.io/) with autocomplete disabled. If you have any suggestions for code editors, comment below and let us know!

There are many resources to create or download dummy content. Since we need a few sentences, though, I recommend [Lipsum](https://www.lipsum.com/), a generator that gives paragraphs of nonsense Latin as a placeholder for projects. Make sure to bookmark that site because you might find yourself using it again.

## Setting it Up
To set up your work environment, we're going to create a folder on your desktop. You can name it anything you want, but it would be best to keep it simple. We're going to save all our files to that folder.

I like to open the folder and then minimize it on my taskbar. It's a personal preference, so you can do whatever you want at this point. Just don't forget to [download jquery](https://jquery.com/)!

There's also an option to use a CDN, which will give you a direct link that will work just as well. The acronym **CDN** stands for *Content Delivery Network*. It makes it easier for projects like jquery to deliver content to users without the need to download the files.

You register for your CDN link and then copy and paste the link into the head section of your web page. Be warned, though; you'll need an internet connection to make your jquery work!

## Basic CSS/HTML

Right now, we're going to open our code editor to create the HTML that will display the jQuery code we make. Since this isn't a tutorial on how to code HTML, I'll slap the code right here:

```HTML
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" type="text/css" href="style.css">
    <link rel="stylesheet" type="text/css" href="normalize.css">
    <script src="https://code.jquery.com/jquery-3.5.1.min.js" integrity="sha256-9/aliU8dGd2tb6OSsuzixeV4y/faTqgFtohetphbbj0=" crossorigin="anonymous"></script>
    <script src="ask.js"></script>
    <meta charset="UTF-8">
    <meta name="description" content="Free Web tutorials">
    <meta name="keywords" content="HTML,CSS,XML,JavaScript">
    <meta name="author" content="John Doe">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ask | Built with JQuery</title>
</head>
<body>
    <div class="wrapper">
        <h1>Ask &mdash; Demo</h1>
        <p>A basic, no frills FAQ built with jquery.</p>
        <input class="open" type="button" value="Open All">
        <dl class="questions">
            <dt>Question 1</dt>
            <dd>Answer</dd>
            <dt>Question 2</dt>
            <dd>Answer.</dd>
        </dl>
    </div>
</body>
</html>
```

If you look at the head section, you'll notice several essential bits of code. The **<link>** code tells the browser where to find the stylesheets. There are two stylesheets, but you don't need the second one. Normalize is a stylesheet that unifies how browsers display web elements. While useful, it's not necessary.

The **<script>** code tells the browser where to find the jquery. There are two sets of **<script>** code; one for the main jQuery and another for our bit of code. Make sure to have both!

The **<dl>** element defines a description list. That is the web element we're going to call in our jquery file. Please give it a bit of content; otherwise, you won't see a change.

Again, we're not learning to code HTML. Copy and paste the code into your index file. Speaking of which, you need to create an index file and save it to your folder.

## The JQuery

Now, we're going to concentrate on creating the script that will make this accordion work. Here is the full code:


```jquery
$(function () {
  var Speed = 800;
  $('.questions dd').hide();
  $('.questions dt').click(function () {
    $(this).next(".questions dd").slideToggle(Speed);
    $(this).toggleClass("expanded_img");
  });
    $('.open').click(function (){
        $('.questions dd').slideToggle('.questions dt');
        $('.questions dt').toggleClass("expanded_img");
        $('.open').val('Open All');
        $('.open').toggleClass('close');
        $('.close').val('Close All').removeClass('.close');
    });
});
```

The above code is simple, and I purposefully made it that way. if you look at the first line of code, you're going to see this:

```jquery
$(function() { ... });
```

That code is the short-hand for the following:

```jquery
$(document).ready(function() { ... });

```

Both of them ensure that the script is loaded once the DOM elements are ready to be used. The phrase "DOM elements" refers to the HTML on a web page. We need it to operate that way because the script won't work correctly if the DOM elements aren't loaded properly.

The next bit of code looks like this:

```jquery
var Speed = 800;
```

In that line, I'm declaring a variable called "Speed." It will tell the script how quickly the accordion should open and close. We could place the number directly into the code, but I prefer the variable route. It's personal preference, so go with what you feel comfortable doing.

Now, we've come to the code that will make our accordion work:

```jquery
$('.questions dd').hide();
  $('.questions dt').click(function () {
    $(this).next(".questions dd").slideToggle(Speed);
    $(this).toggleClass("expanded_img");
  });
```

We're telling the script to find the class "questions" and hide the answer portion of it. The following code makes the question a clickable link so that it will reveal the answer below it. The last bit of code appends the class "expanded_img" to the DIV.

The class appended to the DIV is controlled by our stylesheet. It calls the icons that indicate the closed or open status of an accordion item.

Oscar Otero created a jquery cheat sheet that I feel is useful. I've used it many times over the years, and I recommend it. It will tell you more about the bits of code we're using for our accordion.

The next portion of our code looks like this:

```jquery
$('.open').click(function (){
        $('.questions dd').slideToggle('.questions dt');
        $('.questions dt').toggleClass("expanded_img");
        $('.open').val('Open All');
        $('.open').toggleClass('close');
        $('.close').val('Close All').removeClass('.close');
    });
```

When I was coding the accordion, I wanted an open and close icon next to the questions. The above code makes that happen repeatedly. The code that calls the "open" class is referring to the "Open All" button.

The button will say "Open All" if the accordion is closed. Once you click the button, the text becomes "Close All." The code doesn't interfere with the click function of the question itself.

The code [val] refers to the text of the button itself. Changing the value of that code will change the text that appears on the button.

## The CSS

Now, all of this is going to look strange until we add something to our stylesheet. If you refer back a few paragraphs, you'll notice that I linked to a stylesheet called "normalize." That is the work of a person named Nicolas Gallagher. You can check out his Github [here](http://github.com/necolas/normalize.css).

It isn't necessary to add the normalize stylesheet. The only thing it does is unify how different browsers display the code. I like adding it to all my projects as a good habit.

The stylesheet that I coded looks like this:

```css
body {
    font-size: 16px;
    font-family: Helvetica, Arial, sans-serif;
    background: #ecf0f1;
    padding: 10px;
}

.wrapper {
    width: 75%;
    max-width: 1140px;
    margin-left: auto;
    margin-right: auto;
}

h1 {
    text-align: center;
}

/* Quetions */

dl.questions {
    background: #DCE3E5;
}

dl.questions dt {
    background: #E8ECEE url('plus.svg') right center no-repeat;
    background-size: 22px;
    background-origin: content-box;
    cursor: pointer;
    padding: 15px;
    border-bottom: 1px solid #DCE3E5;
}

dl.questions dd {
    padding: 15px;
    background: #DCE3E5;
}

dl.questions .expanded_img {
  background: #E8ECEE url('minus.svg') right center no-repeat;
  background-size: 15px;
  background-origin: content-box;
  cursor: pointer;
}

```

The stylesheet adds aesthetics to the web page. It's essentially personal preference, and it has little to do with jQuery itself. Altering the code here changes the way it appears on the web page.

The classes with icon backgrounds are essential. That is how jQuery changes the icon from one to another.  However, it can be tweaked to fit your project.

## Have Some Fun

I encourage you to experiment with the code. Playing around with someone else's code is how many developers learned how to do it themselves. When you handle the code, you're learning what each section does. You can download this code on [github](https://github.com/jvkrakowski/Ask).

Or, you can see a demo of it [here](http://jvkrakowski.com/Ask/).
