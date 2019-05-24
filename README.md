Simple dmenu frontend for MPD.

# Arguments

Pass mpdmenu arguments first, followed by any dmenu arguments. They are separated by `::`. For example:

    mpdmenu -p :: -sb '#000000'

`-l` is library mode (default), which descends artists and albums. `-p` is
playlist mode, which selects a track from the current playlist.
`-t` enables track mode, allowing you to pick a single track after selecting an album.

By default this program sorts by `artist`, if you want to sort by `albumartist` instead, use the `-a` flag.
