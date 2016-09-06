DeTuner README
===================
- **Basic Idea** is to be able to make any Kontakt Instrument follow a different tuning system
- **Main Appliction** of that idea is to play a piano (or other sample library) tuned as a gamelan instrument

## Usage
- There will be various presets available to speed up the tuning
- Presently, a max of 15 notes per script can be remapped.
    - But, you could have multiple instances of this script running in different slots.
    - Each row in the table is a remapped / retuned note.
- Each retuned note has 4 variables, corresponding to the 4 columns in the UI 
    1. Triggered Note
        - The MIDI note on the controller (e.g. keyboard) you want to physically play (i.e. trigger)
    2. Mapped Note
        - The note that will be repitched for the given trigger note.
        - Typically, this will be note in the given sample library whose frequency is closest to the frequency you want to hear.
            - That's bc as the retune amount increases, the results sound more artificial.  
    3. Mapped Pitch
        - This is the F0 (in Hz) for the mapped note (previous column)
    4. Target Pitch
        - This is the F0 (in Hz) that you want to hear.
- Based on these input values, the script will calculate and apply a cent-based detune amount.

## Theoretical Background
- TODO: General info
- While the just noticeable difference for tones is dependent on a variety of factors (e.g. volume, timbre, etc.), it begins around 3 or 4 cents. (TODO: get a reference here)  

## Bugs / TODOS
- **POSSIBLE BUG**: If the root key is already being shifted (ie 1 sample for multiple tones), not sure this will work.  Needs testing.
- Clean up code
- Recalc Button
    - Auto calc when loading a preset
    - Reset color after pressing
    - Change color when needing a Reset
- Column label names should be changed
- Menu driven selections for gamelan & std base mappings/tunings would be nice.


