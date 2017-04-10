---
layout: post

title: Adventurers Guide to React (Part I)
tip-number: 72
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: So you've heard of this *React* thing, and you actually peeked at the docs, maybe even went through some of the pages. Then you suddenly came across mysterious runes that spelled somewhat along the lines of Webpack, Browserify, Yarn, Babel, NPM and yet much more.

categories:
    - en
    - react
---

> I used to be an adventurer like you, but then I took a RTFM in the knee...
>
> Guard outside of Castle Reducer in the Land of React

So you've heard of this *React* thing, and you actually peeked at the docs,
maybe even went through some of the pages. Then you suddenly came across
mysterious runes that spelled somewhat along the lines of Webpack, Browserify,
Yarn, Babel, NPM and yet much more.


Thus, you went to their official sites and went through the docs, just to find
yourself lost in the ever growing collection of modern tools (tm) to build
web applications with JS.


Afraid you must be not.

## Yarn, NPM
They are just dependency managers, nothing to be afraid of. In fact, they are
the less scary part. If you've ever used a GNU/Linux distro, FreeBSD, Homebrew
on MacOSX, Ruby and Bundler, Lisp and Quicklisp just to name a few, you'll be
familiar with the concept.


Should you not be, it's a very simple thing, so don't worry. The Land of React
is but a province in a much bigger world, which some call Javascript and others
Ecmascript (JS/ES for short).


Now suppose you are starting your own town, but you really want to use React's
tools for your buildings, because, let's face it, it is popular. The traditional
way would be to walk to the Land of React and ask the ruler to handle you some
of his tools. The problem is you waste time, and you must keep contact with him
so if any tools is faulty, you get a new one.


However, with the advent of drones and near-instant travel for them, some smart
guys started a registry of the different towns, cities and provinces. Furthermore,
they built especial drones that could deliver the tools right to you.


Nowadays, to require React in your project, you just have to go

```bash
$ npm init . # create town
$ npm install --save react # get react and put the materials in the store
```


Handy, isn't it? and free.


## Webpack, Browserify and friends
In the old times, you had to build your town all by yourself. If you wanted a
statue of John McCarthy you would have to fetch marble and some parentheses
on your own. This improved with the advent of *dependency managers*, which could
fetch the marble and the parentheses for you. Yet, you had to assemble them on
your own.


Then came some folks from Copy & Paste (inc) and developed some tools that allowed
you to copy and paste your materials on some specific order, so you could have
your parentheses over the statue or under it.


That was actually pretty cool, you just placed all the material and specified
how they were going to be built, and all was peaceful for a while.


But this approach had a problem, which I'm sure other folks tried to circumvent.
Namely, that if you wanted to replace the parentheses by cars you would have
to rebuild your entire town. This was no problem for small towns, but large cities
suffered by this approach.


Then inspiration was given by the mighty Lord and building and module bundlers
were born.


This module bundlers allowed you to draw blueprints, and specify exactly how
the town was to be constructed. Furthermore, they grew quickly and supported
only rebuilding parts of the town, leaving the rest be.


## Babel
Babel is a time traveler who can bring materials from the future for you. like
ES6/7/8 features.


## How they all mix together
Generally, you'll create a folder for your project, fetch dependencies, configure
your module bundler so it knows where to search for your code and where to output
the distributable. Furthermore, you may want to wire that to a development server
so you can get instant feedback on what you're building.


However, the documentation of module bundlers is a bit overwhelming. There are so
many choices and options for the novice adventurer that he might lose his
motivation.


## create-react-app and friends
Thus yet another tool was created.

```bash
$ npm install -g create-react-app # globally install create-react-app
$ create-react-app my-shiny-new-app
```

And that's all. It comes pre-configured so you don't have to go through all
of Webpack/Browserify docs just to test React. It also brings testing scripts,
a development web server and much more.


However, this is not yet the final word to our history. There exists a myriad
of different builders and tools for React, which can be seen here
https://github.com/facebook/react/wiki/Complementary-Tools