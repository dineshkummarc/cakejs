# Introduction #


> [Canvas](Canvas.md) is the canvas manager class. It takes a canvas element and handles updating its childNodes and drawing them onto the canvas.

> The normal way to use CAKE is to create a Canvas for a canvas element and attaching the scene to the Canvas object.

> You can set the Canvas's background color by setting the `fill` property to a color, Pattern or Gradient. If you want to preserve the previous frame image, set the `clear` property to false. As an example, preserving the previous frame can be used for doing a motion trail effect by using a transparent background so that it shows the previous frames beneath the current one.

> An example with a rotating rectangle:
```
    var c = E.canvas(500, 500)
    var canvas = new Canvas(c)
    canvas.fill = [255,255,255,0.8]
    canvas.clear = false
    var rect = new Rectangle(100, 100)
    rect.x = 250
    rect.y = 250
    rect.fill = 'green'
    rect.addFrameListener(function(t) {
      this.rotation = ((t / 3000) % 1) * Math.PI * 2
    })
    canvas.append(rect)
    document.body.appendChild(c)
```

> To use a Canvas as a manually updated image you can set `redrawOnlyWhenChanged` to true. When you want the Canvas to be redrawn, set its `changed` property to true:
```
    var canvas = new Canvas(E.canvas(200,40), {
      isPlaying : false,
      redrawOnlyWhenChanged : true
    })
    var c = new Circle(20)
    c.x = 100
    c.y = 20
    c.fill = 'red'
    c.addFrameListener(function(t) {
      if (this.root.absoluteMouseX != null) {
        this.x = this.root.mouseX // relative to canvas surface
        this.root.changed = true
      }
    })
    canvas.append(c)
```

> You can also use `onFrame`-calls to make the Canvas redraw itself:
```
    var canvas = new Canvas(E.canvas(200,40), {
      isPlaying : false,
      fill : 'white'
    })
    var c = new Circle(20)
    c.x = 100
    c.y = 20
    c.fill = 'red'
    canvas.append(c)
    canvas.onFrame()
```

> Using `onFrame` is also the recommended way to use a Canvas inside another Canvas:
```
    var canvas = new Canvas(E.canvas(200,40), {
      isPlaying : false
    })
    var c = new Circle(20, {
      x: 100, y: 20,
      fill: 'red'
    })
    canvas.append(c)

    var topCanvas = new Canvas(E.canvas(500, 500))
    var canvasImage = new ImageNode(canvas.canvas, {x: 250, y: 250})
    topCanvas.append(canvasImage)
    canvasImage.addFrameListener(function(t) {
      this.rotation = (t / 3000 % 1) * Math.PI * 2
      canvas.onFrame(t)
    })
```



# Object API #

Canvas derives from CanvasNode.

## Constructor ##

```
  new Canvas(canvas, config)
```
> Canvas constructor takes a canvas element and an optional config object that is merged with the Canvas object.

## Properties ##

```
  clear : true,
  frameLoop : false,
  recording : false,
  opacity : 1,
  frame : 0,
  elapsed : 0,
  frameDuration : 30,
  speed : 1.0,
  time : 0,
  fps : 0,
  currentRealFps : 0,
  currentFps : 0,
  fpsFrames : 30,
  startTime : 0,
  realFps : 0,
  fixedTimestep : false,
  playOnlyWhenFocused : true,
  isPlaying : true,
  redrawOnlyWhenChanged : false,
  changed : true,
  drawBoundingBoxes : false,
  cursor : 'default',

  mouseDown : false,
  mouseEvents : [],

  // absolute pixel coordinates from canvas top-left
  absoluteMouseX : null,
  absoluteMouseY : null,

  /*
    Coordinates relative to the canvas's surface scale.
    Example:
      canvas.width
      #=> 100
      canvas.style.width
      #=> '100px'
      canvas.absoluteMouseX
      #=> 50
      canvas.mouseX
      #=> 50

      canvas.style.width = '200px'
      canvas.width
      #=> 100
      canvas.absoluteMouseX
      #=> 100
      canvas.mouseX
      #=> 50
  */
  mouseX : null,
  mouseY : null,

  elementNodeZIndexCounter : 0,
```

## Methods ##

```

  initialize : function(canvas, config)

  /**
    Integrating CAKE scene graph with the DOM event model
    */
  // FIXME
  removeEventListeners : function() {},
  addEventListeners : function()
  updateKeys : function(ev)
  addWindowEventListeners : function()
  removeWindowEventListeners : function()
  addMouseEvent : function(x,y,mouseDown)
  allocMouseEvent : function()
  freeMouseEvent : function(ev)
  clearMouseEvents : function()

  /**
    Start frame loop.

    The frame loop is a setInterval where #onFrame is called every
    #frameDuration milliseconds.
    */
  play : function()

  /**
    Stop frame loop.
    */
  stop : function()

  dispatchEvent : function(ev)

  /**
    The frame loop function. Called every #frameDuration milliseconds.
    Takes an optional external time parameter (for syncing Canvases with each
    other, e.g. when using a Canvas as an image.)

    If the time parameter is given, the second parameter is used as the frame
    time delta (i.e. the time elapsed since last frame.)

    If time or timeDelta is not given, the canvas computes its own timeDelta.

    @param time The external time. Optional.
    @param timeDelta Time since last frame in milliseconds. Optional.
    */
  onFrame : function(time, timeDelta)

  /**
    Returns the canvas drawing context object.

    @return Canvas drawing context
    */
  getContext : function()

  /**
    Gets and returns an augmented canvas 2D drawing context.

    The canvas 2D context is augmented by setter functions for all
    its instance variables, making it easier to record canvas operations in
    a cross-browser fashion.
    */
  get2DContext : function()

  /**
    Creates and returns a mock drawing context.

    @return Mock drawing context
    */
  getMockContext : function()

  /**
    Creates and returns a recording context for recording drawing commands.

    @return Recording context
    */
  getRecordingContext : function()

  /**
    Canvas drawPickingPath uses the canvas rectangle as its path.

    @param ctx Canvas drawing context
    */
  drawPickingPath : function(ctx)

  isPointInPath : function(x,y)

  /**
    Sets globalAlpha to this.opacity and clears the canvas if #clear is set to
    true. If #fill is also set to true, fills the canvas rectangle instead of
    clearing (using #fillStyle as the color.)

    @param ctx Canvas drawing context
    */
  draw : function(ctx)
```