---
layout: post

title: Create an easy loop using an array
tip-number: 55
tip-username: jamet-julien
tip-username-profile: https://github.com/jamet-julien
tip-tldr: Sometimes, we need to loop endlessly over an array of items, like a carousel of images or an audio playlist. Here’s how to take an array and give it “looping powers” 

redirect_from:
  - /en/make-easy-loop-on-array/

categories:
    - en
    - javascript
---
Sometimes, we need to loop endlessly over an array of items, like a carousel of images or an audio playlist. Here's how to take an array and give it "looping powers":

```js
var aList = ['A','B','C','D','E'];

function make_looper( arr ){

    arr.loop_idx = 0;

    // return current item
    arr.current = function(){

      if( this.loop_idx < 0 ){// First verification
        this.loop_idx = this.length - 1;// update loop_idx
      }

      if( this.loop_idx >= this.length ){// second verification
        this.loop_idx = 0;// update loop_idx
      }

      return arr[ this.loop_idx ];//return item
    };
    
    // increment loop_idx AND return new current
    arr.next = function(){
      this.loop_idx++;
      return this.current();
    };
    // decrement loop_idx AND return new current
    arr.prev = function(){
      this.loop_idx--;
      return this.current();
    };
}


make_looper( aList);

aList.current();// -> A
aList.next();// -> B
aList.next();// -> C
aList.next();// -> D
aList.next();// -> E
aList.next();// -> A
aList.pop() ;// -> E
aList.prev();// -> D
aList.prev();// -> C
aList.prev();// -> B
aList.prev();// -> A
aList.prev();// -> D
```

Using the ```%``` ( Modulus ) operator is prettier.The modulus return division's rest ( ``` 2 % 5 = 1``` and ``` 5 % 5 = 0```):

```js

var aList = ['A','B','C','D','E'];


function make_looper( arr ){

    arr.loop_idx = 0;

    // return current item
    arr.current = function(){
      this.loop_idx = ( this.loop_idx ) % this.length;// no verification !!
      return arr[ this.loop_idx ];
    };

    // increment loop_idx AND return new current
    arr.next = function(){
      this.loop_idx++;
      return this.current();
    };
    
    // decrement loop_idx AND return new current
    arr.prev = function(){
      this.loop_idx += this.length - 1;
      return this.current();
    };
}

make_looper( aList);

aList.current();// -> A
aList.next();// -> B
aList.next();// -> C
aList.next();// -> D
aList.next();// -> E
aList.next();// -> A
aList.pop() ;// -> E
aList.prev();// -> D
aList.prev();// -> C
aList.prev();// -> B
aList.prev();// -> A
aList.prev();// -> D
```
