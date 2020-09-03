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

Open the .html file in a browser. Once it is loaded the browser will execute the javascript and draw a picture like the following.

![example1.png](example1.png)

The reference for p5.js is at <https://p5js.org/reference/>

Getting started with p5.js is at <https://p5js.org/get-started/>

Examples using p5.js are at <https://p5js.org/examples/>
