# Introduction #

AudioNode is a CanvasNode used to play a sound.

AudioNode tries to use the HTML 5 audio tag to play sound, but that's not too good an idea, as it doesn't support panning and MP3 playback. Better disable that or figure something out. For the time being, add this line to your script: `CanvasSupport.getSupportsAudioTag = function(){return false};`

If you don't have audio tag support, AudioNode uses Flash with [SoundManager2](http://www.schillmania.com/projects/soundmanager2/) to play the sounds, so you need to include SoundManager2 on your page.


# Object API #

AudioNode derives from CanvasNode.

## Properties ##
```
  ready : false
```
> Is the sound ready to play.

```
  autoPlay : false
```
> Start playing when ready to play if true.

```
  playing : false
```
> Is the sound playing.

```
  paused : false
```
> Is the sound paused.

```
  pan : 0
```
> Stereo pan for the sound [-1..1], use setPan to set.

```
  volume : 1
```
> Volume for the sound [0.0..1.0], use setVolume to set.

```
  loop : false
```
> Whether to loop sound.

```
  transformSound : false
```
> If transformSound is true, the AudioNode pans its sound according to its horizontal position on the canvas.

## Methods ##

```
  initialize : function(filename, params)
```

```
  loadSound : function()
```

```
  play : function()
```

```
  stop : function()
```

```
  pause : function()
```

```
  setVolume : function(v)
```

```
  setPan : function(p)
```

```
  handleUpdate : function()
```