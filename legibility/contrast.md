# contrast

## the band: 10:1 to 12.5:1, centred on 11:1

this is the part that isn't wcag, and the part everyone gets wrong.
wcag 2.1 aa sets a floor of 4.5:1 and says nothing about a ceiling,
because it was written for readers who can't get enough contrast. i
have a ceiling as well: 13:1 reads as glare, and 16.4:1, which every
theme i had shipped until that day used, is painful and smears. under
10:1 is too dim to follow at length.

so prose lives in a band, and ink and dim end up close together. that
is correct. a band that narrow has no room for three brightness levels,
so hierarchy comes from size and weight instead, which is sturdier
anyway.

state chips are the exception. they're scanned, not read, so they sit
around 8:1; forcing them into the band breaks the state vocabulary for
no gain.

## contrast ratio is blind to hue

that's a real gap. a colour on a tint of its own hue can score 5:1 and
still be unreadable, because there's an edge in brightness and none in
colour. i measured an amber chip one degree of hue from its own fill,
and a red one twenty-four degrees away, and every one passed the
contrast test. red is the worst case: the eye focuses long wavelengths
least sharply, so a red-on-red edge is blurrier at the same ratio.

so text needs a background that differs in more than brightness:
either at least 40 degrees of hue apart, or a background desaturated
below about 0.35, so the ink's own colour carries the edge. chip fills
are neutral; a chip's meaning lives in its ink and its border.
