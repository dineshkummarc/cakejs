# Introduction #

This document will outline some of the issues you may have when converting to the new cake. Many of the new performance enhancements are based around reducing function calls, floating point math, recursion, and canvas state changes. Many of these changes limit some of the convenient nature of the scene graph, but with a few fixes you should be good to go in no time.

# Major changes #

More aggressive **changed** flag.
  * The matrix transform on nodes will only be updated when the changed flag is set. In some modes this is also required to render a new frame and/or create redraw regions.