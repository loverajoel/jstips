---
layout: post

title: Tapping for quick debugging
tip-number: 65
tip-username: loverajoel
tip-username-profile: https://twitter.com/loverajoel
tip-tldr: This little beastie here is tap. A really useful function for quick-debugging chains of function calls, anonymous functions and, actually, whatever you just want to print.
tip-md-link: https://github.com/loverajoel/jstips/blob/master/_posts/en/javascript/2017-03-16-tapping-for-quick-debugging.md

categories:
    - en
    - javascript
---

This little beastie here is tap. A really useful function for quick-debugging
chains of function calls, anonymous functions and, actually, whatever you just
want to print.

``` javascript
function tap(x) {
    console.log(x);
    return x;
}
```

Why would you use instead of good old `console.log`? Let me show you an example:

``` javascript
bank_totals_by_client(bank_info(1, banks), table)
            .filter(c => c.balance > 25000)
            .sort((c1, c2) => c1.balance <= c2.balance ? 1 : -1 )
            .map(c =>
                 console.log(`${c.id} | ${c.tax_number} (${c.name}) => ${c.balance}`));
```

Now, suppose you're getting nothing from this chain (possibly an error).
Where is it failing? Maybe `bank_info` isn't returning anything, so we'll tap it:

``` javascript
bank_totals_by_client(tap(bank_info(1, banks)), table)
```

Depending on our particular implementation, it might print something or not.
I'll assume the information that we got from our tapping was correct and
therefore, bank_info isn't causing anything.

We must then move on to the next chain, filter.

``` javascript
            .filter(c => tap(c).balance > 25000)
```

Are we receiving any c's (clients actually)? If so, then bank_totals_by_client
works alright. Maybe it's the condition within the filter?

``` javascript
            .filter(c => tap(c.balance > 25000))
```

Ah! Sweet, we see nothing but `false` printed, so there's no client with >25000,
that's why the function was returning nothing.

## (Bonus) A more advanced tap.

``` javascript
function tap(x, fn = x => x) {
    console.log(fn(x));
    return x;
}
```

Now we're talking about a more advanced beast, what if we wanted to perform a
certain operation *prior* to tapping? i.e, we want to access a certain object
property, perform a logical operation, etc. with our tapped object? Then we
call old good tap with an extra argument, a function to be applied at the moment
of tapping.


``` javascript
tap(3, x => x + 2) === 3; // prints 5, but expression evaluates to true, why :-)?
```
