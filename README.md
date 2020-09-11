# Life, the Universe, and JavaScript
> A half-day workshop that uses modern JavaScript to explore Conway’s Game of Life, complex numbers, fractal geometry and the Mandelbrot set. You’ll learn how to implement Conway’s Game of Life in JavaScript, using the HTML Canvas API to render the Game of Life directly in your web browser. We’ll look at how to load and run classic Game of Life patterns - gliders, glider guns, spaceships - and how to use those patterns to build simple logic gates and circuits. 
>
> In the second part of the workshop, you’ll learn about imaginary numbers, complex arithmetic - and how this mathematical curiosity holds the key to one of the most astonishing objects in nature, the Mandelbrot set. We’ll implement a library in JavaScript to do arithmetic with complex numbers, and then use this library and the browser canvas API to draw the famous Mandelbrot set, and explore the relationship between the Mandelbrot set and the family of related shapes known as the Julia sets.

## What's here?

Right now, nothing! But over the course of the workshop, I'll be showing you how to implement some fairly neat things using modern JavaScript and browser APIs, and we'll be pushing code and examples to this repository as we go. Here's how we're going to be laying things out:

```
canvas/
	- Introduction to the HTML Canvas API, which we'll be using throughout the workshop
conway/
	- Conway's Game of Life implemented in JavaScript
mandel/
	- The Mandelbrot Set
```

## Part 1: The HTML Canvas API

#### Drawing with the Canvas API

* Create a blank web page.
* Add an HTML `canvas` element to the page
* Use `canvas.getContext("2d")` to retrieve a drawing context
* Use `context.fillStyle` and `context.fillRect` to draw a chessboard pattern (an 8x8 grid of alternating black & white squares)
* Customise your chessboard by choosing two contrasting colours of your choice instead of black and white. 

#### Interacting with the Canvas

* Model the state of your chessboard as a nested array of JavaScript values, where "truthy" values are your primary colour, and "falsy" values are your secondary colour

* Add a `render` method that will take the state of your chessboard and draw it onto the canvas
* Click handlers: add an onclick handler to the chessboard canvas that toggles the colour of the square you clicked on 
  * Your handler should modify the state of the **model** and then call the `render` method to draw the updated model onto the screen

## Part 2: Conway's Game of Life

#### The Rules of Life

* The Game of Life is played on a grid of cells
* A cell is either living or dead
* A living cell with 0 or 1 living neighbours will die of loneliness
* A living cell with 4 or more living neighbours will die of overcrowding
* A living cell with 2 or 3 neighbours will survive to the next generation
* A dead cell with exactly 3 neighbours will come back to life

#### Objective

To implement the Game of Life in a web browser:

* You can draw configurations by clicking cells with the mouse to toggle them on/off (living/dead)
* You can run one 'round' of the game by clicking the 'Tick' button
* You can run the game by clicking the 'Start' button
* You can stop the game by clicking the 'Stop' button
* Bonus credit: you can load and save configurations to your local machine.

#### Step by Step

We'll be reusing the code and ideas developed in part 1, and adding some rules, behaviour and animation to run Conway's Game of Life in a browser.

* Create a JavaScript object to model a single cell on the game grid. A cell needs to store two properties:
  * `isAliveRightNow`: is this cell currently alive?
  * `isAliveNextTime`: will this cell survive the current cycle?
* Each cell also needs to know which grid it belongs to, and its position on that grid
  * This is necessary so that for a given cell, we can ask it to count its living neighbours
* Figure out how to implement a Grid data structure in JavaScript for storing a 2-dimensional array of Cell objects
  * Clue: JavaScript doesn't have 2D arrays, but you can nest arrays inside each other...
* Implement two methods on your Cell object:
  * `prepareToEvolve()` - will count the cell's neighbours and set the `isAliveNextTime` property according to the rules of Life.
  * `evolve()` - will update the cell's `isAliveRightNow` property to reflect the `isAliveNextTime` property.
* Create a `tick` method on your Grid, that will advance the whole game grid by a single generation
  * this method should call `prepareToEvolve() ` on every cell in turn, and then call `evolve()` on every cell in turn.
* Add three buttons to your page:
  * A "Tick" button - should advance the game by a single tick
  * A "Start" button - should start the game running (use `window.setInterval` to called `tick` repeatedly)
  * A "Stop" button - should stop the game running

#### Extra Credit: Loading and Saving Configurations

Add two more buttons to your page:

* "Save" - will prompt you to save the current layout to your local filesystem
* "Open" - will allow you to open a saved layout from your local filesystem

Tips:

```javascript
// Save a file using client-side JavaScript
let data = { foo: "bar", hello: "world", count: 3 }; // or whatever data you want to save.
let json = JSON.stringify(data);
window.location = "data:application/octet-stream," + encodeURIComponent(json);

// Open and read a file using client-side JavaScript
<input type="file" id="fileinput" />
<script type="text/javascript">
function readFile(evt) {
	var file = evt.target.files[0];   
	if (file) {
		var reader = new FileReader();
		reader.onload = function(e) { 
			var text = e.target.result;
			console.log(text); // or whatever you want to do with your data.
		}
		r.readAsText(f);
	} else { 
		alert("Failed to load file");
	}
}
</script>
```

## Part 3: The Mandelbrot Set

#### Objective:

1. Draw the Mandelbrot set in a web browser, using `for()` loops and the canvas `fillRect()` method
2. Go "wow, that's really slow"
3. Optimise it in all kinds of interesting ways

#### Complex Numbers and Drawing the Mandelbrot Set

1. Implement a Complex object in JavaScript that will let us do arithmetic with complex numbers
   1. A complex number has a real part R and an imaginary part I, and is often written as *x + yi*
   2. The **absolute value** of a complex number *x + yi* is given by *sqrt(x<sup>2</sup> + y<sup>2</sup>)* 
   3. Create methods to add and multiply complex numbers
      1. The result of adding two complex numbers (a + bi) + (c + di) is a new complex number (a+b) + (c+d)i
      2. The result of multiplying two complex numbers (a + bi) * (c + di) is (ac) + (a*di) + (bi * c) - (b*d)
2. Figure out how to map pixel coordinates (0,0) => (800,800) to points in the complex plane from (-2,1.5i) => (2,-1.5i)
3. Choose a THRESHOLD value (try 100) - this is how many times we'll test each number before we decide that it lies within our set.
4. For each pixel:
   1. Calculate the complex number *z* corresponding to that pixel's coordinates
   2. Repeatedly square z and then add the original value c, so *z => z<sup>2</sup> + c*
   3. If the absolute value of the result is > 2, the point lies *outside* the Mandelbrot set - colour the corresponding pixel white
   4. If after THRESHOLD iterations, the absolute value is still < 2, then the point lies *inside* the Mandelbrot set - colour the corresponding pixel black
5. Colour pixels by setting `context.fillStyle` and then using the `context.fillRect(x,y,width,height)` method we've used previously.

### Making it Pretty

For points outside the set, instead of colouring the corresponding pixel white, choose a colour based on the number of iterations it took to exceed the limit.

### Making it Fast

Finally, we'll apply a bunch of optimisations to take our total rendering time for an 800x800 pixel Mandelbrot set from 2-3 minutes down to less than 1 second. I'll walk you through all this and share the code as I go so you can refer back to it :)

* Use the `console.time()` and `console.timeEnd()` methods to measure just how long our rendering is taking.
* Isolate the complex arithmetic inside a JavaScript background worker
* Use `context.putImageData()`, which is considerably faster than `context.fillRect()` when working with the canvas API.

## Useful Links and References

The material in this workshop is based on work I did when writing my talk [The Art of Code](https://www.youtube.com/watch?v=6avJHaC3C2U), which includes detailed discussions of Conway's Game of Life and the Mandelbrot Set, as well as a whole bunch of stuff about esoteric languages, quines, music programming, and the [Rockstar programming language](https://codewithrockstar.com).

#### Canvas API

* [Canvas API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API) docs at developer.mozilla.org

#### Conway's Game of Life

* [LifeWiki](https://www.conwaylife.com/wiki/Main_Page), an extensive wiki all about Conway's Game of Life
* [Golly](http://golly.sourceforge.net/), an open source, cross-platform application for exploring Conway's Game of Life and many other types of cellular automata ([wikipedia](https://en.wikipedia.org/wiki/Golly_(program)))

#### The Mandelbrot Set

* [Mandelbrot set](https://en.wikipedia.org/wiki/Mandelbrot_set) at Wikipedia
* An *incredibly* fast online [Mandelbrot set renderer](https://mandelbrot.ophir.dev/), built using [svelte](https://svelte.dev/), with [source code on Github](https://github.com/lovasoa/mandelbrot)
* ["What's so special about the Mandelbrot Set?"](https://www.youtube.com/watch?v=FFftmWSzgmk) by Numberphile on YouTube
* [HD video of a Mandelbrot zoom to 10^227](https://www.youtube.com/watch?v=PD2XgQOyCCk) on YouTube





