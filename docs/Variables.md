# Vars

```create var as {name} [into {levelName}] [where [value={value}] [condition={value}] [completion={routine}] end]```

Variables are not an alteration but a way of tracking values and using them later. They have a special feature built into them, that if they have a certain value, they will trigger a completion event. You set that value with the **condition** property.

First you define your variable, then you **add** or **subtract** from it in a routine. You may also set the variable value explicitly. Here are the 3 ways to change the value of a *var* object:
```
update var countHits set=1
update var countHits add=1
update var countHits subtract=1
```

In the example below, if the value of *countHits* ever reaches 0, then a routine called countDone is run.
```
create var as countHits 
  where value=3 condition=0 completion=countDone 
end 
create routine as spriteHit 
  update var countHits subtract=1 
end 
```

You can also create a **var** using shorthand. Shorthand allows you to simply create a variable and assign it value like: var MyVar="pineapple" The above is equivalent to: ```create var as MyVar where value="pineapple" end```. The shorthand does not allow you to add conditions or completion events but the variable created with shorthand can be changed and manipulated in all the same ways as a full declaration.

There are 2 kinds of **var** commands. One created inside a routine, and ones create outside a routine (or "globally"). Using **var** inside a routine only stores a value and *does not* support any of the properties of a global **var**. In fact, a **var** created inside a routine is just a storage tag.

This page only refers to global vars.

## Parameters
- **into** {levelName}
   - Assigns the variable to a *level*. The allows the var to have different values depending on the current level. A level is set inside routine with the **set level={levelName}** command. This mechanism works together with data levels and are ideal for game development.
- **where**
   - **value**={number} the starting value of the variable.
   - **condition**={number|string} The condition of variables are checked just once per frame, after all sprites have been processed. The order in which different variable conditions are met is indeterminate. Therefore you cannot know the order that routines will be called as different conditions are met in that frame. 
There are 2 frame events which can help in processing your variable conditions. Conditions are checked after the "penultimate" frame event, and before "frameexit". If the value held by the variable reaches this "condition" value, then the completion event will fire.
   - **completion**={routine} specify a routine to run when the value of the variable reaches the condition.

> [!NOTE]
> Try out code samples at https://canvaslanguage.com/studio/github-examples.
> Paste the code samples into the box under that "Advanced" tab,
> then push the "Rec" button to view the animation.

```
create var as ClickCount
  where value=3 condition=0 completion=ClicksDone
end
create routine as Start
  draw onto _bottom
    font "normal 300 20px sans-serif"
    filltext "Click 3 times",20,20,500
  enddraw
  set click=OnClick
end
create routine as OnClick
  update var ClickCount subtract=1
  draw onto _bottom
    clear
    font "normal 300 20px sans-serif"
    filltext ClickCount.value,20,20,500
  enddraw
 
end
create routine as ClicksDone
  draw onto _bottom
    clear
    font "normal 300 20px sans-serif"
    filltext "Done.",20,20,500
  enddraw
  set click=_none
end
```

