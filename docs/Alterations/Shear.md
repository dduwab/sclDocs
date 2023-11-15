# Shear
Shearing is best understood by example. 

> [!NOTE]
> Try out code samples at https://canvaslanguage.com/studio/github-examples.
> Paste the code samples into the box under that "Advanced" tab,
> then push the "Rec" button to view the animation.

```
create sprite from star.png as Star 
  where x=250 y=250 center=auto
  having alt=Shear1
end 
create shear as Shear1
  where rate=3 until=1 type=x completion=Shear2
end 
create shear as Shear2
  where rate=-3 until=0 type=x completion=Shear1
end 

create routine as Start 
  launch Star 
end 
```

## Properties
- **where**
  - **completion**={routine|alteration} specify a routine or alteration to run when the shearing is complete.
  - **rate**={number} a shear rate per second. Use a negative value as appropriate.
  - **type**={x|y} specify in which direction to shear the sprite. If type is not specified the shearing is performed both ways.
  - **until**={number} the value at which the shearing should end. Be sure this number makes sense with respect to the initial size of the sprite and the rate being negative or positive.

> [!WARNING]
> FireFox cannot always correctly run a shearing effect.
> This bug in FireFox has been submitted to Bugzilla (661452)
> See the tutorial for more details.
