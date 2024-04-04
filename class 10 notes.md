#### SESSION #10
# FUNCTIONAL PROGRAMMING

## WHAT IS FUNCTIONAL PROGRAMMING
- In Javascript, functions are objects, and they behave like other variables/values with their own properties and methods and can be passed as arguments and returned by functions. 
- This makes functions very flexible and they can be used to create modules and libraries for cleaner code and speedier execution.
- Functional programming  uses functions and their features to build out the operations to perform single discrete tasks through encapsulation. Then it can combine them all to build out more complex structures.
- Each function performs a task and returns a value that can be worked on by another (doesn't change or use the outside world).
- The emphasis is on simplicity where data and functions are concerned, and building complex tasks through a series of simple tasks.


## THE BASICS

### A Pure Function
- No side-effects - non-destructive data transformation
- No external dependencies
- Return Transparency


### Basic Structure:
- At least one argument
- A return value

## FUNCTIONAL CONCEPTS
```
const xs = [1,2,3,4,5];

// pure
xs.slice(0,3); // [1,2,3]
console.log(xs); //the same as before

// impure - as it mutates original data and can have side effects
xs.splice(0,3); // [1,2,3]
```

Simple example of pure:
```
function random(a, b) {
  if (b === undefined) {
    b = a, a = 1; // if no 2nd argument, lower limit is 1
  }
  return Math.floor((b - a + 1) * Math.random()) + a;
}
random(6);
random(6, 20);
```

An impure example:
```
let def = 6;
function random(a, b) {
  if (b === undefined) {
    b = a, a = def; // if no 2nd argument, lower limit is def
  }
  return Math.floor((b-a+1) * Math.random()) + a;
}
```

An Example:
```
function reverse(string) {
  let array = string.split("");
  array.reverse();
  return array.join("");
}

const message = "Hello";
const newmess = reverse(message);
console.log(newmess);
console.log(message);

This can also be written as: 
function reverse(string) {
return string.split("").reverse().join(""); 
}
```

This makes it easier to string/chain - method chaining
```
const newmess = reverse(message).toLowerCase().substr(0,3);
```

OR without that function
```
const newmess = message.split("").reverse().join("").toLowerCase().substr(0,3);
```


Another Example:
```
const string = " The Answer is Forty-Two ";

const slugify = string =>
 string
   .toLowerCase()
   .trim()
   .split(" ")
   .join("-");

slugify(string); // slugged up version
```
OR without a wrapper function:
```
string.toLowerCase().trim().split(" ").join("-");
```

## HIGHER ORDER FUNCTIONS

Helps write more compact and simple functions that can be re-combined to create more complex functions:
```
function square(x){
  return x*x;
}

function hypotenuse(a,b) {
  let total = square(a) + square(b);
  return Math.sqrt(total);
}
```

## CALLBACKS

Functions that are sent as arguments to another function. Allows for more generalized function definitions with delegating complex tasks to externally defined functions
```
// pass function as a parameter
const convertToCelsius =  function(deg_fah) {
     let converted_deg = (deg_fah-32) * 5/9;
     return converted_deg;
};
const convertToFahrenheit =  function(deg_cent) {
     let converted_deg = (deg_cent * 9/5) + 32;
     return converted_deg;
};
// pass function as a parameter
function convert(converter, temperature) {
     console.log(converter(temperature));
}
convert(convertToCelsius, 23);
convert(convertToFahrenheit, 23);
```


## RECURSIVE FUNCTIONS

Calls itself until a certain condition is met - useful for iterative processes:
```
function factorial(n) {
  if (n === 0) {
    return 1
  } else {
    return n * factorial(n - 1);
  }
}

factorial(10);
```


## RETURNING FUNCTIONS

Returns a function based on specific params:
```
function power(x) {
  return function(power) {
    return Math.pow(x,power);
  }
}
let twoExp = power(2);
twoExp(5);
power(2)(5);
```

## CLOSURES

Function that contain functions that get access to the outer function's variables and params, and stay alive after the initial call:

```
function counter(start){
  i = start;
  return function() {
return i++; 
  }
}
let count = counter(1); // start a counter at 1
count();
```
```
function multiplier(factor) {
  let ret = function(number) {
    return number * factor;
  };
  return ret;
}
const square = multiplier(2);
const cubed = multiplier(3);

square(3);
cubed(3);
multiplier(2)(3); // same as above square(3)
```

## PROMISES

Created to better manage the results of asynchronous operations. Cleans up Callback Hell:

```
const promise = new Promise( (resolve, reject) => {
    // initialization code goes here
    if (success) {
        resolve(value);
    } else {
        reject(error);
    }
});

const dice = {
  sides: 6,
  roll: function() {
    		return Math.floor(this.sides * Math.random()) + 1;
  }
}

const promise = new Promise( (resolve,reject) => {
const n = dice.roll();
setTimeout(() => {
        (n > 3) ? resolve(n) : reject(n);
     }, 2000);
});

// promise.then(resolve_function, reject_function);

promise.then(	result => console.log(`Yes! I rolled a ${result}`), 
result => console.log(`Drat! ... I rolled a ${result}`) 
);

promise.catch( result => console.log(`Damn! ... I made a mistake - ${result}`));

```


### A more compact version:
```
const dice = {
  sides: 6,
  roll: function() {
    		return Math.floor(this.sides * Math.random()) + 1;
  }
}

const promise = new Promise( (resolve,reject) => {
        const n = dice.roll();
        setTimeout(() => {
          (n > 3) ? resolve(n) : reject(n);
        }, 2000);
   	})
    .then( result => console.log( `Yes! I rolled a ${result}`) )  //resolver function
    .catch( result => console.log(`Dammit! ... I rolled a ${result}`));  //rejector function

```

## IIFEs
An Immediately Invoked Function Expression is a function that gets invoked as soon as it’s defined.
Keeps scope of variables local and doesn't clutter global.
Also called Anonymous Closures
One of the most useful Javascript features!

```
( function() {
  const temp = "world";
  console.log("Hello " + temp);
}() );


console.log('What is temp outside the IIFE', temp);
```

## IIFEs - block scopes

Most languages let a variable have scope inside a code block, but not JavaScript (pre ES6) - its variables can live outside a block. But IIFE can mimic the block scope:
```
const list = [1,2,3];
for (var i = 0, max = list.length ; i < max ; i++ ){
  console.log(list[i]);
}
console.log(i); //i is still outside


const list = [1,2,3];
(function(){
for (var i = 0, max = list.length ; i < max ; i++ ){
  		console.log(list[i]);
}
}());
console.log(i); // i is not available outside the for block
```


## IIFEs - global import, local scope

IIFE can access the global scope just like any function. But it's better practice to pass a global variable to it to keep the block self-contained:
```
let list = [1,2,3];
(function(my_list){
for (let i = 0, max = my_list.length ; i < max ; i++ ){
  		console.log(my_list[i]);
}
}(list));
console.log(i); // i is not available outside the for block
```

This is how we use jQuery!
```
(function($){
  // we have access to globals jQuery (as $)
  // bind click event to all internal page anchors
  $(".menu-link").bind("click touchstart", function (e) {
      // prevent default action and bubbling
      e.preventDefault();
      e.stopPropagation();
      $("#off-canvas-nav").toggleClass("active");
      $("#wrapper").toggleClass("active");
  });
})(jQuery);
```

## IIEFs - with ES6

Using ES6 variable initializers let, const, you don't need IIFEs since both these declariations are block scoped:
```
{
  const list = [1,2,3];
  for (let i = 0, max = list.length ; i < max ; i++ ){
  		console.log(list[i]);
  }
};
console.log(i); // i is not available outside the for block
console.log(list); // list is not available outside the for block
```

WHAT HAPPENS WITH THIS CODE?
```
{
  var list = [1,2,3];
  for (let i = 0, max = list.length ; i < max ; i++ ){
  		console.log(list[i]);
  }
};
console.log(i);
console.log(list);
```


# MODULES

- Self-contained piece of code that provides functions and methods that can then be used elsewhere
- Improves usability, readability, maintainability, namespacing, error-checking etc.
- Generally organized by distinct functionality
- Modules store private/public methods and properties inside an object that can interact with the outside through an API (similar to Classes)


## ANONYMOUS CLOSURE 

An Anonymous function has its own evaluation environment which is  immediately evaluated, hiding variables from the parent (global) namespace.

```
(function() {
  "use strict";

  function square(x) {
    return x * x; 
  }
  function sum(array, callback) {
    if (typeof callback === "function") {
      array = array.map(callback);
    }
    return array.reduce(function(a,b) { return a + b; });
  }
  function mean(array) {
    return sum(array) / array.length;
  }
  function sd(array) {
    return sum(array,square) / array.length - square(mean(array));
  }
  console.log(sd([1,3,5,7]));
}());
```

## GLOBAL IMPORT 

An Anonymous function which receives globals as parameters.

```
(function(my_list) {
  "use strict";
  console.log(my_list);
  function square(x) {
    return x * x; 
  }
  function sum(array, callback) {
    if (typeof callback === "function") {
      array = array.map(callback);
    }
    return array.reduce(function(a,b) { return a + b; });
  }
  function mean(array) {
    return sum(array) / array.length;
  }
  function sd(array) {
    return sum(array,square) / array.length - square(mean(array));
  }
  console.log(sd(my_list));
}([1,3,5,7]));
```

## REVEALING MODULE PATTERN 

Uses an IIFE to return the module as an object that’s stored in a global variable, keeping all methods and variables private until explicitly exposed:
```
const Stats = (function() {
  "use strict";
  function square(x) {
    return x * x; 
  }
  function sum(array, callback) {
    if (typeof callback === "function") {
      array = array.map(callback);
    }
    return array.reduce(function(a,b) { return a + b; });
  }
  function mean(array) {
    return sum(array) / array.length;
  }
  function sd(array) {
    return sum(array,square) / array.length - square(mean(array));
  }
  return {
    mean: mean,
    standardDeviation: sd
  };
}());

let counts = [1,3,5,7];
Stats.mean(counts);
Stats.standardDeviation(counts);
```

## ES6 MODULES


ES6 provides for a native format for importing and exporting modules from different files
- import function brings the module into the current namespace. 
- export exposes the elements in the module to public so it can be used.
- 
```
//------ scripts.js ------
import {stats} from './stats.js';

console.log(stats.mean(counts));
console.log(stats.standardDeviation(counts));
```

```
//------ stats.js ------
const Stats = function(my_list) {
... ...
}
export const stats = Stats;
```



stats.js:
```
const stats = {
  square(x) {
    return x * x;
  },
  sum(array, callback) {
      if(callback) {
          array = array.map(callback);
      }
          return array.reduce((a,b) => a + b );
  },
  mean(array) {
      return this.sum(array) / array.length;
  },
  variance(array) {
      return this.sum(array,this.square)/array.length - this.square(this.mean(array)) }
}
export default stats;
```

main.js:
```
import {stats} from './stats.js';
var counts = [1,3,5,7];
console.log(stats.mean(counts));
```

# WEB APIs

- Extends the functionality of the browser
- Simplifies complex and often used functions
- Provides easy syntax to complex features
- Typically used by Javascript but it can be html only


## HTML5 DATA ATTRIBUTES 

- Allows for a more structured method for passing configs and attributes from html to javascript.
- Used by all javascript/jQuery plugins to define settings for the plugin.

```
<div id="slideshow" data-type="carousel" data-transition="fade-in" data-auto-start="true">
  <div>Slide 1</div>
  <div>Slide 2</div>
</div>
```
```
const slide = document.getElementById("slideshow");
const type = slide.dataset.type;
const transition = slide.dataset.transition;
const auto_start = slide.dataset.autoStart;

// alternative generic way to get attributes:
const type = slide.getAttribute("data-type");
slide.setAttribute('data-type', 'slider' );
```


## HTML5 GEOLOCATION 

Navigator contains current position information for the client and can be accessed through:

```
navigator.geolocation
-> returns a Geolocation object:

function youAreHere(position) {
  console.log("position: ", position);
}

if(navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(youAreHere);
}
```

Watch for changes:
```
function youHaveMoved(position) {
  console.log("changed position: ", position);
}
if (navigator.geolocation) {
  navigator.geolocation.watchPosition(youHaveMoved);
}
```

Reference: https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API


## HTML5 VIDEO/AUDIO

A clean and extensible approach to embedding media objects.

Pre-html5: 
```
<div>
    <object classid="clsid:02bf25d5-8c17-4b23-bc80-d3488abddc6b" codebase="http://www.apple.com/qtactivex/qtplugin.cab">
      <param name="src"  value="movie.mp4" />
      <param name="autoplay"  value="false" />
      <param name="controller"  value="true" />

      <!--[if !ie] -->
      <object type="video/mp4"  data="movie.mp4">
        <param name="controller"  value="true" />
        <param name="autoplay"  value="false" />
      </object>
      <!--[endif]-->
    </object>
</div>
```

NOW: 
```
<audio src="assets/08_please.mp3" controls>
  Your browser does not support the audio element.
</audio>

<video src="assets/Nearness_on_Vimeo.mp4">
  Your browser does not support the video element.
</video>
```

## HTML5 VIDEO/AUDIO ATTRIBUTES

### Media attributes:
```
<video src="assets/Nearness_on_Vimeo.mp4" autoplay>
  Your browser does not support the video element.
</video>


<video src="assets/Nearness_on_Vimeo.mp4" controls>
  Your browser does not support the video element.
</video>

<video src="assets/Nearness_on_Vimeo.mp4" loop>
  Your browser does not support the video element.
</video>

<video src="assets/Nearness_on_Vimeo.mp4" poster="assets/casa2_hero_1452814189.jpg">
  Your browser does not support the video element.
</video>

<video src="assets/Nearness_on_Vimeo.mp4" preload="none">
  Your browser does not support the video element.
</video>
```

## HTML5 VIDEO/AUDIO CONTROL

Controlling media with Javascript: 
```
const video = document.getElementsByTagName("video")[0];

video.play();
video.pause();
video.volume = 90;
video.muted  = true;
video.loop   = true;
```

Events: 
```
video.addEventListener("pause", function(event) {
  	console.log("video has been paused"); 
})

video.addEventListener("play", function(event) {
  	console.log("video has been paused"); 
})

video.addEventListener("volumechange", function(event) {
  	console.log("video volume has been changed"); 
})

video.addEventListener("timeupdate", function(event) {
  	console.log("video timecode has changed"); 
})

```

### Custom player: 
```
const btn = document.getElementById('play-pause-button');

const mediaPlayer = document.getElementsByTagName("video")[0];

mediaPlayer.controls = false;
btn.addEventListener('click', togglePlayPause.bind(btn));


//play pause toggle
function togglePlayPause() {
   //var btn = document.getElementById('play-pause-button');
   if (mediaPlayer.paused || mediaPlayer.ended) {
	  changeButtonType(btn, 'pause');
      mediaPlayer.play();
   }
   else {
	  changeButtonType(btn, play);
      mediaPlayer.pause();
   }
}

// a generic function to handle button states
function changeButtonType(btn, value) {
   btn.title = value;
   btn.innerHTML = value;
   btn.className = value;
}

//stop
let btn = document.getElementById('stopButton');
btn.addEventListener('click', stopPlayer);

function stopPlayer() {
   mediaPlayer.pause();
   mediaPlayer.currentTime = 0;
}

//mute
let btn = document.getElementById('mute-button');
btn.addEventListener('click', toggleMute);

function toggleMute() {
   const btn = document.getElementById('mute-button');
   if (mediaPlayer.muted) {
      changeButtonType(btn, 'mute');
      mediaPlayer.muted = false;
   }
   else {
      changeButtonType(btn, 'unmute');
      mediaPlayer.muted = true;
   }
}

//reset
let btn = document.getElementById(reset-button');
btn.addEventListener('click', resetPlayer);

function resetPlayer() {
   mediaPlayer.currentTime = 0;
   changeButtonType(playPauseBtn, 'play');
}

// show progress bar
mediaPlayer.addEventListener('timeupdate', updateProgressBar, false);
function updateProgressBar() {
   const progressBar = document.getElementById('progress-bar');
   const percentage = Math.floor((100 / mediaPlayer.duration) *
   mediaPlayer.currentTime);
   progressBar.value = percentage;
   progressBar.innerHTML = percentage + '% played';
}
```


## HTML5 CAMERA API

Navigator provides the getUserMedia Promise object to access the device's camera: 
```
// access the camera for video
navigator.mediaDevices.getUserMedia({
  video: true
})
```

```
// example
const constraints = { video: { facingMode: "user" }, audio: false };

navigator.mediaDevices
    .getUserMedia(constraints)
    .then(function(stream) {
        track = stream.getTracks()[0];
        cam_pic.srcObject = stream;
  })
  .catch(function(error) {
      console.error("Oops. Something is broken.", error);
  });
```

## HTML5 CANVAS

Canvas allows graphics to be drawn onto a web page in real time through JavaScript.
```
<canvas id="canvasDrawing1" width="200" height="100">
This browser doesn't support the canvas element.
</canvas>

const canvas = document.getElementById("canvasDrawing1");
```

### Context:

An object containing all the methods used to draw onto and manipulate the canvas. 
```
// 2D
let context = canvas.getContext("2d");

// 3D
let context3D = canvas.getContext("webgl");
```

## HTML5 CANVAS - ADDING SHAPES

Create Shapes
```
// set defaults
context.fillStyle = "#0000cc"; // a blue fill color
context.strokeStyle = "#ccc"; // a gray stroke color
context.lineWidth = 4;

// draw
context.fillRect(10,10,100,50);

// draw
context.strokeRect(10,100,100,50);


// Lines
context.beginPath();
context.moveTo(20, 50);
context.lineTo(180, 50);
context.moveTo(20, 50);
context.lineTo(20, 90);
context.strokeStyle = "#c00";
context.lineWidth = 10;
context.stroke();

// ARCs
context.beginPath();
context.arc(200, 200, 30, 0, Math.PI * 2, false);
context.strokeStyle = "#ff0";
context.lineWidth = 4;
context.stroke();

// text
context.fillStyle = "#cc0033"; // fill color
context.font = "bold 26px sans-serif";
context.fillText("Hello", 20, 200);

// fill
context.fillStyle = "#443";
context.beginPath();
for (let y = 10; y < 200; y+= 10) {
  console.log(y);
  context.moveTo(10,y);
  context.lineTo(200,y);
  context.lineTo(200,y+(0.05*y));
}
context.fill();

// Image
let img = document.createElement('img');
img.src = 'assets/no_image.gif';
img.addEventListener('load', function() {
	context.drawImage(img, 10, 10 );
});

//Transform
context.scale(1,2) // works on anything drawn after
context.rotate(0.1*Math.PI)
context.translate(50,100)
```

## HTML5 CANVAS - EXAMPLE

```
// draw random circles
for (let y = 0; y < 200; y++) {
  let cx = Math.random()*600;
  let cy = Math.random()*400;
  let cw = Math.random()*15;
  let cc = 'rgba('+ Math.floor(Math.random()*25)*10 + ', ' + Math.floor(Math.random()*25)*10 + ', ' + Math.floor(Math.random()*15)*10 + ')';
  // alpha:
  //let cc = 'rgba('+ Math.floor(Math.random()*25)*10 + ', ' + Math.floor(Math.random()*25)*10 + ', ' + Math.floor(Math.random()*15)*10 + ', ' + Math.random() + ')';

  console.log(y,cx,cy,cw,cc);

  context.fillStyle = cc;
  context.moveTo(cx,cy);
  context.beginPath();

  context.arc(cx, cy, cw, 0, Math.PI * 2, false);
  context.fill();
  context.lineWidth = 1;
  context.stroke();
}
```

## In-class Assignment
Assignment - make a pie or bar chart

```
const data = [
  {name: "Name 1", count: 1045, color: "blue"},
  {name: "Name 2", count: 563, color: "red"},
  {name: "Name 3", count: 231, color: "silver"},
  {name: "Name 4", count: 423, color: "pink"}
];
```

## MORE HTML5 APIs

- Prefetch API
- Speech Synthesis API
- Geolocation API
- Fullscreen API
- Web Storage API
- Battery API
- Clipboard API
- etc...

An exhaustive list: https://developer.mozilla.org/en-US/docs/Web/API
