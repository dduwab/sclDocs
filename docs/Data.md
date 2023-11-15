# Data Structures in SCL
There are two types of data structures in SCL: Lists and key/value pairs.

## Data Lists
Lists let you keep a set of values that you can access in loops. There are many special commands that help you go through a list.

```
create data from list as MyList
set
  “yellow” “red” “blue”
End
```

## Data Pairs
Key/value pairs let you access values using a 'key' name that you give the value. This is a convenient way to store and retrieve data that is used through-out your program. 

```
create data from pairs as MyPairs
set
	x=100 y=222 z="hi there"
end

create routine as OnClick
	update sprite _sprite set x=data.MyPairs.x
	update sprite _sprite set y=data.MyPairs.y
	var data.MyPairs.y=333
end
```

## Data Letter
Letter can be pulled individual out of strings in cases where you want to treat each letter as a data value.
```
var LASTWORD="dude"
create data from letters as WordBits
set
  "Welcome" "Everyone" "and you" LASTWORD 
end
```
When processing letters, no distinction is made between words. Every value in the example above is combined into a single long string and processed letter by letter that way. Like so: "WelcomeEveryoneand youdude" - if you want spaces, add " them yourself "
## List Processing
List processing is done inside routines with these commands.

```
current retrieves the current value
update sprite Dog where x=data.MyList.current
next retrieves the next value in the list
var nextVal=data.MyList.next
prev retrieves the previous value in the list
var prevVal=data.MyList.prev
select retrieves a random value from the list
update var curId set=data.Ids.select
pluck retrieves a random value from the list, and will not retrieve that value again. Use “update data MyList renew” to reset the list and pluck it again.
var nextCard=data.CardDeck.pluck
tofirst move the pointer back to the first item in the list. When you move through a list using data..next, a pointer tracks where you are. To return to the start of the list, use tofirst
update data MyList tofirst
Changing Lists
push will add a value at the end of the list.
update data MyList push dogSprite.x
pop will remove the value at the end of the list and return it. (ex: update var NAME set data.LISTNAME.pop) fush will add a value to the beginning of the list.
update sprite _sprite where angle=data.MyAngles.pop
fop will remove the value from the beginning of the list and return it.
update sprite _clone where angle=data.MyAngles.fop
remove will remove the first instance of the given value from the list remove _all will remove all items from the list
update data MyList remove “red”
update data YourList remove _all
reset will reset the list to its original state (as given by its 'create' statement).
update data MyList reset
renew will re-randomize the list. This is useful when using pluck or select
update data MyList renew
set will set a particular list item value. The value to change is specified by the position (1-based) that it appears in the list. The first item is number 1. 
update data MyList set 3=”new value”
```

## Getting List Information
Data also supports some information requests in the form data.LISTNAME.request

- contains({test value}) returns true if the test value exists in the list. 
```
var result=data.MyList.contains("happy dog")
if (result==true)
  launch Bone
endif
```
- count returns the number of items in the list
```var listCount=data.MyList.count```
- current returns the current item in the list without changing where you are in the list.
```var currentSprite=data.SpriteList.current```
- first returns the value of the first item in the list
```var firstItem=data.MyList.first```
- fopped returns the value that was most recently returned using fop. IE: fopped items are items just removed from the front of the list using fop
- ```get({position in list})``` get the value at the given position in the list (1-based indexing).
```var item7=data.MyList.get(7)```
- last returns the value of the last item in the list
```var last=data.MyList.last```
- popped returns the value that was most recently returned using pop
```var popped=data.MyList.popped```
- position returns a number from 1 to {n} indicating at what position you are in the list as you move through it.
```var pos=data.MyList.position```
- remaining returns the number of items left as you move through it
```var firstItem=data.MyList.last```

## Calling Routines with Data
You can pass data to routines in two ways: using repeat or by passing the data object as a parameter.
```
run routine FinalizeMonkeys where repeat=data.MonkeyList
create routine as FinalizeMonkeys
  var nextMonkey=data.MonkeyList.next
// … do stuff …
End
```

repeat will cause FinalizeMonkeys to be run repeatedly until the end of the data list is reached. Inside the routine, we assign the next value in the list to a local var, in this case nextMonkey.

**IMPORTANT**: It is vital that you call data.MonkeyList.next inside the routine else your animation will call the same routine forever using the same value from the data object.

The second method to pass data to routines is to pass the data object as a parameter. For example:

```
create data from list as MyData set 1 2 3 end
create routine as Start
  MyR(data.MyData)
End
create routine as MyR
  var dataObj=arg.1
  update sprite MySprite where x=dataObj.next
end
```

In the above example, the data is passed as a parameter and the parameter is assigned to a local var. This makes is available to the routine as a normal(ish) object.
```
var PList=arg.1
update sprite MySprite where x=PList.next
```

Setting up levels in SCL
Levels are supported in SCL by assigning data or variables into levels. You then select a level by setting the global level variable. Names for data and variables assigned to different levels have the same name, but different level names. Then when a value is requested by a given name, the value for that level is used. Levels can be names or numbers.
Example 
```
create data from list as charNames into Level1
set
  "Sue" "Mary" "Johnny" "Casper"
end
create data from list as charNames into Level2
set
  "Larry" "Steward" "Ann" "Nadine"
end
create var as EastGuy into Level1 where value="ED" end
create var as WestGuy into Level2 where value="STEVE" end

create routine as Start
  set level=Level1
  log(data.charNames.next) // prints "Sue"
  log(EastGuy) // prints "Ed"

  set level=Level2
  log(data.charNames.next) // prints "Larry"
  log(WestGuy) // prints "STEVE"
end
```
