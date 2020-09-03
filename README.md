## p5.js

Processing.js has been replaced with [p5.js](https://p5js.org/).  According to the [processing-js repo](https://github.com/processing-js/processing-js):

>With the development of p5js and the API advances in Processing itself, as well as Processing.js itself having been in maintenance mode for quite a few years now, this project has been archived as of December 2018.

To create p5.js apps, p5.js (or the compressed p5.min.js) is needed. These files are available at <https://p5js.org/download/>.

Put the .js file(s) in a folder.  Then, create an .html file in the same folder with the following contents. The .html file needs to be created/edited with a plain text editor such as Atom, Visual Studio Code, etc.

```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>p5.js test1</title>
    
    <style type="text/css">
		body{ background-color: black; }
    </style>
    <script src="p5.js"></script>
  </head>
  <body>
    <script>
		function setup() {
		  createCanvas(800, 800);
		}

		function draw() {
		  if (mouseIsPressed) {
			fill(128);
		  } else {
			fill(255);
		  }
		  ellipse(mouseX, mouseY, 80, 80);
		}
    </script>
  </body>
</html>
```

The above is an HTML 5 document. The ```<script src="p5.js"></script>``` in the head of the web page loads the p5.js javascript file which contains the library of code to draw pictures.  If you use the compressed version, replace p5.js with p5.min.js.

In the body is a ```<script></script>``` block that contains two javascript functions: ```setup()``` and ```draw()```. ```setup()``` is called by code in p5.js to do the setup.  In the example code, it is where the canvas of 800 x 800 is created using ```createCanvas(800, 800)```.  The canvas is where the picture is drawn. The ```draw()``` function is where code is placed to draw the picture. In the case of the draw() function shown, the state of the mouse button is used  to set the fill color (for filled objects that are drawn after it is set). The location of the mouse cursor is used to draw 80 x 80 ellipses (circles) with the fill color.

Open the .html file in a browser. Once it is loaded the browser will execute the javascript and draw a picture like the following. The html file is also available in ![example1.html](example1.html).

![example1.png](example1.png)

The reference for p5.js is at <https://p5js.org/reference/>

Getting started with p5.js is at <https://p5js.org/get-started/>

Examples using p5.js are at <https://p5js.org/examples/>

The following image was created using the scripts shown in the html document below. It takes some time for the image to appear. This image requires a lot of computations to create it. If nothing appear immediately...wait. This is [The Mandelbrot Set example](https://p5js.org/examples/simulate-the-mandelbrot-set.html) in the examples provided on the p5.js web site. The following html is also available in [mandelbrot.html](mandelbrot.html)  in this repository.

![mandelbrot](mandelbrot.png)

```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>p5.js test1</title>
    
    <style type="text/css">
		body{ background-color: black; }
    </style>
    <script src="p5.js"></script>
  </head>
  <body>
    <script>

		function setup() {
		  createCanvas(710, 400);
		  pixelDensity(1);
		  noLoop();
		}

		function draw() {
		  background(0);

		  // Establish a range of values on the complex plane
		  // A different range will allow us to "zoom" in or out on the fractal

		  // It all starts with the width, try higher or lower values
		  const w = 4;
		  const h = (w * height) / width;

		  // Start at negative half the width and height
		  const xmin = -w/2;
		  const ymin = -h/2;

		  // Make sure we can write to the pixels[] array.
		  // Only need to do this once since we don't do any other drawing.
		  loadPixels();

		  // Maximum number of iterations for each point on the complex plane
		  const maxiterations = 100;

		  // x goes from xmin to xmax
		  const xmax = xmin + w;
		  // y goes from ymin to ymax
		  const ymax = ymin + h;

		  // Calculate amount we increment x,y for each pixel
		  const dx = (xmax - xmin) / (width);
		  const dy = (ymax - ymin) / (height);

		  // Start y
		  let y = ymin;
		  for (let j = 0; j < height; j++) {
			// Start x
			let x = xmin;
			for (let i = 0; i < width; i++) {

			  // Now we test, as we iterate z = z^2 + cm does z tend towards infinity?
			  let a = x;
			  let b = y;
			  let n = 0;
			  while (n < maxiterations) {
				const aa = a * a;
				const bb = b * b;
				const twoab = 2.0 * a * b;
				a = aa - bb + x;
				b = twoab + y;
				// Infinty in our finite world is simple, let's just consider it 16
				if (dist(aa, bb, 0, 0) > 16) {
				  break;  // Bail
				}
				n++;
			  }

			  // We color each pixel based on how long it takes to get to infinity
			  // If we never got there, let's pick the color black
			  const pix = (i+j*width)*4;
			  const norm = map(n, 0, maxiterations, 0, 1);
			  let bright = map(sqrt(norm), 0, 1, 0, 255);
			  if (n == maxiterations) {
				bright = 0;
			  } else {
				// Gosh, we could make fancy colors here if we wanted
				pixels[pix + 0] = bright;
				pixels[pix + 1] = bright;
				pixels[pix + 2] = bright;
				pixels[pix + 3] = 255;
			  }
			  x += dx;
			}
			y += dy;
		  }
		  updatePixels();
		}

    </script>
  </body>
</html>

```
