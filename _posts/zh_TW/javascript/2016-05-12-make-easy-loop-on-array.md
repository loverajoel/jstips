---
layout: post

title: 使用一個陣列建立一個簡單的迴圈
tip-number: 55
tip-username: jamet-julien
tip-username-profile: https://github.com/jamet-julien
tip-tldr: 有時候我們需要不停的 loop 我們陣列的項目，像是旋轉木馬的圖片或是播放清單。這裡是如何把一個陣列並給他「looping powers」。

redirect_from:
  - /zh_tw/make-easy-loop-on-array/

categories:
    - zh_TW
    - javascript
---
有時候我們需要不停的 loop 我們陣列的項目，像是旋轉木馬的圖片或是播放清單。這裡是如何把一個陣列並給他「looping powers」：

```js
var aList = ['A', 'B', 'C', 'D', 'E'];

function make_looper( arr ){

    arr.loop_idx = 0;

    // 回傳目前項目
    arr.current = function(){

      if( this.loop_idx < 0 ){ // 第一次檢查
        this.loop_idx = this.length - 1; // 更新 loop_idx
      }

      if( this.loop_idx >= this.length ){// 第二次檢查
        this.loop_idx = 0;// 更新 loop_idx
      }

      return arr[ this.loop_idx ]; // 回傳項目
    };

    // 增加 loop_idx 並回傳 new current
    arr.next = function(){
      this.loop_idx++;
      return this.current();
    };
    // 減少 loop_idx 並回傳 new current
    arr.prev = function(){
      this.loop_idx--;
      return this.current();
    };
}


make_looper( aList);

aList.current(); // -> A
aList.next(); // -> B
aList.next(); // -> C
aList.next(); // -> D
aList.next(); // -> E
aList.next(); // -> A
aList.pop() ; // -> E
aList.prev(); // -> D
aList.prev(); // -> C
aList.prev(); // -> B
aList.prev(); // -> A
aList.prev(); // -> D
```

使用 ```%```（模數）運算符更好看一些。模數運算回傳餘數（``` 2 % 5 = 1``` 和 ``` 5 % 5 = 0```）：

```js

var aList = ['A', 'B', 'C', 'D', 'E'];


function make_looper( arr ){

    arr.loop_idx = 0;

    // 回傳目前項目
    arr.current = function(){
      this.loop_idx = ( this.loop_idx ) % this.length; // 沒有驗證！
      return arr[ this.loop_idx ];
    };

    // 增加 loop_idx 並回傳 new current
    arr.next = function(){
      this.loop_idx++;
      return this.current();
    };

    // 減少 loop_idx 並回傳 new current
    arr.prev = function(){
      this.loop_idx += this.length - 1;
      return this.current();
    };
}

make_looper( aList);

aList.current(); // -> A
aList.next(); // -> B
aList.next(); // -> C
aList.next(); // -> D
aList.next(); // -> E
aList.next(); // -> A
aList.pop() ; // -> E
aList.prev(); // -> D
aList.prev(); // -> C
aList.prev(); // -> B
aList.prev(); // -> A
aList.prev(); // -> D
```
