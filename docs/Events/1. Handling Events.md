# Events

Events are signals that occur when something happens in the animation or the to the canvas. For example, two sprite might collide triggering an event, or a user might tap the screen. There are many many events supported by SCL.

**Completion** events occur when an alteration is finishes running. Two things can happen with a completion event: a new alteration can be applied to the sprite, or a routine can be triggered.

**Events Handlers** are routines that are trigged by a broad set of occurances. Completion events, mouse events, animation events, and more can trigger event handlers. When an event handler is run, the sprite that initiated the event is available to be referenced with the **_sprite** identifier.

**User Events** are event triggerd by user action. These can be captured as mouse events, touch events, and even a special SCL object called a **joystick**. Read more about joysticks later.

**Animation Events** are events triggered by the animation process, for example upon entering the animation frame or exiting the frame.

Many events can be set on individual sprites or on the canvas as a whole:
 - **Canvas events** are set in routines using a **set** command.
 - **Sprite events** are set in the **where** clause. For details about **sprite events**, see the **sprite** documentation.

> [!NOTE]
> Try out code samples at https://canvaslanguage.com/studio/github-examples.
> Paste the code samples into the box under that "Advanced" tab,
> then push the "Rec" button to view the animation.

Click either the sprite or the canvas. **NOTE:** Clicking a sprite will still trigger a canvas click event.
```
create sprite from square.png as S1
  where x=250 y=50 center=auto click=MySpriteClickEvent
end
create routine as Start
  launch S1
  set click=MyCanvasClickEvent
end
create routine as MySpriteClickEvent
  log("MySpriteClickEvent")
  insert into _sprite where alt=(sub create vector where speed=200 distance=100 end)
end
create routine as MyCanvasClickEvent
  log("MyCanvasClickEvent")
  insert into S1 where alt=(sub create rotation where distance=-30 end)
end
```
