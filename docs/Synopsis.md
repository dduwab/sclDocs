# Synopsis

```
create sprite from star.png as Star
  where x=100 y=100 center=auto
  having alt=RotateClockwise
end
create rotation as RotateClockwise
  where speed=-90
end
create routine as Start
  launch Star
end
```

- All animations begin by calling the **Start** routine.
- The **launch** command will draw the named sprite onto the canvas and activate it.
- Sprites are the core object of an animation and are defined using a **create** command.
- Sprites are animated by attaching *alterations* to them. Each type of alteration defines a different type of movement or action for the sprite.
- Alterations are attached to a sprite using a **having** clause.
- The **having** clause can support any number of values; sometimes multiple values of the same type, for example **alt**. Any number of **alt** values can be provided in a **having** clause thus permitting multiple animations being applied to a sprite.
- **rotation** is a type of alteration that causes the sprite to rotate around its center point.
- Both sprites and alterations have a **where** clause. The **where** clause of objects provide property values for those objects.
- Properties of **where** clauses and values of **having** clauses may or may not be separated with an **and** keyword.

## Test Prompt
**ChatGPT 3.5**

Here is an md file explaining an animation programming language. Please read the following and write me a new animation that will display 4 hearts rotating counter-clockwise. The 4 hearts will be equidistant apart on a 500x500 sized canvas. The synopsis of the language follows:

*Then attached the synopsis description above.*

### Result
```
create sprite from heart.png as Heart1
  where x=250 y=50 center=auto
  having alt=RotateCounterClockwise
end

create sprite from heart.png as Heart2
  where x=450 y=250 center=auto
  having alt=RotateCounterClockwise
end

create sprite from heart.png as Heart3
  where x=250 y=450 center=auto
  having alt=RotateCounterClockwise
end

create sprite from heart.png as Heart4
  where x=50 y=250 center=auto
  having alt=RotateCounterClockwise
end

create rotation as RotateCounterClockwise
  where speed=-90
end

create routine as Start
  launch Heart1
  launch Heart2
  launch Heart3
  launch Heart4
end
```
**Passed**

