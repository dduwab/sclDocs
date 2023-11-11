## Sprite

Each moving entity is called a sprite. Normally sprites are defined with an image and a name. You can create a sprite without an image then use it as a container for other things. Sprites support many parameters. 
Sprites are moved using alterations. Alterations include rotation, slide and many more. 
The general animation structure of SCL is based on this relationship.

A sprite is put on screen with either the **launch** command or the **clone** command. Launch is the simplest and most direct method to do this and usually starts an animation in the **Start** routine.
After a sprite is on the screen it can be changed in a routine through various methods described later. 

If you want to change a sprite that you just created with a clone command, then refer to the clone by _clone instead of a sprite name. 

If you want to refer to a sprite that signalled an event (such as click or completion event), then use _sprite to refer to the current sprite. 

```
create routine as Start
  launch Dog
  launch windfarm
end
create sprite from dog.png as Dog
  where center=auto x=50 y=50
end
create sprite from windmill.png as windmill into windfarm 
  where x=100 y=200 alpha=0.5 angle=60 vflip=true xscale=2.5 yscale=5.6
    beenhit=OnBeenHit 
    center=20,25 click=clickWM composition="xor" 
    enterframe=clickWM exitframe=exitFrame
    hashit=OnHasHit hflip=true 
    mousein=mouseInWM mousemove=mouseMoveWM
    mouseout=mouseOutWM 
    parent=PlayArea penultimate=penultimateExit
  having target=bumbleBee children=(fin1,fin2) 
    alt=spinal,moveUp 
  set memvar1="dog" memvar2=4 
end
```

## Parameters
- **into** sprites can be grouped and the groups can be used as subjects or targets of different operations (ex: collision detection).
- **where** clause lists properties of the sprite. Here they are:
  - x={number}
  - y={number}
  - size={number}
  - hflip={true|false} flip the sprite horizontally about the center point.
  - vflip={true|false} vertical position of sprite based on the sprite's center
  - xscale={number} scale the sprite horizontally
  - yscale={number} scale the sprite vertically
  - alpha={range 0.0-1.0}
  - angle={number}
  - composition={See below}
  - center={number},{number} OR auto (example: center=auto)


create sprite as MySprite where x=7 y=334 end

0.0 makes sprite completely transparent. 1.0 makes the sprite fully opaque.
at what angle to place sprite relative to the unit circle (0 degrees is default and is pointing towards the right)
beenhit={routine}
specify a routine to run when it has been hit by another sprite
specify the sprite’s 0,0 origin relative to the 0,0 position of its image. The center given is the point around which the sprite will rotate, placed on the screen, or used as a collider.
click={routine}
specify a routine to run when the mouse click while on an opaque portion of the sprite. Set to _ignore to disable all user interactions on the sprite.
This parameter determines how a sprite is drawn with respect to the background. It can be one of: "source-atop", "source-in", "source-out", "source-over", "destination-atop", "destination-in", "destination-out", "destination-over", "lighter", "copy", "xor". It is best to experiment to see what you need 
enterframe={routine}
specify a routine to run when the frame is entered
exitframe={routine}
specify a routine to run after the penultimate event and after all variable conditions have been checked and all the completion routines have finished running.
hashit={routine}
specify a routine to run when this sprite has hit its target (see target below)
mouseup={routine}
specify a routine to run when the mouse button is released over an opaque portion of the sprite
mousedown={routine}
specify a routine to run when the mouse depressed over an opaque portion of the sprite
mousein={routine}
specify a routine to run when the mouse moves onto an opaque portion of the sprite
mouseout={routine}
specify a routine to run when the mouse moves out of an opaque portion of the sprite
mousemove={routine}
specify a routine to run when the mouse moves within an opaque portion of the sprite
parent={sprite}
specify a parent sprite onto which to attach this sprite as a child
penultimate={routine}
specify a routine to run after all sprites are processed for the frame, but before the var conditions are tested
set {name}={value}
creates a variable specific only to the sprite. Do not use the same name as one of the built in properties
scale the sprite relative to its natural size. Size=1 is normal size
touchdrag={routine}
indicates that the sprite can be dragged via touch on a touch screen device
touchend={routine}
specify a routine to run when a sprite touch is lifted off a touch screen device
touchstart={routine}
specify a routine to run when the sprite is first touched via a touch screen device
flip the sprite vertically about the center point.
horizontal position of sprite based on the sprite's center

having clause
Sprite have some parameters that can have more than one value. These parameters are preceded by a "having" clause: 
create sprite as MySprite having children=(dog,cat) end

alt={alteration} alt={alteration}...
apply an alteration to the sprite. A sprite can have any number of alterations applied to it by assigning alt repeatedly.
children=({sprite},{sprite},...)
specify a list of sprites that move and orient themselves relative to this sprite. Children sprites do not need to be launched separately but are automatically launched when its parent sprite is launched. Note, child sprites absorb events and do not relay them to the parent. Set touch events on child sprites, not the parent sprite. This will change in upcoming releases.
target={sprite}
specify a single sprite for which to trigger a collision event
targets={spritegroup}
specify a group of sprites which can all trigger collision events. Sprites are assigned to groups using "into" (see above)
