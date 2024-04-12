**Functions**

A number of functions are supported as specified below.

***random(a,b)***

returns a random integer in the range of * *a* * through * *b-1* *
```
var r=random(4,8) // returns a random value between 4-7 inclusive
```

***arcdistance(x1,y1,x2,y2)***

returns the smallest number of degrees between 2 points

***canvaswidth()***

returns the width of the canvas

***canvasheight()***

returns the height of the canvas

***covered(spriteName)***

Detemines if a sprite is covered, in the display area, by another sprite. It accounts of the scaling of sprites, 
but not orientation, or children/parent relationships, or transparency. Okay, this is pretty limited, bordering on 
useless. This may need to be updated in the future.

returns true or false

***distance(x1,y1,x2,y2)***

returns the pixel distance between 2 points

***getcolor(target,x,y)***

Where:
- **target** is either:
  - a sprite name
  - **_all** or **_canvas**
- **x** coordinate on the canvas or sprite
- **y** coordinate on the canvas or sprite

returns the color of the given location as an integer

***getglobalx(spriteName)***

returns the x coordinate of the given sprites center on the canvas, accounting for parent/child relations, scaling, and orientation

***getglobaly(spriteName)***

returns the y coordinate of the given sprites center on the canvas, accounting for parent/child relations, scaling, and orientation

***getpolard(x1,y1,x2,y2)***

returns the number of degrees between point 1 and point 2

***getpolarx(x,angle,distance)***

Where:
- **x** is the x-coordinate to start from.
- **angle** the angle to travel from the given x-coordinate
- **distance** the distance to travel from the x-coordinate

returns a new x-coordinate travel the angle and distance given

***getpolary(y,angle,distance)***

Where:
- **y** is the y-coordinate to start from.
- **angle** the angle to travel from the given y-coordinate
- **distance** the distance to travel from the y-coordinate

returns a new y-coordinate travel the angle and distance given

***getsavedata(key)***

returns the requested value from browser local storage

***iskeydown(key)***

returns true if the given key is currently pressed, else returns false

***islive(spriteName)***

returns true if the given sprite is currently in the canvas rendering tree, else returns false

***jsvar(varName)***

returns the value of the given JavaScript variable

***Math.floor(value)***

returns the floor of the given value (ie: chop off decimals without rounding)

***Math.max(value1,value2,...)***

returns the highest value of any number of given parameters

***Math.abs(value)***

returns the absolute value of the given parameter

***Math.min(value1,value2,...)***

returns the lowest value of any number of given parameters

***Math.ceil(value)***

returns the ceiling of the given value (ie: always rounds up to the nearest integer)

***Math.cos(value)***

returns the cosine of the given value

***Math.sin(value)***

returns the sine of the given value

***Math.tan(value)***

returns the tangent of the given value

***savedata(key,value)***

saves the given key/value pair to browser local storage

***timems()***

returns the number of milliseconds since the animation began running


