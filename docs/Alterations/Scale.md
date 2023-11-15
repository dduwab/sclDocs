# Scale
The Scale alteration will cause the sprite to incrementally change size. You can scale on the x or y axis or both.
FireFox may fail to launch completion events if sprite size reaches 0.0. Therefore, also set a minimum size of 0.01 or something smaller if necessary. 

> [!NOTE]
> Try out code samples at https://canvaslanguage.com/studio/github-examples.
> Paste the code samples into the box under that "Advanced" tab,
> then push the "Rec" button to view the animation.

```
create sprite from star.png as Star 
  where x=250 y=250 center=auto
  having alt=ScaleY 
end 
create scale as ScaleY 
  where rate=-1 until=0.1 type=y completion=ScaleX
end
create scale as ScaleX 
  where rate=-0.75 until=0.1 type=x completion=ScaleUp
end
create scale as ScaleUp 
  where rate=1.5 until=1 completion=ScaleY
end
create routine as Start 
  launch Star 
end 
```

## Properties
- **where**
  - **rate**={number} a scale rate per second. Use a negative value to shrink and a positive value to grow the sprite.
  - **type**={x|y} specify in which direction to scale the sprite. If type is not specified the scaling is performed both ways.
  - **until**={number} the value at which the scaling should end. Be sure this number makes sense with respect to the initial size of the sprite and the rate being negative or positive.
  - **completion**={routine} specify a routine to run when the scaling is complete.
