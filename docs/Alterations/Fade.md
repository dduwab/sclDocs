# Fade
The Fade alteration will cause the sprite to incrementally change its transparency.

This effects the alpha value of the sprite. Therefore, to fade, you must specify a negative value for the rate and to unfade, use a positive value. 

```
create sprite from star.png as Star
  where x=250 y=250 alpha=0
  having alt=FadeIn
end
create fade as FadeIn
  where rate=1 until=1 completion=FadeOut
end
create fade as FadeOut
  where rate=-1 until=0 completion=FadeIn
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
  - **rate**={number} a fade rate per second. Use a negative value to fade (increase transparency) and a positive value to make the sprite more opaque.
  - **until**={number} the value at which the fade should stop. Also, the final alpha value for the sprite. Must be a value between 0.0 and 1.0. Be sure this number makes sense with respect to the initial alpha of the sprite and the rate being negative or positive.
  - **completion**={routine|alteration} specify a routine or alteration to run when the fade is complete.
