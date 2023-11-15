# Flipbooks
The Flipbook alteration will change the image of your sprite repeatedly to create a simple flipbook animation. 

> [!NOTE]
> Try out code samples at https://canvaslanguage.com/studio/github-examples.
> Paste the code samples into the box under that "Advanced" tab,
> then push the "Rec" button to view the animation.

```
create sprite from star.png as Flippable
  where x=250 y=250
  having alt=MyFlipbook
end
create flipbook as MyFlipbook
  where loop=true images=(star.png,heart.png,square.png,triangle.png)
    times=(100,500,50,200)
end 
create routine as Start
  launch Flippable
end
```

## Properties
- **where**
  - **completion**={routine} specify a routine to run when the last frame is complete (non-looping)
  - **frames**=({number},{number},...}) a list of frame numbers in the order in which the frames should display. The first frame is number 1. You can also use *random* (no quotes) as a value to randomize frames.
  - **images**=({string},{string},...}) list of images to be shown for each frame. Image names must be quotes, with no spaces around the commas.
  - **keeplast**={true|false} specify if the sprite should keep the last frame as its image after the flipbook is done running
  - **loop**={true|false} specify if the flipbook should repeat continuously
  - **times**=({number},{number},...}) specify how long each frame should be displayed. The default is 50ms per frame.
