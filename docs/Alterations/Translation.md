# Translation
A Translation is an alteration that will move a sprite from its current location to a new location in a sliding motion. 

```
create sprite from star.png as Star
  where x=80 y=100
  having alt=Translate
end 
create translation as Translate 
  where x=420 y=390 speed=200 completion=Start 
end
create routine as Start 
  launch Star 
end 
```
> [!NOTE]
> Try out code samples at https://canvaslanguage.com/studio/github-examples.
> Paste the code samples into the box under that "Advanced" tab,
> then push the "Rec" button to view the animation.


## Properties
- **where**
 - **completion**={routine|alteration} specify a routine or alteration to run when the sprite reaches its destination
 - **easein**={number} distance to use to accelerate up to speed
 - **easeout**={number} distance to use to slow down to 0
 - **speed**={number} speed of movement in pixels per second
 - **x**={number} horizontal destination of the translation [optional]
 - **y**={number} vertical destination of the translation [optional]
