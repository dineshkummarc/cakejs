CAKE is a [JavaScript](http://en.wikipedia.org/wiki/JavaScript) [scene graph](http://en.wikipedia.org/wiki/Scene_graph) library for the [HTML5](http://en.wikipedia.org/wiki/HTML_5) [canvas tag](http://en.wikipedia.org/wiki/Canvas_(HTML_element)). You could think of it as [SVG](http://en.wikipedia.org/wiki/Scalable_Vector_Graphics) sans the XML and not be too far off.

UPDATE 2.7.12: A new cake (2.0) is on it's way! With new docs, [Closure](https://developers.google.com/closure/compiler/) compatibility, performance tweaks and more, we hope for this to be the most solid release yet.

Released under the [MIT license](http://en.wikipedia.org/wiki/MIT_license).

### 2.0 (Unreleased) Features ###
  * Cacheable containers
  * Lazy scene updates (reduced floating point math)
  * Superior performance, even on mobile
  * Redraw regions
  * Prototype inheritance allowing type coherence and extension

### Features ###
  * Dynamic and extensible JavaScript scene graph
  * Animation timelines and tweening
  * Picking and mouse events
  * Node primitives (ImageNode, Rectangle, Circle, etc..)
  * Works well in complex web layouts

## Examples ##

### Rich graphics ###
  * [Flashy website without Flash](http://glimr.rubyforge.org/cake/redesign.html) - silly and a way too heavy drawing load. It's more of a browser benchmark than something you could realistically use.

### Games ###
  * [Missile Fleet](http://glimr.rubyforge.org/cake/missile_fleet.html) - a game written with CAKE
  * [Web Mega Pong](http://jeko.free.fr/megapong) - another game written with CAKE
  * [Mahjong Solitaire: Valentine's](http://www.amazon.com/Toy-Studio-Mahjong-Solitaire-Valentines/dp/B006WP5YK8) - an Android game by Toy Studio with a delicious CAKE core
  * [Word Off!](http://www.wordoff.com/) - An [Android](https://play.google.com/store/apps/details?id=com.toystudio.wordoff), [iPhone](http://itunes.apple.com/us/app/word-off/id489202036), & [Web](http://www.wordoff.com/game) HTML 5 Game built on Cake

### File formats ###
  * [CanvasMage](http://code.google.com/p/cakejs/source/browse/trunk/examples/canvasmage.js) - a simple vector image format written in JavaScript

## Documentation ##
Documentation is on it's way! The next draft of cake will support JSDocs completely. We'll hopefully have the entire public API uploaded soon.

### Tutorials ###
  * [Getting started with CAKE](http://www.codeproject.com/KB/scripting/GettingStartedWithCAKE.aspx)

### API reference ###
See [here](http://glimr.rubyforge.org/cake/jsdoc/) for JSDoc generated documentation. It's got the toplevel objects, but doesn't have the method documentation from the source code. The cake.js file has JavaDoc-style documentation, but JSDoc doesn't parse it quite right. Suggestions and help most [welcome](http://code.google.com/p/cakejs/issues/list)!

## Download ##

  * [cake.js](http://cakejs.googlecode.com/svn/trunk/src/cake.js) fresh off the SVN trunk
  * CAKE does not have a fancy tar-ball, so use SVN to download it. Let's keep the trunk bug-free, shall we?

## Contact ##

Use the [issue tracker](http://code.google.com/p/cakejs/issues/list) to report bugs and file feature requests.

## Usage tips ##

  * Use a JavaScript minifier ([YUI compressor](http://developer.yahoo.com/yui/compressor/) is excellent.)
  * Enable compression on your web server.
  * If you don't minify CAKE, it'll be 200 kB in size. Minified it's 100 kB and further gzip-compresses to 28 kB.
  * See MinimizingDownloadSize for more details.