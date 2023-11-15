# Wait
The wait alteration isn't an alteration so much as a timing device. When applied to a sprite it will trigger a completion event after the given number of milliseconds.

```
create sprite from arrow.png as Arrow
  where center=0,26 x=250 y=250 angle=90
  having alt=Timer
end 
create wait as Timer
  where
    delay=500 repeat=forever completion=TimerDone
end
create rotation as Rot1 where speed=-400 easeout=10 distance=30 end

create routine as Start 
  launch Arrow
end 
create routine as TimerDone 
  insert into Arrow where alt=Rot1
end
```
> [!NOTE]
> Try out code samples at https://canvaslanguage.com/studio/github-examples.
> Paste the code samples into the box under that "Advanced" tab,
> then push the "Rec" button to view the animation.

## Properties
- **where**
  - **delay**={number} number of milliseconds to pass before triggering the completion event. The timer starts when the alteration is added to the sprite or the sprite is launched.
  - **repeat**={number|forever} specify the number of iterations that the wait should occur, or mark it to repeat it forever. The completion routine will be called after each iteration and the _repeat value in the routine will be set to which iteration this is, starting at 1.
  - **completion**={routine|alteration} specify a routine or alteration to run when the timer delay is reached.


## Pausing a wait
A wait can be paused and unpaused in a routine: 

```
pause wait WaitName
unpause wait WaitName
```

To use pause/unpause, the 'wait' must have a name. Therefore it cannot be anonymous, and it cannot be an unnamed clone. 
