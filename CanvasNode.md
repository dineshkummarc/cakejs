# Introduction #

CanvasNode is the base CAKE scene graph node. All the other scenegraph nodes derive from it. A plain CanvasNode does no drawing, but it can be used for grouping other nodes and setting up the group's drawing state.
```
  var scene = new CanvasNode({x: 10, y: 10})
```
> The usual way to use CanvasNode is to append them to a Canvas object:
```
    var scene = new CanvasNode()
    scene.append(new Rectangle(40, 40, {fill: 'black'}))
    var elem = E.canvas(400, 400)
    var canvas = new Canvas(elem)
    canvas.append(scene)
```
> You can also use CanvasNode to draw directly to a canvas element:
```
    var scene = new CanvasNode()
    scene.append(new Circle(40, {x:200, y:200, stroke: 'black'}))
    var elem = E.canvas(400, 400)
    scene.handleDraw(CanvasSupport.getContext(elem))
```

# Object API #

CanvasNode derives from Animatable and Transformable.

## Constructor ##

## Properties ##
```
  // whether to draw the node and its childNodes or not
  visible : true

  // whether to draw the node (doesn't affect subtree)
  drawable : true

  // the CSS display property can be used to affect 'visible'
  // false     => visible = visible
  // 'none'    => visible = false
  // otherwise => visible = true
  display : null

  // the CSS visibility property can be used to affect 'drawable'
  // false     => drawable = drawable
  // 'hidden'  => drawable = false
  // otherwise => drawable = true
  visibility : null,

  // whether this and the subtree from this register mouse hover
  catchMouse : true,

  // Whether this object registers mouse hover. Only set this to true when you
  // have a drawable object that can be picked. Otherwise the object requires
  // a matrix inversion on Firefox 2 and Safari, which is slow.
  pickable : false,

  // true if this node or one of its descendants is under the mouse
  // cursor and catchMouse is true
  underCursor : false,

  // zIndex in relation to sibling nodes (note: not global)
  zIndex : 0,

  // x translation of the node
  x : 0,

  // y translation of the node
  y : 0,

  // scale factor: number for uniform scaling, [x,y] for dimension-wise
  scale : 1,

  // Rotation of the node, in radians.
  //
  // The rotation can also be the array [angle, cx, cy],
  // where cx and cy define the rotation center.
  //
  // The array form is equivalent to
  // translate(cx, cy); rotate(angle); translate(-cx, -cy);
  rotation : 0,

  // Transform matrix with which to multiply the current transform matrix.
  // Applied after all other transformations.
  matrix : null,

  // Transform matrix with which to replace the current transform matrix.
  // Applied before any other transformation.
  absoluteMatrix : null,

  // SVG-like list of transformations to apply.
  // The different transformations are:
  // ['translate', [x,y]]
  // ['rotate', [angle, cx, cy]] - (optional) cx and cy are the rotation center
  // ['scale', [x,y]]
  // ['matrix', [m11, m12, m21, m22, dx, dy]]
  transformList : null,

  // fillStyle for the node and its descendants
  // Possibilities:
  //   null // use the previous
  //   true      // use the previous but do fill
  //   false     // use the previous but don't do fill
  //   'none'    // use the previous but don't do fill
  //
  //   'white'
  //   '#fff'
  //   '#ffffff'
  //   'rgba(255,255,255, 1.0)'
  //   [255, 255, 255, 1.0]
  //   new Gradient(...)
  //   new Pattern(myImage, 'no-repeat')
  fill : null,

  // strokeStyle for the node and its descendants
  // Possibilities:
  //   null // use the previous
  //   true      // use the previous but do stroke
  //   false     // use the previous but don't do stroke
  //   'none'    // use the previous but don't do stroke
  //
  //   'white'
  //   '#fff'
  //   '#ffffff'
  //   'rgba(255,255,255, 1.0)'
  //   [255, 255, 255, 1.0]
  //   new Gradient(...)
  //   new Pattern(myImage, 'no-repeat')
  stroke : null,

  // stroke line width
  strokeWidth : null,

  // stroke line cap style ('butt' | 'round' | 'square')
  lineCap : null,

  // stroke line join style ('bevel' | 'round' | 'miter')
  lineJoin : null,

  // stroke line miter limit
  miterLimit : null,

  // set globalAlpha to this value
  absoluteOpacity : null,

  // multiply globalAlpha by this value
  opacity : null,

  // fill opacity
  fillOpacity : null,

  // stroke opacity
  strokeOpacity : null,

  // set globalCompositeOperation to this value
  // Possibilities:
  // ( 'source-over' |
  //   'copy' |
  //   'lighter' |
  //   'darker' |
  //   'xor' |
  //   'source-in' |
  //   'source-out' |
  //   'destination-over' |
  //   'destination-atop' |
  //   'destination-in' |
  //   'destination-out' )
  compositeOperation : null,

  // Color for the drop shadow
  shadowColor : null,

  // Drop shadow blur radius
  shadowBlur : null,

  // Drop shadow's x-offset
  shadowOffsetX : null,

  // Drop shadow's y-offset
  shadowOffsetY : null,

  // HTML5 text API
  font : null,
  // horizontal position of the text origin
  // 'left' | 'center' | 'right' | 'start' | 'end'
  textAlign : null,
  // vertical position of the text origin
  // 'top' | 'hanging' | 'middle' | 'alphabetic' | 'ideographic' | 'bottom'
  textBaseline : null,

  // What cursor style should be used when hovering the CanvasNode.
  cursor : null

  // Does the CanvasNode needs redraw?
  changed : true

```

## Methods ##

```

  /**
    Initialize the CanvasNode and merge an optional config object with it.
    */
  initialize : function(config)

  /**
    Create a clone of the node and its subtree.
    */
  clone : function()

  /**
    Alias for clone
    */
  cloneNode : function()

  /**
    Returns this node's next sibling or null if this node is the last node.
    */
  getNextSibling : function()

  /**
    Returns this node's previous sibling or null if this node is the first node.
    */
  getPreviousSibling : function()

  /**
    Gets node by id.
    */
  getElementById : function(id) 

  /**
    Alias for getElementById.
    */
  $ : function(id)

  /**
    Alias for append().

    @param Node[s] to append
    */
  appendChild : function()

  /**
    Appends arguments as childNodes to the node.

    Adding a child sets child.parent to be the node and calls
    child.setRoot(node.root)

    @param Node[s] to append
    */
  append : function(obj) 

  /**
    Removes all childNodes from the node.
    */
  removeAllChildren : function()

  /**
    Alias for remove().

    @param Node[s] to remove
    */
  removeChild : function()

  /**
    Removes arguments from the node's childNodes.

    Removing a child sets its parent to null and calls
    child.setRoot(null)

    @param Child node[s] to remove
    */
  remove : function(obj)

  /**
    Calls this.parent.removeChild(this) if this.parent is set.
    */
  removeSelf : function() 

  /**
    Returns true if this node's subtree contains obj. (I.e. obj is this or
    obj's parent chain includes this.)

    @param obj Node to look for
    @return True if obj is in this node's subtree, false if it isn't.
    */
  contains : function(obj)

  /**
    Set this.root to the given value and propagate the update to childNodes.

    @param root The new root node
    @private
    */
  setRoot : function(root)

  /**
    Adds a callback function to be called before drawing each frame.

    @param f Callback function
    */
  addFrameListener : function(f)

  /**
    Removes a callback function from update callbacks.

    @param f Callback function
    */
  removeFrameListener : function(f)

  addEventListener : function(type, listener, capture)

  /**
    Synonym for addEventListener.
  */
  when : function(type, listener, capture)

  removeEventListener : function(type, listener, capture)

  dispatchEvent : function(event)

  broadcastEvent : function(event)

  handleEvent : function(event)

  /**
    Handle scenegraph update.
    Called with current time before drawing each frame.

    This method should be touched only if you know what you're doing.
    If you need your own update handler, either add a frame listener or
    overwrite {@link CanvasNode#update}.

    @param time Current animation time
    @param timeDelta Time since last frame in milliseconds
    */
  handleUpdate : function(time, timeDelta)

  /**
    Update this node. Calls all frame listener callbacks in the order they
    were added.

    Overwrite this with your own method if you want to do things differently.

    @param time Current animation time
    @param timeDelta Time since last frame in milliseconds
    */
  update : function(time, timeDelta)

  /**
    Tests if this node or its subtree is under the mouse cursor and
    sets this.underCursor accordingly.

    If this node (and not one of its childNodes) is under the mouse cursor
    this.root.target is set to this. This way, the topmost (== drawn last)
    node under the mouse cursor is the root target.

    To see whether a subtree node is the current target:

    if (this.underCursor && this.contains(this.root.target)) {
      // we are the target, let's roll
    }

    This method should be touched only if you know what you're doing.
    Overwrite {@link CanvasNode#drawPickingPath} to change the way the node's
    picking path is created.

    Called after handleUpdate, but before handleDraw.

    @param ctx Canvas 2D context
    */
  handlePick : function(ctx)

  /**
    Returns true if the point x,y is inside the path of a drawable node.

    The x,y point is in user-space coordinates, meaning that e.g. the point
    5,5 will always be inside the rectangle [0, 0, 10, 10], regardless of the
    transform on the rectangle.

    Leave isPointInPath to false to avoid unnecessary matrix inversions for
    non-drawables.

    @param x X-coordinate of the point.
    @param y Y-coordinate of the point.
    @return Whether the point is inside the path of this node.
    @type boolean
    */
  isPointInPath : false,

  /**
    Handles transforming and drawing the node and its childNodes
    on each frame.

    Pushes context state, applies state transforms and draws the node.
    Then sorts the node's childNodes by zIndex, smallest first, and
    calls their handleDraws in that order. Finally, pops the context state.

    Called after handleUpdate and handlePick.

    This method should be touched only if you know what you're doing.
    Overwrite {@link CanvasNode#draw} when you need to draw things.

    @param ctx Canvas 2D context
    */
  handleDraw : function(ctx)

  /**
    Transforms the context state according to this node's attributes.

    @param ctx Canvas 2D context
    @param onlyTransform If set to true, only do matrix transforms.
    */
  transform : function(ctx, onlyTransform)

  /**
    Draws the picking path for the node for testing if the mouse cursor
    is inside the node.

    False by default, overwrite if you need special behaviour.

    @param ctx Canvas 2D context
    */
  drawPickingPath : false

  /**
    Draws the node.

    False by default, overwrite to actually draw something.

    @param ctx Canvas 2D context
    */
  draw : false

  /**
    Adds event handlers to this object so that you can drag it around with the mouse.

    Experimental!
    */
  makeDraggable : function()

  /**
    Bounding box internals
    */
  createSubtreePath : function(ctx, skipTransform)
  getSubtreeBoundingBox : function(identity)
  mergeBoundingBoxes : function(bb, bb2)
  getAxisAlignedBoundingBox : function()
```