---
layout: post

title: Improving your Async functions with WebWorkers
tip-number: 74
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: JS runs in a single thread in the browser, this is the truth. In this tip I'll show you how to unleash the full power of asynchronous processing with Web Workers.

categories:
    - en
    - javascript
---

> JS shall have but one Thread (in the browser at least)
>
> -- Thus spoke the master programmer.

JS runs in a single thread in the browser, this is the truth.

Somewhere in its own universe, there exists a Queue which holds messages
and functions associated with them.

Every time an event (i.e, a user clicks a button) is registered, there's
a runtime check to see whether there's any listener attached to that event.
If there's one, it will enqueue the message. Otherwise, it will be lost
forever.

Now, our event loop processes one message at a time, meaning that if you
do some CPU intensive operation (i.e, number crunching) this will indeed
'block' the one Thread, rendering our application useless.

This is true even for `async` functions, which will be queued as soon as
invoked and executed as soon as possible (immediately given the queue is
empty).

I/O such as requests to external resources are non-blocking though, so you
can request a file as large as you want without fear. The associated
callback, however, will show the same characteristics of an `async` function.

Strategies for processing lots of data vary a lot. You could partition data
and set timeouts for processing bits of it a time for example. But to unleash
the full power of asynchronous processing, you should use Web Workers.

To do so, you separate the processing part in a different file (possibly
'my_worker.js'), create a worker with `newWorker = new Worker('my_worker.js');`
and offload the processing to it.

``` javascript
// my_worker.js
const do_a_lot_of_processing = (data) => {
    ....
}

onmessage = (e) => {
    postMessage(do_a_lot_of_processing(e.data));
}

// main.js
const myWorker = new Worker('my_worker.js');

async function get_useful_data() {
    const raw_data = await request(some_url);
    myWorker.postmessage(raw_data);
}

const show_data => (e) {
    const data = e.data;
    ...
}

myWorker.onmessage(show_data);
get_useful_data();
```

Your mileage may vary of course, and there are many abstractions that can be
built upon this model.