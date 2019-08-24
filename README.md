Advanced dmenu frontend for MPD.

# Arguments

Pass mpdmenu arguments first, followed by any dmenu arguments. They are separated by `::`. For example:

    mpdmenu -p :: -sb '#000000'

Any argument of the format `--[arg]=[value]` will be passed along directly to MPC. This can be used, for example, to control
the formatting shown or point `mpdmenu` to a specific MPD instance (using `--format` and `--host` respectively).

There are 2 types of arguments, "search" arguments and "mode" arguments:

## Mode Arguments
`-l` - library mode (default), used to search through your library

`-p` - playlist mode, used to select a track from the current playlist (search arguments have no effect here)

`-c` - clears the current playlist before adding a new item

`-C` - control mode, used to control mpd.

## Library Mode
As noted above, library mode is to be used when you want to search through your library to play tracks.

### Search Arguments
`-a` - search by `artist` tag

`-A` - search by `albumartist` tag

`-al`- search by `album` tag

`-g` - search by `genre` tag

`-t` - search by `title` tag

`-[mpd supported tag]` - search by any mpd supported tag. For example, `-comments` will search by the `comments` tag

### Order of Arguments
While mode and search arguments can be added in any order, the order of the search arguments is important
as they are processed in order. For example, if you wanted to search through your library in the flow:

`genre` -> `albumartist` -> `album` -> `title`

You would call `mpdmenu -g -A -al -t`. Any input you give in the view of a previous tag will restrict your
search in the next tag (unless the `[ANY]` option is chosen). If no search arguments are passed, the default flow of 
`mpdmenu -g -A -al` will be used.

## Control Mode
Again, control mode is used to control the connected MPD instance. There are a couple of "modules", you can add the buttons
for these modules to dmenu by using the following arguments.

### Control Arguments
`-prev` - Plays the previous track in the playlist

`-next` - Plays the next track in the playlist

`-toggle` - Toggles play/pause

`-pause` - Pauses MPD

`-play` - Start playing MPD

`-stop` - Stop MPD

`-clear` - Clear the MPD playlist

`-[mpc supported action]` - Will pass the given action directly to mpc. For example, `-crop` will perform `mpc crop`.

If no arguments are given, the `toggle`, `next`, `prev` and `stop` buttons will be added.

To leave the controls menu, simple press escape

### Integration with MPA
`mpdmenu` also supports some integration with my other project, `mpa` (found at github.com/rafaeltheraven/mpa), which is
used to allow more control over playing albums and to queue tracks indefinitely. With `mpa` installed, you can also
add the following controls to the control menu:

`-nextA` - Plays the next album in the playlist

`-prevA` - Plays the previous album in the playlist

`-rand` - Plays a random track from your library

`-randA` - Plays a random album from your library

`-queue` - Continuously queues random tracks from your library

`-queueA` - Continously queues random albums from your library

Of note should be that the queue options will take control of your `mpdmenu` until you quit.

## Requirements
`mpdmenu` makes frequent use of mcp search expression queries. Therefore, you need the following packages:

1. `mpd >= 0.21`

2. `libmpdclient >= 2.16`

3. `mpc >= 0.31`

4. `dmenu`

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
