cake.js is 200kB without minification and compression, which is, frankly, huge.

To bring the file size (and page load times) down, you should at least minify cake.js and preferably gzip it too.

Here are the file sizes (circa 2008-03-21):
```
cake.js        212 kB  -- plain source
cake_min.js    106 kB  -- minified
cake_min.js.gz  28 kB  -- minified and gzipped
```

Download times on a 384kbps 3G connection:
  * cake.js: around 5 seconds
  * cake\_min.js: around 2.5 seconds
  * cake\_min.js.gz: around 0.6 seconds

If you also strip out the SVGParser at the end of cake.js, the minified CAKE will be 86 kB in size, and 23 kB gzipped.

To minify, download [YUI compressor](http://developer.yahoo.com/yui/compressor/) and do the following:
```
java -jar yuicompressor-*.jar cake.js -o cake_min.js
```

To GZIP, set up your mod\_deflate equivalent (instructions for [Apache 2](http://httpd.apache.org/docs/2.0/mod/mod_deflate.html) and [Nginx](http://wiki.nginx.org/NginxHttpGzipModule))