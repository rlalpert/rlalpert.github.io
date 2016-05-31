---
title: "Sublime Text 3 Snippet: Angular 2 Component"
date: 2016-05-30
layout: post
tags: workflow sublime angular2 snippets
---
Something I don't do enough is write (or use) Sublime snippets. For a long time, I had a pedagogical justification for it: forcing myself to write every character of code reinforced my understanding of syntax, meaning, and best practices. I still believe that this is an effective way to learn and would recommend it to anyone who is really interested in engaging with the fundamentals of a programming language.

That said, I finally feel like I'm at a point where I can really dig into the exciting world of **Workflow**. 🌟Hurray!🌟 So, what simpler way to dive into workflow is there than Sublime code snippets?

Since I am learning Angular 2, which is component based, I figured I'd need to spend *a lot* of time creating new components. Writing it all out by hand? *Boring*. Enter this simple component snippet for TypeScript:

{% highlight xml linenos %}
<snippet>
  <content><![CDATA[
import {Component} from '@angular/core';

@Component({
  selector: '${1:my-selector}',
})

export class ${2:MySelector} { }
]]></content>
  <tabTrigger>comp</tabTrigger>
  <scope>source.ts</scope>
  <description>Creates a new Angular 2 TypeScript component.</description>
</snippet>
{% endhighlight %}

Using this snippet is simple. With Sublime Text 3 (I'm using OSX), navigate to:

{% highlight bash %}
Tools > Developer > New Snippet...
{% endhighlight %}

In the new window, just paste in the above snippet and save it (preferably in a dedicated custom snippets folder) as a `whateverNameYouLike.sublime-snippet` file.

 Now you need only type `comp` in any TypeScript file and hit the `TAB` key to create a simple, new Angular 2 Component. Easy!