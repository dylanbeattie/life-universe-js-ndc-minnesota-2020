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

### Useful Links and References

The material in this workshop is based on work I did when writing my talk [The Art of Code](https://www.youtube.com/watch?v=6avJHaC3C2U), which includes detailed discussions of Conway's Game of Life and the Mandelbrot Set, as well as a whole bunch of stuff about esoteric languages, quines, music programming, and the [Rockstar programming language](https://codewithrockstar.com).

#### Canvas API

* [Canvas API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API) docs at developer.mozilla.org

#### Conway's Game of Life

* [LifeWiki](https://www.conwaylife.com/wiki/Main_Page), an extensive wiki all about Conway's Game of Life
* [Golly](http://golly.sourceforge.net/), an open source, cross-platform application for exploring Conway's Game of Life and many other types of cellular automata ([wikipedia](https://en.wikipedia.org/wiki/Golly_(program)))

#### The Mandelbrot Set

* [Mandelbrot set](https://en.wikipedia.org/wiki/Mandelbrot_set) at Wikipedia
* An *incredibly* fast online [Mandelbrot set renderer](https://mandelbrot.ophir.dev/#{%22pos%22:{%22x%22:-0.5,%22y%22:0},%22zoom%22:250}), built using [svelte](https://svelte.dev/), with [source code on Github](https://github.com/lovasoa/mandelbrot)
* ["What's so special about the Mandelbrot Set?"](https://www.youtube.com/watch?v=FFftmWSzgmk) by Numberphile on YouTube
* [HD video of a Mandelbrot zoom to 10^227](https://www.youtube.com/watch?v=PD2XgQOyCCk) on YouTube





