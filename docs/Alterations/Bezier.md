# Bezier Curves

Make your sprite travel along a bezier curve. This is a bit complicated because you must import a path from a graphic program. See below.

```
var STAR="arrow-black.png"
var SQUARE="square.png"
var TRIANGLE="triangle.png"
var HEART="arrow-black.png"

create sprite from HEART as Heart
  where center=auto x=250 y=100 angle=270
  having alt=MyBezierTraversal
end
create bezier as MyBezierTraversal
  where start=234,95
    orientation="normal" // none|tangent|normal
    time=6000
    laps=2
    path="138.00,112.00 82.00,135.00 130.00,246.00 196.00,329.00 92.00,488.00 273.00,369.00 345.00,317.00 463.00,317.00 357.00,224.00 301.00,168.00 478.00,52.00 234.00,95.00"
end

create routine as Start
  launch Heart
end
```
The Bezier alteration will move your sprite along a curve you specify with a path.
Curves are implemented via cubic bezier curves(View on Wikipedia), that is, a start point, an end point, and 2 guide points between them.

Curve coordinates are mapped relative to the sprite's location when the alteration is applied
start is a point separate from the main coordinate list (path.) start acts are a guidepost. It has nothing to do with where your sprite is or will be. Let me explain: If you use a drawing program to design a path, you'll draw the curve on the canvas of the drawing program. But you don't know how your sprite will map to that canvas. So the start point lets you tell SCL™ that when designing the curve you started at that point so SCL™ can map all the later coordinates relative to that point, then apply those points to where the sprite actually is.
Each coordinate is mapped by subtracting the start point position from its value. This gives a relative position to the current position of the sprite (trust me, its magical)
A simple way to design your curves is in GIMP (gimp.org). Use the curve drawing tool then export the curve as a text file and edit the curve description.
Since coordinates are relatively mapped, when designing your curve you don't need to guess where your sprite might be.
You can specify orientation as being none, normal or tangent. This describes the angle that the sprite will hold as it follows the curve
If you need the sprite to loop the curve infinitely, then set a high value for laps such as 9999999.

## Properties
completion={name}
the name of a routine to run with the sprite is finished following all the laps of the curve.
laps={number}
how many times sprite should follow the path. For unlimited, use a high number like 99999999
orientation={none|normal|tangent}
indicates how to angle the sprite on the path
path={"x,y "...}
a series of points separated by spaces. The first two points are guides leading from start. Do not put a linefeed inside the path value.
start={number,number}
x,y position from which to compare path coordinates. See the notes above
time={number}
a rough guide to how long it should take the sprite to traverse the path
