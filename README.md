# Humdrum figured bass filter demo

Based on the [`hint -l`](https://www.humdrum.org/Humdrum/commands/hint.html)
command it should be possible to create a filter for Humdrum that adds spines
for automatic detection of the figured bass numbers. For each part separately as
*Intervallsatz*, or as real basso continuo numbers.

With the hint command you get specific intervals like e.g. "major third" (M3) or
"minor third" (m3). But with figured bass it does not matter if an interval is
major or minor. Instead the relation to the key and the key signature needs to
be taken into account.

An implementation into the Verovio JS toolkit would be appreciated to create
such an analysis on the fly in the browser. Similar to the existing `cint`
filter.

## Examples

Here is a test set of what I think this command should be capable of.

### 1. Verbose *Intervallsatz*

Calculate the exact intervall without converting compound to non-compound
intervals.

[01.krn](kern/01.krn) | [View in
VHV](https://verovio.humdrum.org/?file=https://raw.githubusercontent.com/WolfgangDrescher/humdrum-figured-bass-filter-demo/master/kern/01.krn)

NB: In bar 6 on the second 16th note the alt voice goes below the bass note.
`-2` of even `-2#` seems like the correct intervall here (see problem 3) but it
cannot be displayed by Verovio.


### 2. Compound *Intervallsatz*

Calculate the the compound intervals. `-c` could be the argument here similar to
the hint commnad.

[02.krn](kern/02.krn) | [View in
VHV](https://verovio.humdrum.org/?file=https://raw.githubusercontent.com/WolfgangDrescher/humdrum-figured-bass-filter-demo/master/kern/02.krn)


### 3. Verbose figured bass (detailed)

Merge both *Intervalsätze* from example 1 to a single figured bass line.

[03.krn](kern/03.krn) | [View in
VHV](https://verovio.humdrum.org/?file=https://raw.githubusercontent.com/WolfgangDrescher/humdrum-figured-bass-filter-demo/master/kern/03.krn)


### 4. Compound figured bass (detailed)

Merge both *Intervalsätze* from example 2 to a single figured bass line. Again
with the `-c` flag.

[04.krn](kern/04.krn) | [View in
VHV](https://verovio.humdrum.org/?file=https://raw.githubusercontent.com/WolfgangDrescher/humdrum-figured-bass-filter-demo/master/kern/04.krn)


### 5. Compound figured bass (simplified)

Same as example 4 but with simplified figured bass numbering.

[05.krn](kern/05.krn) | [View in
VHV](https://verovio.humdrum.org/?file=https://raw.githubusercontent.com/WolfgangDrescher/humdrum-figured-bass-filter-demo/master/kern/05.krn)


## Problems, questions and ideas

 1. Name of the command is tbd.
 2. Calculating intervals relativ to a specified spine seems usefull so it
    would be possible to pass different voices as base via arguments to the
    command.
 3. Could there be an argument to always calculate the intervals relative to the
    lowest note, ignoring the given base voice/staff? Since there is music where
    the lowest note is not always in the bass.
 4. Should negative value be allowed?
 5. Should there be a difference between 1 and 8 for the *Intervallsatz*?
 6. How could we calculate the difference between 2 and 9?
 7. Negative values are not allowed in `**fb` spines since the `-` get
    translated into a flat accidental. Should this be implementet or does this
    need a new interpretation records?
 8. Add option to only calculate intervals or figured bass on certain beats
    (quarter notes in 4/4, oder 1st and 4th eighth note in 6/8).
 9. How can we get this command in VHV and the Verovio JavaScript toolkit?
10. Add option to ignore negative intervals?
11. Decide how to display `5 4` to `6 4` in bar 7 (with 5 or without). Maybe add
    a config with a flag.
12. Decide how to display `5 3` chors. Never? Always? Contextual? Maybe add a
    config with a flag.
13. Should `-#2` in bar 7 resolte to 1/8?
14. `-c` option should be default with another flag to display them not
    compounded.
