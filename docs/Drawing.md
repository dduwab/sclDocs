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
    strokestyle black
    circle 250,160,20
    stroke
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
- **arc** draws an arc using current line settings
  - ```arc x,y,radius,startAngle,endAngle,counterClockwise{false|true}```
- **arcto** extends the current path as an arc
  - ```arcto x1,y1,x2,y2,radius```
- **beziercurveto** extends the current path following this bezier curve
  - ```beziercurveto controlPt1X,controlPt1Y,controlPt2X,controlPt2Y,endPointX,endPointY```
- **beginpath** lifts the pen, and restarts the drawing path
   - ```beingpath```
- **circle** creates a circle at x,y with radius: circle 100,230,50
   - ```circle x,y,radius```
- **clear** clear all the drawing from the surface but only for _top and _bottom. If drawing onto a sprite then you must use **clearrect** instead
   - ```clear```
- **clearrect** clears a rectangle of the given size
   - ```clearrect x,y,w,h```
- **clip** creates a clipping region based on current path. Any drawing that occurs outside the clipped region will not be visible
   - ```clip```
- **closepath** closes the current drawing path. ie: it ends now so you can start a new path with beginpath
   - ```closepath```
- **composition** sets a layer composition on the subsequent draws. Valid values are here https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/globalCompositeOperation
   - ```composition xor```
- **fill** fills the current path with the current fillstyle
   - ```fill```
- **fillrect** fills a rectangle with the current fillstyle
   - ```fill x,y,w,h```
- **fillstyle** sets a fill color which is used to fill an area created by paths
   - ```fillstyle {string}```
   - ```fillstyle red```
   - ```fillstyle "rgba(124,255,17,0.5")```
- **filltext** draws given text using the current fillstyle
   - ```filltext "my text",x,y,maxWidth```
- **floodfill** fills an enclosed space with the given rgba color
   - ```floodfill x,y,r,g,b,a```
- **font** specifies font properties to use when drawing text. See docs reference below for settings. ex ("italic 400 12px/2 Unknown Font, sans-serif"). That format is "[style] [weight] [size/line height] [font]"
   - ```font "italic 500 24px sans-serif"```
- **image** draws an image at the specified x/y: image dog.png,0,0
   - ```image {file name},x,y```
- **lineto** draws a line from the current path position to the given coordinate
   - ```lineto x,y```
- **linewidth** set the line width for new strokes
   - ```linewidth {number}```
- **moveto** moves your current drawing tip to the given coordinate
   - ```moveto x,y```
- **quadraticcurveto** extends the current path using the quadratic curve method
   - ```quadraticcurveto controlPointX,controlPointY,endPointX,endPointY```
- **rect** creates a rectangular subpath to the current path
   - ```rect x,y,w,h```
- **shadowblur** sets the amount of blur to shadows drawn under text (1 is slight blur, 20 is very blurry, 20+ is possible
   - ```shadowblur {number}```
- **shadowcolor** set text shadow color
   - ```shadowcolor "{css color value}"```
   - ```shadowcolor "green"```
- **shadowoffsetx** set text shadow x-offset
   - ```shadowoffsetx {number}```
- **shadowoffsety** set text shadow y-offset
   - ```shadowoffsety {number}```
- **stroke** outlines the current path with the current strokestyle
   - ```stroke```
- **strokerect** draws a rectangle outline with the current stroke style. This does not effect the current path.
   - ```strokerect x,y,w,h```
- **strokestyle** sets a stroke color which is applied to lines draw with paths or text
   - ```strokestyle "{css color value}"```
   - ```strokestyle "#ffff00"```
- **stroketext** draws the given text using the current strokestyle
   - ```stroketext "my text",x,y,maxWidth```
- **textalign** set to a value of "center", "left", or "right"
   - ```textalign {value}```
- **textbaseline** set to a value of "top","middle","hanging","alphabetic","ideographic","bottom"
   - ```textbaseline {value}```

## Read the W3 drawing specification for details but be aware of some basics with SCL: 
- All the names of draw commands are completely small case
- After the command name, leave a space, then a list of parameters separated by commas. Do not use an equal sign or paranthesis.
- Using moveto and lineto doesn't draw anything unless you follow the list of commands with "stroke" or "fill".
- Once you draw something, it stays until you call "clear". That clears all the drawn items from the target (the target being “_top”, “_bottom”). For drawing on sprites, you must use **clearrect** instead.
- Multiple lines can be separated with \n In this case, vertical spacing of lines will be based on the most recent call to 'font' where a px value was specified.

