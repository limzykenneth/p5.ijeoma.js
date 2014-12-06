#p5.ijeoma.js
 
A p5.js addon [ijeoma.js](https://github.com/ekeneijeoma/p5.ijeoma.js), a JS library for creating animations. More documentation and examples can be found in the [ijeoma.js README](https://github.com/ekeneijeoma/p5.ijeoma.js).

#Download   
Developement: [p5.ijeoma.js](http://goo.gl/04mfZ7)

Production: [p5.ijeoma.min.js](http://goo.gl/Aeb2UP)

[ijeoma.js required](https://github.com/ekeneijeoma/ijeoma.js)

#Getting Started 
###Creating tweens
Tweening a variable named x from 0 to 1024 in 1000 millseconds. 
```javascript 
//createTween(object, property, end, duration, [delay], [easing])
var x = 0;
var tween = createTween(window, "x", 1024, 1000).play(); // if no object is passed it will default to window
```
or
```javascript 
//createTween(property, [start,end], duration, [delay], [easing])
var tween = createTween("x", [0,1024],1000).play(); // object defaults to window and the variable x is defined in window with a starting value of 0
```

Tweening multiple variables and object properties
```javascript
//createTween(duration, [delay], [easing])
var tween = createTween(1000).add(window, "x", [0,1024]).add(window, "y", [0,768]).add(window, "size", [0,100]).play();
```
or
```javascript
//createTween(duration, [delay], [easing])
var tween = createTween(1000).add("x", [0,1024]).add("y", [0,768]).add("size", [0,100]).play(); // object defaults to window
```

You can also call play and stop on all motion objects using
```javascript
playAll()
stopAll()
```

##Destroying tweens
```javascript
Motion.remove(motion)
```

If you're creating and playing a lot of tweens that you're only using once you should can call useOnce() which will automatically destroy them after. It's set to false by default.
```javascript
createTween(...)(...).useOnce();
or
//applies call to all tween instances
useOnce();
```

###Delaying
```javascript
var tween = createTween("w", 1024, 1000, 500).play(); //delay for 500 milliseconds
```
or
```javascript
var tween = createTween("w", 1024, 1000).delay(500).play();
```
###Pausing, Resuming  
```javascript  
t.pause(); 
t.resume(); 
t.seek(position); 

pauseAll();
resumell();
seekAll(position);
```
###Repeating
```javascript
var tween = createTween(...).repeat().play();

repeatAll([duration]);
```
###Reversing
```javascript 
var tween = createTween(...).repeat().reverse().play();

reverseAll();
```

###Changing speed/timescale
```javascript 
var tween = createTween(...).timeScale(2) //plays back twice as fast

timeScaleAll(time);
``` 

##Playing back tweens in parallel
```javascript 
timeMode(FRAMES); //frames by default
p = beginParallel() // returns MOTION.Parallel() object
  tween(...) // same arguments and functions as createTween()
  tween(...)
endParallel();
p.play()
//or play(p); 
```

##Playing back tweens in sequence
```javascript 
var s = beginSequence(); // returns MOTION.Sequence() object
  tween(...)
  tween(...)
endSequence()
s.play();
```

##Playing back tweens in a timeline
```javascript 
var t = beginTimeline(); // returns MOTION.Timeline() object
  beginKeyframe(100);
    tween(...)
  endKeyframe();
  beginKeyframe(200);
    tween(...)
  endKeyframe();
endTimeline();
t.play();
```