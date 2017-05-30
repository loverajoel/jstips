---
layout: post

title: Upping Performance by Appending/Keying
tip-number: 75
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: React uses a mechanism called **reconciliation** for efficient rendering on update.

categories:
    - en
    - react
---

React uses a mechanism called **reconciliation** for efficient rendering on
update.

**Reconciliation** works by recursively comparing the tree of DOM elements,
the specifics of the algorithm might be found on the official documents or
the source, which is always the best source.

This mechanism is partly hidden, and as such, there are some conventions
that might be followed to ease its inner workings.

One such example is **appending** vs **inserting**.

**Reconciliation** compares the list of root's nodes children at the same
time, if two children differ, then React will mutate every one.

So, for example, if you've got the following:

``` html
<ul>
    <li>Sherlock Holmes</li>
    <li>John Hamish Watson</li>
</ul>
```

And you insert an element at the beginning

``` html
<ul>
    <li>Mycroft Holmes</li>
    <li>Sherlock Holmes</li>
    <li>John Hamish Watson</li>
</ul>
```

React will start of by comparing the old tree, where `<li>Second</li>` is the
first child and the new tree where `<li>First</li>` is the new first child.
Because they are different, it will mutate the children.

If, instead of inserting good Mycroft you appended him, React would perform
better, not touching Sherlock nor John.

But you can't always append, sometimes you've just got to insert.

This is were **keys** come in. If you supply a **key** *attribute* then React
will figure out an efficient transformation from the old tree to the new one.

``` html
<ul>
    <li key="3">Mycroft Holmes</li>
    <li key="1">Sherlock Holmes</li>
    <li key="2">John Hamish Watson</li>
</ul>
```