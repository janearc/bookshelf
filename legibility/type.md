# type

## sizes and spacing

- body text is 24px at weight 400. not heavier: light text on a dark
  ground blooms, so it reads heavier than it is and the counters fill
  in. the fix is lighter, not bolder; i rated 500 worse than 400 at the
  same size.
- prose line-height is 1.75. table cells get a real line-height too:
  `normal` is about 1.2, the densest thing on any page with rows.
- letter-spacing about .015em. i rated zero as cramped and .22em as
  unreadable; both extremes are wrong.
- nothing below 16px, anywhere.

## three taxes

all-caps, wide tracking and monospace each cost legibility. don't stack
them, and prefer none. a census on 2026-09-03 found 1,106 all-caps runs
across eleven surfaces, every one also letter-spaced, and 823 of them
also monospace, at a median of 17px.

- all-caps removes word shape, the profile of ascenders and descenders a
  reader navigates by, and forces letter-by-letter reading. use sentence
  case for anything a person reads. a one-word status chip is the only
  defensible exception, and it isn't worth taking.
- tracking above about .05em stops a word being a unit.
- monospace for prose removes the silhouette that tells words apart.
  keep it for ids, hashes, paths, timestamps and code, which are read
  character by character and benefit from it.

## the reader's own settings

- ligatures off: `font-variant-ligatures: none`. fi, fl and ffi are
  drawn as one glyph by default, which deletes the boundary between
  letters. that's a nicety in print and actively harmful to a reader
  fighting crowding.
- size in `rem`, not `px`, so a browser or system text-size setting
  actually reaches the page. a hard-coded px silently overrides it.
- respond to `prefers-reduced-transparency` and `prefers-contrast`.
  macos, gnome and windows all let a person say once what they need. a
  surface that ignores that is choosing to.
