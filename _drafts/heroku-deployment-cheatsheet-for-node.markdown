---
title: Heroku Deployment Cheatsheet for Node
layout: post
---
Something I like to do when learning a new technology is distill it down to its most practical parts and create a cheatsheet for myself to reference later when I inevitably forget the minutiae necessary to actually *Make It Go*.

For the moment, [Heroku](https://www.heroku.com/) seems like a fine way to dip my feet into deploying a few little Node apps I'm working on and I don't feel particularly inclined to sift through the [15 page long Getting Started guide](https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction) or the [slightly different Deployment guide](https://devcenter.heroku.com/articles/deploying-nodejs#how-to-keep-build-artifacts-out-of-git) every time I forget how to do one small thing or other (which I *totally* will). Enter this Cheatsheet. 

*(Okay, some might call this simply **taking notes**, but shhhhh now, don't worry your pretty little head. Sharing it makes it a Cheatsheet. Yay! I'm **Helping**!)*

The following assumes you've gone through Heroku's [Basic Setup](https://devcenter.heroku.com/articles/getting-started-with-nodejs#set-up) and have the Heroku Toolbelt, [Node](https://nodejs.org/en/), [npm](https://www.npmjs.com/), and [Git](https://git-scm.com/) installed.

# The Cheatsheet

## CLI

{% highlight bash %}
heroku create
{% endhighlight %}

* Creates an app on Heroku.
* Optional: Specify your app name by passing it as a parameter.

{% highlight bash %}
git push heroku master
{% endhighlight %}

* Pushes your app to Heroku.
* Needs to be run from the folder where your app lives.
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

* Opens your app in a browser window.
* Takes a path as a parameter. For example, `heroku open cholula` will open a browser window to `yourapp.herokuapp.com/cholula`.

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

### package.json

* Running `npm init` in your root directory walks you through creating the file.
* Defines dependencies that should be installed with your app.
* Make sure you have the version of node you are developing with in your file:

{% highlight json %}
"engines": {
    "node": "6.2.0"
  },
{% endhighlight %}

## Using the $PORT Variable

* If you are using a web dyno, you *must* bind it to a port number set by the `$PORT` variable, or the dyno won't start. 
* You can access this variable with `process.env.PORT`
* An example of using this in Express is:

{% highlight js %}
var express = require('express');
var app = express();

app.set('port', (process.env.PORT || 5000));
{% endhighlight %}

* Using `5000` as a fallback allows you to run on that port locally for development.

---

# Wait, There's *More!*

**The above is the *most basic* info you need to get your Node app up and running on Heroku.** However, in the interest of keeping all of my basic reference in one place, here are some more useful commands from the [Getting Started Guide](https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction):

### Logs

{% highlight bash %}
heroku logs
{% endhighlight %}

* Fetches 100 log lines by default
* You can specify the number of logs by using the `-n` or `--num` option, up to 1,500:

{% highlight bash %}
heroku logs -n 200
{% endhighlight %}

{% highlight bash %}
heroku logs --tail
{% endhighlight %}

* Opens a session for real-time logs to stream in.

### App Scaling

* You can check the number of dynos currently running with the command `heroku ps`.
* You can change the number of dynos running commands from your `Procfile`.

{% highlight bash %}
heroku ps:scale web=0
{% endhighlight %}

* The above will remove all dynos from running the `web` command from your `Procfile`. If you try to access your app in a browser with this set to `0`, you'll get an error message.

### Addons

{% highlight bash %}
heroku addons
{% endhighlight %}

* Lists Addons being used by your app.

{% highlight bash %}
heroku addons:create addonname
{% endhighlight %}

* "Provisions" the use of an addon by your app.

{% highlight bash %}
heroku addons:open addonname
{% endhighlight %}

* Opens the web console for an addon.

### Start A Console

* You can open a one-off dyno using `heroku run`.

{% highlight bash %}
heroku run node
{% endhighlight %}

* Opens a Node console.

{% highlight bash %}
heroku run bash
{% endhighlight %}

* Opens a shell on your dyno.
* Need to type `exit` to close the shell. (As opposed to `CTRL C`.)

---

# Official Links

* [Reference](https://devcenter.heroku.com/categories/reference) - Documentation for digging into the nitty gritty of the platform. These are really well done docs.
* [Articles](https://devcenter.heroku.com/categories/nodejs/articles) - For the kind of information that doesn't fit into the Documentation format. Tutorials, best practices, etc..
* [Best Practices for Node.js Development](https://devcenter.heroku.com/articles/node-best-practices) - Self explanatory.