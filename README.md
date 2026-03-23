# EOS-busk-sheet-indicators
ETC Eos busking magic sheet with current/next cue indication. Minimal reliance on macros, heavy reliance on cue lists.

I was recently hanging out with an MA3 programmer for a busking show, and envying their color selection grid. I went home and spent the next few days working on this setup, which I'm pretty happy with. It's based off of Mark LaPierre's eos busking template tutorial, so the general sense of what's going on with the cue lists should be answered in there.

![magic sheet](/img/sheet.png)


## What is it?

It's a standard grid color picker, but better: it shows what color is active on a system, and what your next selected color is (if you're in manual mode).


## Notes

You can swap between manual (on a fader) or timed fades. The color picker itself is entirely cue-based; the only macros are to adjust timing settings, and to assert all faders if in manual mode.


## How to use

This picker relies on cue lists 100/ thru 110/; you could change these but it would take some work updating macros.
Ideally I would use macros as easy-change variables, but I didn't do that to start, and it'll take some time for me to make the change.
It also relies on macros 101 thru 107, 111 thru 120, and 200 thru 207. These are, again, all changeable, but could be frustrating to edit; they're called in cues, on the magic sheet, and (esp in the 200 range) from other macros.

To use it in a show file of your own, you'll need to import:

* fixtures (you'll need the dummy fixture profile)
* patch (again, for dummy channels)
* groups
  * or you can use your own here; just be sure to
    * assign your filters on the cue lists
    * update the group buttons on the sheet
* cue list 100/
  * if you put it somewhere else, you'll have to update the magic sheet; this isn't entirely painful, but it's not nothing
*macros
  * 101 thru 107 to change cue timing
  * 111 thru 120 to assert all picker cues simultaneously
  * 200 thru 207 to build ("cook") color picker cues
*color palettes 1 thru 25 if you want to
  * you can use your own if you want, but they won't match what the magic sheet shows
  * i'll fix that someday
*fader config if you want to
  * you just need to have cue lists 100/ thru 110/ mapped to faders, you can easily do this yourself wherever you want


## Action Pics

![selected colors, pending a manual timing](/img/selected-moves.png)
![the result](/img/completed-moves.png)


## Gripes/Bugs/Todos/Other Notes

* The indicators are done with a dummy channel in each cue list, and point cues to manage setting the dummy color before setting the fixture color. I think that in retrospect I could have done this with part cues, which could be a little more elegant.
* Also on the future list: assigning the cue selection circles by a color palette inside of the cue, rather the hard-coded situation that I have at the moment. I think this is trivial by adding an rgb cell to the dummy channels and including it in the color palettes up front, then putting another circle object behind the (transparent) cue selector to reference that channel.
* Asserting all faders is pretty slow, because I can't select multiple cue lists at a time - this means that I have to step through each one in turn. Same with the timing selection macros, although I find that less problematic.
  * if I were firing multiple color changes at one time off this chart, I would do it with fader buttons and multiple fingers
* If you look at the macros, you'll see a lot of repetition. My kingdom for variables in eos macros!
  * I included the macros that you would need to massage parts of the showfile back into working, because they're what I used to get everything formatted. 
  * There's no documentation (apart from one text file I wrote for m10099, which I'm including here), and style/ideas are a little varied, but it worked well enough for me.
