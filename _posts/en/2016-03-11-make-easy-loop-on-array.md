---
layout: post

title: Create an easy loop using an array
tip-number: xx
tip-username: jamet-julien
tip-username-profile: https://github.com/jamet-julien
tip-tldr: Create an easy loop using an array 

categories:
    - en
---
We often need to build a loop, else the condition list would be huge.

```js

var index = 0,
    aList = ['A','B','C', 'D', 'E'];

function change( dir ){
    
    //Is it the start ? So go to the last element
    if( index < 0 ){
      index = aList.length-1;
    }
    
    // Is it the end ? So go to the first element
    if( index >= aList.length ){
      index = 0;
    }

   dir   = ( dir )? -1 : 1;
   index = index + dir;
   return aList[ index ];
}

change();//A
change();//B
change();//C
change();//D
change();//E
change();//A  LOOP !
change( true );//A
change( true );//E
change( true );//D
change( true );//C
change( true );//B
change( true );//A
change( true ); //E LOOP !
```

Using the ```%``` operator is prettier:

```js

var index = 0,
    aList = ['A','B','C', 'D', 'E']

function change( dir ){
   dir   = ( dir )?  aList.length - 1 : 1 ;
   index = ( index + dir ) % aList.length;
   return aList[ index ];
}

change();//A
change();//B
change();//C
change();//D
change();//E
change();//A  LOOP !
change( true );//A
change( true );//E
change( true );//D
change( true );//C
change( true );//B
change( true );//A
change( true ); //E LOOP !
```
