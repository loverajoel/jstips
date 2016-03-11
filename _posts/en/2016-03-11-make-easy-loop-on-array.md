---
layout: post

title: Make easy loop on array
tip-number: xx
tip-username: jamet-julien
tip-username-profile: https://github.com/jamet-julien
tip-tldr: Make a elegant loop on array 

categories:
    - fr
---
We often need to build a loop, else the condition list would be huge.

```js

var index = 0,
    aList = ['A','B','C', 'D', 'E']

function change( dir){

    if( index < 0){
      index = aList.length-1;
    }

    if( index >= aList.length ){
      index = 0;
    }

    dir = ( dir )? -1 : 1;

    index = index + dir;

   return aList[ index ];
}

change(); //A
change(); //B
change(); //C
change(); //D
change(); //E
change(); //A  LOOP !

change( true); //A
change( true); //E
change( true); //D
change( true); //C
change( true); //B
change( true); //A
change( true); //E LOOP !


```

Using the ```%``` operator is prettier:

```js

var index = 0,
    aList = ['A','B','C', 'D', 'E']

function change( dir){
   dir   = ( dir)?  aList.length - 1 : 1 ;
   index = ( index + dir ) % aList.length;
   return aList[ index ];
}

change(); //A
change(); //B
change(); //C
change(); //D
change(); //E
change(); //A  LOOP !

change( true); //A
change( true); //E
change( true); //D
change( true); //C
change( true); //B
change( true); //A
change( true); //E LOOP !


```
