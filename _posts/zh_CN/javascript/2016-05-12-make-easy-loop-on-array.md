---
layout: post

title: 用数组建立一个简单的循环
tip-number: 55
tip-username: jamet-julien
tip-username-profile: https://github.com/jamet-julien
tip-tldr: 有时我们需要不停的循环数组的元素，就像一组旋转的图片，或者音乐的播放列表。这里告诉你如何使一个数组拥有循环的能力。

redirect_from:
  - /zh_cn/make-easy-loop-on-array/

categories:
    - zh_CN
    - javascript
---
有时我们需要不停的循环数组的元素，就像一组旋转的图片，或者音乐的播放列表。这里告诉你如何使一个数组拥有循环的能力：

```js
var aList = ['A','B','C','D','E'];

function make_looper( arr ){

    arr.loop_idx = 0;

    // 返回当前的元素
    arr.current = function(){

      if( this.loop_idx < 0 ){// 第一次检查
        this.loop_idx = this.length - 1;// 更新 loop_idx
      }

      if( this.loop_idx >= this.length ){// 第二次检查
        this.loop_idx = 0;// 更新 loop_idx
      }

      return arr[ this.loop_idx ];//返回元素
    };
    
    // 增加 loop_idx 然后返回新的当前元素
    arr.next = function(){
      this.loop_idx++;
      return this.current();
    };
    // 减少 loop_idx 然后返回新的当前元素
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

使用 ```%``` ( 取模 ) 操作符更优雅。取模返回除法的余数 ( ``` 2 % 5 = 1``` and ``` 5 % 5 = 0```)：

```js

var aList = ['A','B','C','D','E'];


function make_looper( arr ){

    arr.loop_idx = 0;

    // return current item
    arr.current = function(){
      this.loop_idx = ( this.loop_idx ) % this.length;// 无需检查 !!
      return arr[ this.loop_idx ];
    };

    // 增加 loop_idx 然后返回新的当前元素
    arr.next = function(){
      this.loop_idx++;
      return this.current();
    };
    
    // 减少 loop_idx 然后返回新的当前元素
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
