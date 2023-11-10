# Routines

Routines coordinate complex animations. The first routine run is called **Start** and is always run when the animation is started.

There are 2 ways that routines are run from code:
1. as an event handler of an alteration
2. called directly from another routine

In the example below, **Start** echos a string, then calls another routine called **Go** which also echos a string.
```
create routine as Start
  log("Hello from Start")
  Go()
end
create routine as Go
  log("Hello from Go")
end
```

## Passing Arguments
Routines also support arguments when listed between the parenthesis. **Important**: no white space is permitted inside the parenthesis unless they are also enclose in the double-quotes of a string literal.
```
create routine as Start
  Go("Hello",99)
end
create routine as Go
  log(arg.1)
  log(arg.2)
end
```

Notice with delight how the incoming argument is reference with that cool dotted syntax. Any number of arguments are supported.

## Looping with repeat
You can call a routine multiple times using a **where repeat** clause.
```
create routine as Start
  run routine Go("I am ") where repeat=3
end
create routine as Go
  log(arg.1+_repeat)
end
```
**_repeat** is a 1-based index. This script will log 3 lines, listing them like:
```
I am 1
I am 2
I am 3
```

**run routine** requires some explanation. Quite simply, if you want to run a routine multiple times, this is the format to do it. Once you learn more about SCL you'll see how this format is consistent with the rest of SCL. For the coders out there, you will not find any of your typical control loop structures in SCL. This is all the looping you get - it's fine though.

## Routine as Event Handlers

Routines are often called by the event handles of alterations (recall that alterations move sprites, like rotations or translations). Routines called by an alteration _completion_ event cannot have parameters. For example:
```
create sprite from ball.png as spinner
  where x=100 y=100 center=auto
  having alt=ThisWay
end
create rotation as ThisWay
  where speed=130 distance=135 completion=RotDone
end
create routine as RotDone
  log("All done")
  drop _sprite
end
create routine as Start
  launch spinner
end
```
When the animation starts it proceeds as follow:
1. it launches the spinner which has a rotation attached
2. once the rotation has travelled 135 degrees, it will stop rotating
3. it will call its completion event, **RotDone**
4. RotDone will then echo "All done"
5. and remove the sprite from the canvas using **drop**.

Please note the special variable **_sprite**. **_sprite** always refers to the sprite that called current routine.

## Conditional Statements

Routines supports flow control via **if** statements using this syntax:
```
if (a==b)
  ... do something
elsif (a==c && x==7)
  ... do something
elsif (a==d || y!=8)
  ... do something
else
  ... do something
endif
```
- You can next **if** statements up to 5 levels deep.
- You can have any number of **elsif** conditions
- No spaces are allowed inside the parenthesis
- Conditions must include some kind of equality operator
  - ie: forbidden this is **if (isBig)**, instead say **if (isBig==true)**
- Take note of the operators, **==, !=, >, <, >=, <=**
- Multiple conditions are acceptable, **&& ||** for 'and' and 'or'

## Local Variables
You can specify a named variable to use inside a routine using **var**. Note that this isn't a declaration, it is a command to make an assignment, therefore you use **var** anytime in the routine where you want to change its value.

```
create routine as Go
  var xloc=arg.1
  var yloc=arg.2
  if (xloc>yloc)
    var xloc=yloc
  else
    var yloc=xloc
  endif
  return xloc
end
```

## Exiting and Return

You can exit a routine with the **exit** command, and return a value from it using the **return** command.

```
create routine as Go
  return arg.1+arg.2
end
create routine as GoFaster
  if (arg.1==arg.2)
    exit
  endif
  log("They are different")
end
```

## More

Routines can do much more as they exist to manipulate sprites. For the purpose of clarity, routine commands for other components of the language will be discussed in their specific documents. This includes altering sprite properties, changing global variables, sound, using data sets, and much much more.

## Extra
Sneak peek with no explanation yet:
```run routine Go where repeat=data.MyList```
You'll learn later, in the **Data** section, how you can traverse data sets and set game levels with this mechanism.

