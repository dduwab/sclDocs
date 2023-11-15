# Vector
The vector alteration will move your sprite in the direction of its angle value. 

> [!NOTE]
> Try out code samples at https://canvaslanguage.com/studio/github-examples.
> Paste the code samples into the box under that "Advanced" tab,
> then push the "Rec" button to view the animation.

```
create routine as Start 
  launch Arrow 
end 
create sprite from arrow.png as Arrow 
  where center=103,27 x=100 y=400 angle=80 
  having alt=Move
end 
create vector as Move
  where speed=100 distance=300 completion=Start 
end 
```

## Properties
- **where**
  - **completion**={routine|alteration} a routine or alteration to run when the movement is complete.
  - **distance**={number} how far to move the sprite.
  - **speed**={number} speed of movement in pixels per seconds.
