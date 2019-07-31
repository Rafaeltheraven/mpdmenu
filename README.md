Advanced dmenu frontend for MPD.

# Arguments

Pass mpdmenu arguments first, followed by any dmenu arguments. They are separated by `::`. For example:

    mpdmenu -p :: -sb '#000000'

There are 2 types of arguments, "search" arguments and "mode" arguments:

## Mode Arguments
`-l` - library mode (default), used to search through your library

`-p` - playlist mode, used to select a track from the current playlist (search arguments have no effect here)

`-c` - clears the current playlist before adding a new item

## Search Arguments
`-a` - search by `artist` tag

`-A` - search by `albumartist` tag

`-al`- search by `album` tag

`-g` - search by `genre` tag

`-t` - search by `title` tag

## Order of Arguments
While mode and search arguments can be added in any order, the order of the search arguments is important
as they are processed in order. For example, if you wanted to search through your library in the flow:

`genre` -> `albumartist` -> `album` -> `title`

You would call `mpdmenu -g -A -al -t`. Any input you give in the view of a previous tag will restrict your
search in the next tag (unless the `[ANY]` option is chosen). If no search arguments are passed, mpdmenu
will just add all your music to the playlist.

# mpdmenu_classic

`mpdmenu_classic` is an updated variant of the classic mpdmenu as originally forked from cdown. 
It was made when I realised that mpdmenu needed a complete overhaul in the way it worked so I could make a back button.

`mpdmenu_classic` lacks features that the new `mpdmenu` has, but might be slightly simpler in use. It does not have:

* A back button
* Ability to choose your own workflow
* Support for BOTH `artist` and `albumartist` tag

Instead, you have the following arguments:

`-l` library mode (default)

`-p` playlist mode

`-t` track mode, same as library mode but allows you to pick a single track

`-a` use `albumartist` tag instead of `artist`

`-c` clears the current playlist before adding a new item

Regardless of arguments, you will have the flow

`genre` -> `albumartist`/`artist` -> `album` (-> `track` if `-t` is enabled)
