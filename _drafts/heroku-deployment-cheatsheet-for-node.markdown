---
title: Heroku Deployment Cheatsheet for Node
layout: post
---
Something I like to do when learning a new technology is distill it down to its most practical parts and create a cheatsheet for myself to reference later when I inevitably forget the minutiae necessary to actually *Make It Go*.

For the moment, [Heroku](https://www.heroku.com/) seems like a fine way to dip my feet into deploying a few little Node apps I'm working on and I don't feel particularly inclined to sift through the [15 page long Getting Started guide](https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction) every time I forget how to do one small thing or other (which I *totally* will). Enter this Cheatsheet. 

*(Okay, some might call this simply **taking notes**, but shhhhh now, don't worry your pretty little head. Sharing it makes it a Cheatsheet. Yay! I'm **Helping**!)*

The following assumes you've gone through Heroku's [Basic Setup](https://devcenter.heroku.com/articles/getting-started-with-nodejs#set-up) and have the Heroku Toolbelt, Node, NPM, and Git installed.

# The Cheatsheet

## CLI

{% highlight bash %}
heroku create
{% endhighlight %}

* Creates an app on Heroku
* Optional: Specify your app name by passing it as a parameter

{% highlight bash %}
git push heroku master
{% endhighlight %}

* Pushes your app to Heroku 
* Needs to be run from the folder where your app lives
* Notes:
  * Make sure you have already used `git init` in your app's root folder and have **added** your file(s)/changes with `git add .` and **committed** them with `git commit -m 'Commit message'`.
  * Heroku will install the necessary dependencies listed in your `package.json` file.

{% highlight bash %}
heroku ps:scale web=1
{% endhighlight %}

* Makes sure at least one instance of your app is running. 

{% highlight bash %}
heroku open
{% endhighlight %}

* Opens your app in a browser window
* Takes a path as a parameter. For example, `heroku open cholula` will open a browser window to `yourapp.herokuapp.com/cholula`

{% highlight bash %}
heroku local
{% endhighlight %}

* Runs the application locally.
* If you have more than just `web` defined in your `Procfile`, you can just run the `web` command by passing it as an argument. If your `Procfile` is only `web: node index.js`, then `heroku local` and `heroku local web` are functionally the same.

## Important Files

### .gitignore

* Make sure you have a `.gitignore` file that contains *at least* `node_modules` and probably `npm-debug.log` for good measure.

### Procfile

* A text file that must be in the root directory of your application.
* This file does **not** have an extension. 
* Explicitly tells Heroku what commands to execute to start your app.
* The most basic `Procfile` would be something like:
{% highlight bash %}
web: node index.js
{% endhighlight %}

---

# Yes, There's *More!*

The above is the most basic info you need to get your app running on Heroku.