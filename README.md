Simple dmenu frontend for MPD.

# Arguments

Pass mpdmenu arguments first, followed by any dmenu arguments. They are separated by `::`. For example:

    mpdmenu -p :: -sb '#000000'

There are 2 types of arguments, "search" arguments and "mode" arguments:

## Mode Arguments
`-l` - library mode (default), used to search through your library

`-p` - playlist mode, used to select a track from the current playlist (search arguments have no effect here)

`-c` - enables mpd's consume mode

## Search Arguments
`-a` - search by `artist` tag

`-A` - search by `albumartist` tag

`-al`- search by `album` tag

`-g` - search by `genre` tag

`-t` - search by `title` tag

While mode and search arguments can be added in any order, the order of the search arguments is important
as they are processed in order. For example, if you wanted to search through your library in the flow:

`genre` -> `albumartist` -> `album` -> `title`

You would call `mpdmenu -g -A -al -t`. Any input you give in the view of a previous tag will restrict your
search in the next tag (unless the `[ANY]` argument is chosen). If no search arguments are passed, mpdmenu
will just add all your music to the playlist.
