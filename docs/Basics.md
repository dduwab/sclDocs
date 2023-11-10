# Basics of an SCL Animation

All SCL scripts begin with the **Start** routine. **Start** is the only upper-case keyword in SCL, and SCL identifier names are case-sensitive. Start is very important and it is the first thing your animation does. Usually it will launch your first sprites.

```
create routine as Start
  launch MyAirplaneSprite
end
```

That is just the beginning of SCL. We must also define sprites, and animations. These tasks are simply pieces that need to be assembled.

Basic SCL code consists of:

**Sprites**
- That define the images that are animated

**Routines**
- That control how your animation plays

**Alterations**
- That define the animations to be applied to sprites

**Events**
- That control interactions between sprites and users

```
create sprite from fan.png as spinner
  where x=100 y=100 center=90,90
  having alt=ThisWay
end
create routine as Start
  launch spinner
end
create rotation as ThisWay
  where speed=130 distance=135 completion=ThatWay
end
create rotation  as ThatWay 
  where speed=-130 distance=135 completion=ThisWay
end
```

In the example above, **Start** launches a sprite and that sprite has a rotation alteration assigned to it that is called **ThisWay**. When that rotation is complete, it assigns the next alteration to the sprite, called **ThatWay**. And when **ThatWay** completes, it assigns **ThisWay** to the sprite… and the circle of animation goes on.

This is the basic process of all SCL animations. Launch sprites, and assign alterations to them.


## Changing Alterations

The primary purpose of routines is to change sprite alterations. You can do this 2 ways:

Adding alterations to a sprite:
```insert into {spritename} where alt={altname}```

Removing alterations from a sprite:
```remove from {spritename} where alt={altname}```

For efficiency you can also use a "sub" to define an alteration inside a routine instruction:
```
insert into {spritename} where alt=(sub
  create rotation where speed=700 distance=530
  end)
```

Alterations defined in routines can be anonymous - they don't need to be named. However it is your responsibility to include an end-point as part of the alteration otherwise the alteration will run forever and can only be removed if all alterations are removed from the sprite. An end-point, for example, is setting a destination or distance to how far a sprite should rotate. When the end-point is reached, the rotation is done and is automatically removed from the sprite.

## Chaining Alterations

Sprite effects in SCL are called Alterations because they alter the sprite in some way. When an alteration completes, an event can be fired for which you can instruct SCL to do something else. That something else can be either to run a routine or to apply one or more alterations. Being able to apply a new alteration when an alteration completes allows for making a chain of alterations.

Anonymous alterations are alterations that may not be given a name but are defined within the completion event.

```
create sprite from 2.png as whatever
  having alt=(sub create slide
      where direction=0 distance=50
    end)
end
```

In the example below a sprite is moved around using a chain of alts. The first alteration requires a name, FirstSlide, so that the last alteration can refer back it to restart the sequence.

```
create sprite from sclicon160x160.png as whatever
  having alt=(sub
    create slide as FirstSlide
      where direction=0 distance=50 completion=(sub
    create slide
      where direction=270 distance=50 completion=(sub
    create rotation
      where speed=600 distance=720 completion=(sub
    create translation
      where x=0 y=0 completion=FirstSlide
    end) end) end) end)
end
create routine as Start 
  launch whatever 
end
```

## Event Handlers

When an alteration completes, the completion event handler can specify another **alteration** or a **routine** to run. Routines run this way are called **event handlers**. If the value assigned to *completion* is the name of a **routine**, then that **routine** is run. 

```
create sprite from fan.png as spinner
  where x=100 y=100 center=90,90
end
create routine as Start
  launch spinner
  run routine ThisWay
end
create routine as ThisWay
  insert into spinner where
    alt=(sub create rotation as rot1 where speed=130
      distance=135 completion=ThatWay end)
end
create routine as ThatWay
  insert into spinner where
    alt=(sub create rotation as rot2 where speed=-130
      distance=135 completion=ThisWay end)
end
```
## Syntax

SCL isn't as loose with rules as some other scripting languages. Here are a few extra rules:
1. No extra whitespace is permitte where it isn't necessary. Therefore, not spaces within an expression like math. For example: 7 + 8 is bad, but 7+8 is good.
2. No extra whitespace inside parenthesis. For example: ( "bad" ) ("goood")


