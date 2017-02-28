---
layout: post

title: Crear un bucle fácil usando un array
tip-number: 55
tip-username: jamet-julien
tip-username-profile: https://github.com/jamet-julien
tip-tldr: A veces, necesitamos un ciclo sin fin sobre un array de items, como un carrusel de imágenes o un lista de reproducción de audio. Así es como tomar un array y darle "bucle poderosos"

redirect_from:
  - /es_es/make-easy-loop-on-array/

categories:
    - es_ES
    - javascript
---

A veces, necesitamos un ciclo sin fin sobre un array de items, como un carrusel de imágenes o un lista de reproducción de audio. Así es como tomar un array y darle "bucle poderosos"

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

Utilizando el operador ```%``` (módulo) es más vistoso. El modulo retorna el resto de la division ( ``` 2 % 5 = 1``` y ``` 5 % 5 = 0```):

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
