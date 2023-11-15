# Rotation
A Rotation is an alteration that will rotate a sprite around its center point. It has a number of interesting options in order to get your sprite angled how you want it. 

When applying a rotation to a child sprite, the angles are relative to the sprite's direct parent sprite, not the screen. 

> [!NOTE]
> Try out code samples at https://canvaslanguage.com/studio/github-examples.
> Paste the code samples into the box under that "Advanced" tab,
> then push the "Rec" button to view the animation.

```
create sprite from square.png as Spinner
  where center=auto x=250 y=250 
  having alt=Rot1
end 
create rotation as Rot1 
  where speed=-360 distance=90 easein=20 easeout=20 completion=Rot1
end
create routine as Start
  launch Spinner
end
```

## Properties
- **where**
  - **destination**={number} rotate until this angle is reached
  - **distance**={number} the distance to rotate - positive values only - speed sets direction. OR,use distance=short to travel the shortest distance to the given destination. In this case, the sign of speed is ignored.
  - **easein**={number} gradually increase speed over this distance (in degrees).
  - **easeout**={number} before reaching distance, gradually decrease speed over this distance (in degrees).
  - **completion**={routine|alteration} specify a routine or another alteration to run when the rotation stops
  - **speed**={number} speed of rotation in degrees per second. This can be a negative value to rotate clockwise.
  - **toward**={number},{number} rotate until pointing at this x,y coordinate
