# Slides
The Slide alteration will cause the sprite to move in the direction given for the given distance. Remember that the directions used in SCL are based on the unit circle where 0 degrees is to the right.

```
create sprite from heart.png as Heart
  where x=50 y=250 center=auto
  having alt=Slider 
end 
create slide as Slider 
  where speed=500 direction=20 easein=100 easeout=100 distance=400 
end
create routine as Start
  launch Heart 
end 
```
> [!NOTE]
> Try out code samples at https://canvaslanguage.com/studio/github-examples.
> Paste the code samples into the box under that "Advanced" tab,
> then push the "Rec" button to view the animation.

## Properties
- **where**
 - **completion**={routines|alteration} a routine or alteration to run when the slide is complete.
 - **direction**={number} the direction to travel without regard to the sprite’s current angle.
 - **distance**={number} how many pixels to travel (optional).
 - **easein**={number} gradually increase speed over this distance.
 - **easeout**={number} before reaching distance, gradually decrease speed over this distance.
 - **speed**={number} move in pixels per second.
