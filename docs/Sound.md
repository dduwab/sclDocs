# Sound

Use "create" to create a sound object and in a routine specify which sound to play and other manipulations.
To play a sound, it must be in mp3 format for maximum portability. Some browsers may have issues with sound fade effects.

_all rather than a sound name can be used for: play, mute, unmute, pause, and unpause.

```
create sound from "music1.mp3" as sndMusic1
  where repeat=3 volume=0.4 fadein=500
end

create sound from "music2.mp3" as sndMusic2
  where repeat=2 volume=0.8 fadeout=1000
end

create routine as ChangeMusic
  stop sound sndMusic1 where fadeout=1200
  play sound sndMusic2
  pause sound sndMusic2 where fadeout=500
  unpause sound sndMusic2 where fadein=500
  mute sound sndMusic2 where fadeout=500
  unmute sound sndMusic2 where fadein=500
end
```

## Parameters
- **where**
  - **from** {mp files} a double-quoted " sound file name.
  - **as** {name} the name of the new sound object.
  - **completion**={routine name} the name of a routine to run when the sound finishes playing.
  - **volume**={0-1} set between 0.0 and 1.0 inclusive
  - **fadein**={milliseconds} the time for which the fadein should last.
  - **fadeout**={milliseconds} the time for which the fadeout should last. This may be limited by some platforms to require a value greater than 300 for best-sounding effect.
  - **repeat**={number} of times the sound repeats. Use a really high 9999999 number for continuous play.

