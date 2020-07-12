# Gakujin no Uta

This example shows one possible workflow, starting from a full MuseScore 3 file all the way to the final ASS file.

The final lyrics are timed to [【ヤマノススメ】岳人の歌　まとめ](https://youtu.be/hJbxgklq6uU) ("Yama no Susume" Gakujin no Uta compilation) by 笠松翔太 at 0:00:47.01.
The song is Gakujin no Uta (岳人の歌; Song of the Alpinist), composer and lyricist unknown.

This example makes use of MSCX files, which can be opened with [MuseScore 3](https://musescore.org/).
When following a similar workflow, MSCZ files maybe used instead of MSCX files.
The MSCX format is only used because it is more suitable for storage in a Git repository.

## Example workflow

1. `01 - Gakujin no Uta (full).mscx`: Start with a base file.
   This can be an existing arrangement as a MIDI file or as sheet music that you found online.
   If you're starting from scratch, you can skip this step.
2. `02 - Gakujin no Uta (rhythm).mscx`: Reduce the music down to a rhythm on a single track.
3. `03 - Gakujin no Uta (rhythm).mid`: Export the MSCX to MIDI.
4. `04 - Lyrics.txt`: Write the lyrics file, creating one syllable per MIDI note.

   `04 - Gakujin no Uta (rhythm).csv`: (Optional) Run `midicsv "03 - Gakujin no Uta (rhythm).mid"` and save the output.
5. `05 - Output.txt`: Run `midicsv "03 - Gakujin no Uta (rhythm).mid" | midicsv2ass "04 - Lyrics.txt"` (or `midicsv2ass -i "04 - Gakujin no Uta (rhythm).csv" "04 - Lyrics.txt"` if you saved the output in the last step).
   The output is sent to stdout, which can be saved to a file if desired.
6. `06 - Gakujin no Uta.ass`: Copy the lines to an ASS file and shift.
