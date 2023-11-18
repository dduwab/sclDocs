# Vars

(Programmers are going to hate this)

Variables are not an alteration but a way of tracking values and using them later.

First you define your variable, then you add or subtract from it in a routine. You may also set the variable value explicitly.

Variables can be set to run a routine when a particular value is set or reached. 

You can also create a var using shorthand. Shorthand allows you to simply create a variable and assign it value like: var MyVar="pineapple" The above is equivalent to: create var as MyVar where value="pineapple" end The shorthand does not allow you to add conditions or completion events but the variable created with shorthand can be changed and manipulated in all the same ways as a full declaration. 

Note that this use of 'var' is done outside of routines. Using 'var' inside a routine is a local variable and behaves differently. Read about them in routines documentation. 

```
create var as countHits 
  where value=3 condition=0 completion=countDone 
end 
create routine as spriteHit 
  update var countHits subtract=1 
end 
```

## Parameters
value={number}
the starting value of the variable.
The condition of variables are checked just once per frame, after all sprites have been processed. The order in which different variable conditions are met is indeterminate. Therefore you cannot know the order that routines will be called as different conditions are met in that frame. 
There are 2 frame events which can help in processing your variable conditions. Conditions are checked after the "penultimate" frame event, and before "frameexit". 
condition={number}
if the value held by the variable reaches this "condition" value, then the completion event will fire.

completion={routine}
specify a routine to run when the value of the variable reaches the condition.

