# Pursuits
The Pursuit alteration will cause a sprite to follow another sprite. If no speed is given then the pursuing sprite will not move but only point at the sprite that it is following. This is a key alteration for action games.

> [!NOTE]
> Try out code samples at https://canvaslanguage.com/studio/github-examples.
> Paste the code samples into the box under that "Advanced" tab,
> then push the "Rec" button to view the animation.

```
create sprite from arrow.png as Arrow 
  where x=250 y=250 center=50,26 angle=90 size=0.25 
  having alt=MyPursuit 
end 
create pursuit as MyPursuit 
  where prey=Star speed=230 follow=300 
end 
create sprite from star.png as Star 
  where x=150 y=30 center=25,25 
  having alt=Move 
end 
create translation as Move 
  where x=random(0,300) y=random(0,300) speed=100 completion=DoneMove 
end 
create routine as DoneMove 
  insert into Star where alt=Move 
end 
create routine as Start
  launch Star 
  launch Arrow 
end 
```

## Properties
- **where**
  - **follow**={number} speed of rotation toward prey in degrees per second
  - **prey**={sprite} the name of the sprite to follow
  - **speed**={number} speed of pursuit in pixels per seconds. If unspecified, the pursuit sprite will only rotate to point at the target sprite.

