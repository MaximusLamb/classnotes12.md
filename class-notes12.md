# The Canvas Element
* The canvas element only has two attributes **width** and **height**.
* With no attributes specified it automatically is set to 300px wide and 150 high.
```html 
As a consequence of the way fallback is provided, unlike the <img> element, the <canvas> element requires the closing tag (</canvas>). If this tag is not present, the rest of the document would be considered the fallback content and wouldn't be displayed.
```
## The rendering context
```html
The <canvas> element creates a fixed-size drawing surface that exposes one or more rendering contexts, which are used to create and manipulate the content shown. In this tutorial, we focus on the 2D rendering context. Other contexts may provide different types of rendering; for example, WebGL uses a 3D context based on OpenGL ES.

The canvas is initially blank. To display something, a script first needs to access the rendering context and draw on it. The <canvas> element has a method called getContext(), used to obtain the rendering context and its drawing functions. getContext() takes one parameter, the type of context. For 2D graphics, such as those covered by this tutorial, you specify "2d" to get a CanvasRenderingContext2D.
```

The script includes a function called **draw()**, which is executed once the page finishes loading; this is done by listening for the load event on the document. This function, or one like it, could also be called using **window.setTimeout()**, **window.setInterval()**, or any other event handler, as long as the page has been loaded first.

# Drawing Shapes with Canvas
## Coordinate Space
First let's look at the rectangle. There are three functions that draw rectangles on the canvas:

```html
fillRect(x, y, width, height)
Draws a filled rectangle.
```
```html
strokeRect(x, y, width, height)
Draws a rectangular outline.
```
```html
clearRect(x, y, width, height)
Clears the specified rectangular area, making it fully transparent.
```
Each of these three functions takes the same parameters. x and y specify the position on the canvas (relative to the origin) of the top-left corner of the rectangle. width and height provide the rectangle's size.

# Drawing paths
A path is a list of points, connected by segments of lines that can be of different shapes, curved or not, of different width and of different color. A path, or even a subpath, can be closed. To make shapes using paths, we take some extra steps:

1. First, you create the path.
2. Then you use drawing commands to draw into the path.
3. Once the path has been created, you can stroke or fill the path to render it.
### Here are the functions used to perform these steps:

* **beginPath()**
Creates a new path. Once created, future drawing commands are directed into the path and used to build the path up.
* Path methods
Methods to set different paths for objects.
* **closePath()**
Adds a straight line to the path, going to the start of the current sub-path.
* **stroke()**
Draws the shape by stroking its outline.
* **fill()**
Draws a solid shape by filling the path's content area.
### The **first step** to create a path is to call the **beginPath()**.
 * Internally, paths are stored as a list of sub-paths (lines, arcs, etc) which together form a shape. Every time this method is called, the list is reset and we can start drawing new shapes.
### The **second step** is calling the methods that actually specify the paths to be drawn.
### The **third, and an optional step**, is to call **closePath()**. This method tries to close the shape by drawing a straight line from the current point to the start. If the shape has already been closed or there's only one point in the list, this function does nothing.
One very useful function, which doesn't actually draw anything but becomes part of the path list described above, is the **moveTo()** function. You can probably best think of this as lifting a pen or pencil from one spot on a piece of paper and placing it on the next.
### Moving the Pen
```html
moveTo(x,y)
```
This moves the pen to the coordinates specified in **x** and **y**.
When the canvas is initialized or **beginPath()** is called, you typically will want to use the **moveTo()** function to place the starting point somewhere else. You could also use **moveTo()** to draw unconnected paths.
### Lines
* For drawing straight lines use the **lineto()** method.
```html
lineTo(x,y)
```
This Draws A line from the current specified position to the position of **x** and **y**.
* This method takes two arguments, **x** and **y**, which are the coordinates of the line's end point. The starting point is dependent on previously drawn paths, where the end point of the previous path is the starting point for the following, etc. The starting point can also be changed by using the **moveTo()** method.
### Arcs
To draw arcs or circles, we use the **arc()** or **arcTo()** methods.
```html
arc(x, y, radius, startAngle, endAngle, anticlockwise)
```
* Draws an arc which is centered at (x, y) position with radius r starting at startAngle and ending at endAngle going in the given direction indicated by anticlockwise (defaulting to clockwise).
```html
arcTo(x1, y1, x2, y2, radius)
```
Draws an arc with the given control points and radius, connected to the previous point by a straight line.
### Bezier and Quadratic curves
The next type of paths available are Bézier curves, available in both cubic and quadratic varieties. These are generally used to draw complex organic shapes.
```html
quadraticCurveTo(cp1x, cp1y, x, y)
```
Draws a quadratic Bézier curve from the current pen position to the end point specified by **x** and **y**, using the control point specified by **cp1x** and **cp1y**.
```html
bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)
```
Draws a cubic Bézier curve from the current pen position to the end point specified by **x** and **y**, using the control points specified by **(cp1x, cp1y)** and **(cp2x, cp2y)**.
The difference between these can best be described using the image on the right. A quadratic Bézier curve has a start and an end point and just one control point while a cubic Bézier curve uses two control points.

The **x** and **y** parameters in both of these methods are the coordinates of the end point. **cp1x** and **cp1y** are the coordinates of the first control point, and **cp2x** and **cp2y** are the coordinates of the second control point.