# midicsv2ass

A Bash script to convert the output of `midicsv` to ASS k-timed Dialogue lines.

## Requirements

This script has only been tested on Linux, but it should run on any POSIX-compliant environment with bash and awk.

[`midicsv`](https://www.fourmilab.ch/webtools/midicsv/) is highly recommended.
While `midicsv2ass` does not make use of `midicsv` directly, it does act on its output

## Usage

This script would typically be a part of a pipe taking in the output of `midicsv`:

```bash
midicsv song.mid | midicsv2ass lyrics.txt
```

If the output of `midicsv` is in a file, use the `-i` flag to use the file:

```bash
midicsv2ass -i midi.csv lyrics.txt
```

Both will output k-timed ASS Dialogue lines to stdout.

For more comprehensive usage instructions, run the script with the `-h` flag.

Full examples can be found in the [examples](./examples) directory.

### MIDI file

The input MIDI file is expected to have one track containing the rhythm of the melody with no overlapping notes.
Any tracks after the first are ignored, and having overlapping notes in the first track will produce unexpected results.
The pitches of the notes are ignored; only their durations are considered.

This script will absorb small gaps between notes (gaps with a duration of one MIDI 32nd note or shorter) by considering them as part of the previous note.
Any gaps larger than a MIDI 32nd note will be considered as lead-in to the next note and will output an empty syllable immediately before the next.
That is of particular note when the next syllable starts a new line, as the empty syllable will also be on the next line.

See the examples for a sample MIDI file.

### Lyrics file

The lyrics file is a plain text file with one line per desired output ASS Dialogue line.
Syllables on each line are separated by a `|` character.
There should be one syllable per MIDI note.

See the examples for a sample lyrics file.

#### Splitting syllables

The output of the [`split-syllables`](./split-syllables) script can be used as a starting point to split words into syllables.
Often, its output cannot be used as-is and will need adjustments to match the actual syllables.

The lyrics file can be provided as an argument to the script or fed in through stdin.
The processed text will be sent to stdout.

The script is a thin wrapper around `sed` and any arguments passed to the script will be forwarded directly to `sed`.

## License

This project is licensed under the MIT license.
See the [LICENSE](./LICENSE) file for details.
