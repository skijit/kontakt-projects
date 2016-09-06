Kontakt Script to Retune Instruments
===================
- **Basic Idea** is to be able to make any Kontakt Instrument follow a different tuning system.
- **Main Appliction** of that idea is to play a piano tuned as a gamelan

## Musical Underpinnings
- See about [stretched tunings](https://en.wikipedia.org/wiki/Stretched_tuning)
- See about [gamelan tunings](/journal/music/Semara dana tuning.xlsx)

## Expected Interface
- There would be about 20 groups of 4 text boxes
- Each of the 4 represents something different about the note:
    1. Incoming MIDI note
    2. Remapped MIDI note
    2. Normal F0 of Remapped note
    3. New F0 of the Remapped note
- Entering data in the group turns **ON** the corresponding Incoming MIDI note.  Otherwise, the note is not passed through.
- When an **ON** Incoming Note is triggered, the script will:
    1. Change the message to refer to a different MIDI note (i.e. the one specified in box 2)
    2. Calculate a detune amount based on the Remapped note's actual F0 and it's desired F0.    
        - For performance reasons, perhaps there will be a button to force recalculation of all the **ON** note's detune amounts.    
- Given a different tuning system like a gamelan, you would:
    1. Figure out the corresponding MIDI notes of the keys you want to play.  (EG maybe you only want to play black notes or white notes) \[Box 1\]
    2. Figure out for each of those notes you play, what F0 you want to hear. \[Box 4\]
    3. Find the MIDI note whose F0 is closest to the desired F0 \[Box 2\].  This is the remapped MIDI note.
    4. Enter the F0 for the MIDI note.  You can use all kinds of tuners (hardware and software) to determine this experimentally.
    5. Maybe press the 'Recalculate' button, if one exists
- The reason for remapping the incoming MIDI note is
    - Detuning a large amount generally sounds weirdly artificial. 
    - If you just detune the notes you want to play, you'll have big, weird-sounding repitching. 
    - If you only play the nearest neighboring keys to the target F0's, then you might have to remember a weird looking scale.
    - SO: it's probably best to decouple the notes you play from the notes you bend.
      
### Questions:
- How to save/load a setting.

## Implementation

## Development Notes
- Start by transposing a fixed note by a fixed value (d)
- See if you can modify the tuning at all (d)
- Then create 2 text boxes and transpose from box 1 to box 2s
    - save and see if the text box values are retained
    - width and placements
    - **Q**: can I set the units to HZ also?
    - **Q**: how do I position these?s
- Then create a grid of text boxes that work like this
- Add a calculate button to the grid and have it set some values in the primary data structure (an array)
- Then find the detune knob and adjust it by a variable amount (reseting it first for each)
- Do the cent-based calculation
- **CAVEATS**
    - reset the tuning for each note-on
    - tuning is a 'source' param, so I need to make the script monophonic otherwise one note's detune will bleed into anothers
        - I don't want to set voices to 1 in the instrument header though bc that will mess up release triggers and other zones associated with a single note.
        - so I need to make it monophonic in the code (if possible)ss
- the values I might want to make_persistent are the gamelan target tunings for the given instrument.  then, I would save these with the instrument preset.s

TODO:
    - figure out the UI and underlying data structure setup
    - ask on vi-control whether I can determine the s.offset progrrammatically so I don't have to use DFD
    - load 6 instances of kontakt in sampler mode to see if it's a problems
    
