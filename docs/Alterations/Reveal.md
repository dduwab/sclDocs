# Reveal
The Reveal alteration hides or shows the images as if appearing from behind an invisible wall. 

> [!NOTE]
> Try out code samples at https://canvaslanguage.com/studio/github-examples.
> Paste the code samples into the box under that "Advanced" tab,
> then push the "Rec" button to view the animation.

```
create sprite from star.png as StarShow 
  where center=25,25 x=150 y=50 
  having alt=Show 
end 
create sprite from heart.png as HeartHide 
  where center=25,25 x=150 y=150 
  having alt=Hide 
end 
create reveal as Show 
  where direction="left" speed=20 type="show" 
end 
create reveal as Hide 
  where direction="right" speed=20 type="hide" 
end 
create routine as Start
  launch StarShow
  launch HeartHide 
end 
```

## Properties
- **where**
  - **type**="{show|hide}" should the sprite enter or leave the view with this alteration.
   - **direction**="{top|bottom|right|left}" from which direction to enter or leave.
   - **speed**={number} the speed with which to move the sprite
   - **completion**={routine name} the name of a routine to run with the operation is complete.


