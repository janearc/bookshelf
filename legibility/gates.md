# gates

anything that renders text for a person is checked by these gates. a
project without them is not exempt; it is unmeasured.

- hold every prose colour to the band (contrast.md), on every surface
  the stylesheet composites, not just the page ground and the card. a
  gate that checks the two surfaces that are easy to name is how
  unreadable text ships with a green build. that happened to me, on the
  day the gate was written.
- hold state chips to their own level, about 8:1.
- enforce the hue rule in the same place.
- measure what is rendered, in a browser. it's the only thing that
  catches a page's own inline styles, which is where every survivor
  hides.
- copy the reference implementations rather than reinventing the
  arithmetic: `internal/bench/contrast_test.go` in gaggle and
  `src/contrast.test.ts` in dodo.

## when a gate fails

the colour changes, not the threshold. if a theme can't express itself
inside the band, the theme is asking for text nobody can read, and the
answer is a different colour. do not widen the band, do not add an
exemption, do not skip the test. if you genuinely believe a number here
is wrong, say so to me and bring a measurement.
