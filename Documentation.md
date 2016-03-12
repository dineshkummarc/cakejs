# Introduction #

I'll be pasting and linking the API documentation from cake.js here. And probably writing some sort of introductory tutorial.

# What CAKE code looks like #

An example with a rotating rectangle:
```
    var c = E.canvas(500, 500)          // create a new canvas element
    var canvas = new Canvas(c)          // create a CAKE [Canvas] for the element
    canvas.fill = [255,255,255,0.8]     // set the Canvas background to 0.8 opacity white
    canvas.clear = false                // show the previous frame behind the current one
    var rect = new Rectangle(100, 100)  // create a CAKE [Rectangle] object
    rect.x = 250                        // move the Rectangle to (250, 250)
    rect.y = 250
    rect.fill = 'green'                 // fill the Rectangle with green color
    // rotate the Rectangle on every frame
    rect.addFrameListener(function(t) {
      this.rotation = ((t / 3000) % 1) * Math.PI * 2 
    })
    canvas.append(rect)                 // append the Rectangle to the Canvas
    document.body.appendChild(c)        // append the canvas element to document body
```


# Using CAKE with Internet Explorer #

The easiest way is to use [Google Chrome Frame](http://code.google.com/chrome/chromeframe). See an example in this [canvas animation demo](http://cs.helsinki.fi/u/ilmarihe/canvas_animation_demo/mozcampeu09.html).

Add `<meta http-equiv="X-UA-Compatible" content="chrome=1">` to the head of your document and the following snippet to your page.

```
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/chrome-frame/1/CFInstall.min.js"> </script> 
<div id="placeholder"></div>
<script>CFInstall.check({ node: "placeholder" });</script> 
```

If you have way too much free time on your hands, you could hypothetically write a SilverLight implementation of the Canvas API. ExplorerCanvas doesn't work at all well for CAKE. Last I checked, ExplorerCanvas's VML renderer chokes on the animations and will likely make IE hang or crash or both.

# How CAKE's inheritance model works: the Klass object #

> The Klass object is used to do inheritance in a less cumbersome fashion than unaugmented JavaScript. To create a new class, you do `MyClass = Klass(superclass, class_body)`.

> Calling Klass returns a new constructor function created from the parameters to Klass. The prototypes of the parameters (or the parameters themselves) are merged with the new constructor's prototype. Finally, the constructor's prototype is merged with the constructor itself, so that you can write `Shape.getArea.call(this)` instead of `Shape.prototype.getArea.call(this)`.

> The constructor calls the class's `#initialize` with the constructor's arguments, so you can easily derive a class from another and customize its initialization procedure, as you can see from the example below.

```
  Shape = Klass({
    getArea : function() {
      raise('No area defined!')
    }
  })

  Rectangle = Klass(Shape, {
    initialize : function(x, y) {
      this.x = x
      this.y = y
    },

    getArea : function() {
      return this.x * this.y
    }
  })

  Square = Klass(Rectangle, {
    initialize : function(s) {
      Rectangle.initialize.call(this, s, s)
    }
  })

  new Square(5).getArea()
  //=> 25
```


# Main classes #

  * [Canvas](Canvas.md) is the canvas manager class. You need to wrap a canvas element in one to use CAKE.
  * CanvasNode is the base class for the CAKE scene graph. All the other scene graph nodes derive from it.


## Scene graph node classes ##

  * [AudioNode](AudioNode.md) is a CanvasNode used to play a sound.
  * [ElementNode](ElementNode.md) is a CanvasNode that wraps an HTML element.
  * [Line](Line.md) is a line drawn from x1,y1 to x2,y2. Lines are stroked by default.
  * [Circle](Circle.md) is used for creating circular paths.
  * [Ellipse](Ellipse.md) is used for drawing ellipses.
  * [Spiral](Spiral.md) draws a strokeable spiral path.
  * [Rectangle](Rectangle.md) is used for creating rectangular paths.
  * [Polygon](Polygon.md) is used for creating paths consisting of straight line segments.
  * [CatmullRomSpline](CatmullRomSpline.md) draws a Catmull-Rom spline, with optional looping and path closing. Handy for motion paths.
  * [Path](Path.md) is used for creating custom paths. The Path segments are used as `[methodName, arguments]`-calls on the canvas drawing context.
  * [ImageNode](ImageNode.md) is used for drawing images.
  * [TextNode](TextNode.md) is used for drawing text on a canvas.


## Fills and strokes ##

  * A value of `null` uses the inherited setting. `false` and `'none'` turn off the fill or stroke.
  * Colors can be given as a CSS color string or an array of color components.
  * [Gradient](Gradient.md) is a linear or radial color gradient that can be used as a stroke or fill.
  * [Pattern](Pattern.md) is a possibly repeating image that can be used as a stroke or fill.

> Examples of possible fill / stroke settings.
```
  null      // use the inherited value and on/off setting
  true      // turn on fill / stroke and use the inherited value
  false     // turn off fill / stroke
  'none'    // turn off fill / stroke

  'white'   // CSS color name
  '#fff'    // short CSS hex color
  '#ffffff' // long CSS hex color
  'rgba(255,255,255, 1.0)' // CSS RGBA color. RGB and HSLA colors work too, if your browser supports them.
  [255, 255, 255, 1.0] // color component array 
  new Gradient(...)    // gradient fill / stroke
  new Pattern(myImage, 'no-repeat') // pattern fill / stroke
```


## SVGParser ##

> [SVGParser](SVGParser.md) is an [SVG](http://www.w3.org/TR/SVG/) parser for simple documents. Converts SVG DOM to CAKE scene graph.
> SVGParser has an emphasis on importing graphical images, not on the "HTML-killer" features of SVG.
```
  var svgNode = SVGParser.parse(
    svgRootElement, filename, containerWidth, containerHeight, fontSize
  )
```
> Features:
    * svg-tag width and height, viewBox clipping.
    * Clipping (objectBoundingBox clipping too)
    * Paths, rectangles, ellipses, circles, lines, polylines and polygons
    * Simple untransformed text using HTML
    * Nested transforms
    * Transform lists (transform="rotate(30) translate(2,2) scale(4)")
    * Gradient and pattern transforms
    * Strokes with miter, joins and caps
    * Flat fills and gradient fills, ditto for strokes
    * Parsing simple stylesheets (tag, class or id)
    * Images
    * Non-pixel units (cm, mm, in, pt, pc, em, ex, %)
    * use-tags
    * preserveAspectRatio
    * Dynamic gradient sizes (objectBoundingBox, etc.)
    * Markers (though buggy)
    * SMIL animation (incomplete, property model is wrong)

> Some of the several missing features:
    * Masks
    * Patterns
    * viewBox clipping for elements other than marker and svg
    * Text styling
    * tspan, tref, textPath, many things text
    * Fancy style rules (tag .class + #foo > bob#alice { ... })
    * Filters
    * Dashed strokes