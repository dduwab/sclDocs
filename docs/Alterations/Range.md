# Range
The Range alteration triggers events based on one sprite's proximity to another. Proximity can be set by both distance and by a region in front of the tracking sprite as identified by an angle. 

**IMPORTANT:** The target sprite must be on screen before this alteration is created! 

```
create sprite from arrow.png as TrackingArrow 
  where x=150 y=350 center=auto angle=45
  having alt=TrackRange
end 
create sprite from arrow.png as Arrow 
  where x=100 y=100 center=auto angle=305
  having alt=MoveArrow 
end 
create routine as Start 
  launch Arrow 
  launch TrackingArrow 
end 
create range as TrackRange 
  where target=Arrow distance=200 enter=Near exit=Leave arc=90 
end 
create routine as Near 
  update sprite TrackingArrow where alpha=0.5 
end 
create routine as Leave 
  update sprite TrackingArrow where alpha=1.0 
end 
create vector as MoveArrow 
  where speed=120 
end 
```

> [!NOTE]
> Try out code samples at https://canvaslanguage.com/studio/github-examples.
> Paste the code samples into the box under that "Advanced" tab,
> then push the "Rec" button to view the animation.

## Properties
 - **arc**={number} You can set an arc "in front" of your sprite such that the target sprite must be within that arc for events to fire. Imagine a cone extending from the front of your sprite. The arc sets this cone. The front is considered to be the angle at which the sprite is pointing. For example, if your sprite is currently at 45 degrees and the arc=20, then the target must be between 35 and 55 degrees for your sprite in order to register a range event.
 - **distance**={number} the number of pixels distance from the center points of the sprites to be considered in range.
 - **enter**={routine} specify a routine to run when the target sprite enters range. This can fire multiple times if no completion event is set
 - **exit**={routine} specify a routine to run when the target sprite leaves range. This can fire multiple times if no completion event is set
 - **target**={sprite} the name of the sprite to watch
 - **completion**={routine} specify a routine to run when the target sprite enters range. If this is set then this alteration will close upon completion. This means that no exit event will fire and no more enter events will fire if the target sprite leaves then re-enters the range.

