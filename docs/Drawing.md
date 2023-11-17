# Drawing
You can use basic drawing calls directly in SCL. You can draw onto sprites, onto the bottom of the canvas, or on top of the canvas overtop of all sprites. 

You draw inside a routine. For example: 

```
create sprite from triangle.png as Triangle
  where center=auto x=100 y=100
  having alt=(sub
    create rotation end)
end
create routine as Start
  draw onto _bottom
    fillstyle "rgba(255,0,255,0.65)"
    fillrect 230,140,40,40
    font "italic bold 48px sans-serif"
    fillstyle "green"
    filltext "Hello",10,10,100
  enddraw
  launch Triangle
  draw onto Triangle
    strokestyle "red"
    moveto 0,0
    lineto 100,100
    stroke
  enddraw
end
```

> [!NOTE]
> Try out code samples at https://canvaslanguage.com/studio/github-examples.
> Paste the code samples into the box under that "Advanced" tab,
> then push the "Rec" button to view the animation.

Draw commands are all small-case, followed by a space, then parameters separated by commas. Strings for text or CSS styles must be double-quoted. The above example demonstrates this.

**Warning**: expressions (like math) are have only experimentally supported in draw commands because of performance considerations.

Drawing onto **_bottom** will draw on the canvas before any sprites are drawn.

Drawing onto **_top** will draw on top of everything after everything else is drawn.

Drawing onto a sprite (specified with its name) will draw onto the sprite with all the sprites alterations applied to the drawing. That means, by drawing on sprites, you create mini-canvases for drawing. When drawing on sprites, the coordinate system is based on the image of the sprite, and not the center. In the example above, starting the draw at 0,0 isn't in the center of the sprite, it is actually the corner of the source image.

Drawing is sticky. Once you draw on a sprite or onto _bottom or _top, that drawing stays until it is cleared with "clear".

**You are strongly advised to read the W3 2D Context drawing specification for how some of these command work.**

## Supported calls are: 
- **arc** 
- **arcto** extends the current path as an arc
- **beziercurveto** draws a curve using the bezier method
- **beginpath**
- **circle** creates a circle at x,y with radius: circle 100,230,50
- **clear** clears the instruction list (see below)
- **clearrect** clears a rectangle of the given size
- **clip** creates a clipping region based on current path
- **closepath**
- **composition**
- **fill** fills the current path with the current fillstyle
- **fillrect** fills a rectangle with the current fillstyle
- **fillstyle** sets a fill color which is used to fill an area created by paths
- **filltext** draws given text using the current fillstyle
- **floodfill**
- **font** defines font to use. See docs reference below for settings. ex ("italic 400 12px/2 Unknown Font, sans-serif"). That format is "[style] [variant] [weight] [size/line height] [font]"
- **image** draws an image at the specified x/y: image dog.png,0,0
- **lineto** draws a line from the current position to the given coordinate
- **linewidth** set the line width for strokes made after
- **moveto** moves your current drawing tip to the given coordinate
- **quadraticcurveto** draws a curve using the quadratic method
- **rect** creates a rectangular subpath
- **shadowblur** set shadow under text blur value (1 is slight blur, 20 is very blurry, 20+ is possible
- **shadowcolor** set shadow color 
- **shadowoffsetx** set shadow under text x-offset
- **shadowoffsety** set shadow under text y-offset
- **stroke** outlines the current path with the current strokestyle
- **strokerect** draws a rectangle outline with the current stroke style
- **strokestyle** sets a stroke color which is applied to lines draw with paths or text
- **stroketext** draws the given text using the current strokestyle
- **textalign** set to "center", "left", or "right"
- **textbaseline** set to "top","middle","hanging","alphabetic","ideographic","bottom"


Read the W3 drawing specification for details but be aware of some basics with SCL: 
- All the names of draw commands are completely small case
- After the command name, leave a space, then a list of parameters separated by commas. Do not use an equal sign or paranthesis.
- Using moveto and lineto doesn't draw anything unless you follow the list of commands with "stroke" or "fill".
- Once you draw something, it stays until you call "clear". That clears all the drawn items from the target (the target being “_top”, “_bottom” or a sprite name)
- Multiple lines can be separated with \n In this case, vertical spacing of lines will be based on the most recent call to 'font' where a px value was specified.

