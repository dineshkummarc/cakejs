# Introduction #

> ElementNode is a CanvasNode that has an HTML element as its content.

> The content is added to an absolutely positioned HTML element, which is added to the root node's canvases parentNode. The content element follows the current transformation matrix.

> The opacity of the element is set to the globalAlpha of the drawing context unless #noAlpha is true.

> The font-size of the element is set to the current y-scale unless #noScaling is true. If the browser supports CSS transforms, the HTML content tracks the transformation matrix of the ElementNode and doesn't need to change font-size.

> Use ElementNode when you need accessible web content in your animations.
```
    var e = new ElementNode(
      E('h1', 'HERZLICH WILLKOMMEN IM BAHNHOF'),
      {
        x : 40,
        y : 30
      }
    )
    e.addFrameListener(function(t) {
      this.scale = 1 + 0.5*Math.cos(t/1000)
    })
```

# Object API #

ElementNode derives from CanvasNode.

## Constructor ##
```
  ElementNode(content, config)
```
> Where `content` is an HTML element or string of HTML to use as the content, and `config` is an optional config object merged with the created ElementNode.

## Properties ##

```
  noScaling : false
```
> If noScaling is true, the HTML content only tracks the position of the ElementNode and not its scale and rotation.

```
  noAlpha : false
```
> If noAlpha is true, the HTML content opacity is always 1, i.e. fully opaque.

```
  align: null
```
> HTML content horizontal alignment with respect to the ElementNode position.

> The accepted values are null, 'left', 'center', 'middle' and 'right'. Null and 'top' align the HTML content so that its left edge goes through the ElementNode's position. The 'center' and 'middle' values align the horizontal center of the HTML content with the ElementNode's position, whereas 'right' aligns the right edge with the ElementNode's position.

```
  valign: null
```
> HTML content vertical alignment with respect to the ElementNode position.

> The accepted values are null, 'top', 'center', 'middle' and 'bottom'. Null and 'top' align the HTML content so that its top edge goes through the ElementNode's position. The 'center' and 'middle' values align the vertical center of the HTML content with the ElementNode's position, whereas 'bottom' aligns the bottom edge with the ElementNode's position.

```
  xOffset: 0
```
> HTML content horizontal offset.

```
  yOffset: 0
```
> HTML content vertical offset.

## Methods ##

```
  initialize : function(content, config)
```
> ElementNode initializer takes the content element and config object. It calls the CanvasNode initializer with the config object.

```
  clone : function()
```
> Clones the ElementNode, including the content element.

```
  setRoot : function(root)
```
> Differs from CanvasNode.setRoot by moving the content element as well.

```
  handleUpdate : function(t, dt)
```
> Also updates the content element visibility.

```
  addEventListener : function(event, callback, capture)
```
> Adds event listener to the content element.

```
  removeEventListener : function(event, callback, capture)
```
> Removes event listener from the content element.

```
  draw : function(ctx)
```
> Updates the content element transform and style.