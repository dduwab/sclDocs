# Canvas Events
Canvas events are events that happen to or on the canvas. They could also be considered as events that occur at the level of the whole animation. Canvas Events are set using a **set** command followed by the name of the event, and then the routine to run when the event occurs. Ex: ```set exitframe=OnMyExit```

And of course, the routine must be defined somewhere in your SCL script.

Here are a list **Canvas Events** supported by SCL.
- set **enterframe** will call a routine before any processing is initiated for the frame and before anything is drawn.
- set **exitframe** will call a routine after all the animation process is completed for a frame.
- set **mousedown** will call a routine when a mouse button is pushed down on the canvas.
- set **mouseup** will call a routine when a mouse button is released over the canvas.
- set **mousemove** will call a routine when the mouse is moved over the canvas.
- set **click** will call a routine when a mouse button is clicked over the canvas.
- set **keypress** will call a routine when a key is pressed and released on the keyboard.
- set **keydown** will call a routine when a key is pressed down on the keyboard.
- set **keyup** will call a routine when a key is pressed up on the keyboard.
- set **touchstart** will call a routine when the canvas is touched - usual a mobile device.
- set **touchend** will call a routine when a canvas touch is ended - usual a mobile device.
- set **touchmove** will call a routine when a canvas touch moved across the canvas - usual a mobile device.
- set **swipeup** will call a routine when the canvas is swiped upwards.
- set **swiperight** will call a routine when the canvas is swiped rightwards.
- set **swipedown** will call a routine when the canvas is swiped downwards.
- set **swipeleft** will call a routine when the canvas is swiped leftwards.
- set **pinch** will call a routine when the canvas is pinched with 2 finger touch events.
- set **pivot** will call a routine when the canvas is rotated with 2 finger touch events.

Please enjoy some more details below.

## Animation Events
The 2 canvas animations events, **enterframe** and **exitframe**, are useful when routines do calculations may affect what is drawn at the very end of an animation or the very beginning. For example, a collision between sprites may change a value that is then used in **exitframe** to draw a score on the canvas.

## Mouse Events
There are 4 mouse events. **click** is the simplest, if the mouse button is pressed the event fires regardless of whether the button is released. The other mouse events works as described above.

All mouse events fill a variable called **mouse**. **mouse** is not preceeed by an underscore but may be in the future, therefore **_mouse** is reserved by unused. So don't use **_mouse**, just use **mouse**.

- **mouse.x** identifies the x coordinate of the mouse click.
- **mouse.y** identifies the y coordinate of the mouse click.

### Mouse Move Event Values
In the event handler for **mousemove**, the **mouse** variable has additional values:

- **mouse.x1** identifies the x coordinate of the previous mouse click.
- **mouse.y1** identifies the y coordinate of the previous mouse click.
- **mouse.x2** identifies the x coordinate of the current mouse click (identical to mouse.x).
- **mouse.y2** identifies the y coordinate of the current mouse click (identical to mouse.y).
- **mouse.angle** identifies the angle between previous click and the current click.
- **mouse.distance** identifies the distance between the previous click and the current click.
- **mouse.distancex** identifies the horizontal distance between the previous click and the current click.
- **mouse.distancey** identifies the vertical distance between the previous click and the current click.

```
create routine as Start
  set mousemove=OnMMove
end
create routine as OnMMove
  draw onto _top
    clear
    font "normal 100 16px monospace"
    filltext "x,y="+mouse.x+","+mouse.y,10,10,500
    filltext "x2,y2="+mouse.x2+","+mouse.y2,10,30,500
    filltext "x1,y1="+mouse.x1+","+mouse.y1,10,50,500
    filltext "angle="+mouse.angle,10,70,500
    filltext "distance="+mouse.distance,10,90,500
    filltext "distancex="+mouse.distancex,10,110,500
    filltext "distancey="+mouse.distancey,10,130,500
  enddraw
end
```
> [!NOTE]
> Try out code samples at https://canvaslanguage.com/studio/github-examples.
> Paste the code samples into the box under that "Advanced" tab,
> then push the "Rec" button to view the animation.



