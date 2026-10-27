# layout

## tables truncate, they don't wrap

an ellipsis costs the tail of a string nobody reads. a wrapped
200-character url turns one row into six and destroys the horizontal
rhythm the eye uses to scan the column below it. the browser shows a
link's full target on hover, and a cell can carry a `title`. a cell
that really is prose opts back in, by name.

## columns

`overflow-wrap: anywhere` also shrinks a column below its longest
word, so identifiers get squeezed and broken mid-token, and a name
split across two lines doesn't read as one name that wrapped. use
`break-word`, which still rescues a long url without collapsing the
column.
