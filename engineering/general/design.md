# design

design lessons for engineers who do not want their boss to get fired.

## bottom up, inside out

when you build a package or change one, start from the deepest
generalisation of the thing you can make without exposing more layers
than you have to. those are called primitives, and the thing you
actually wanted is a composition of them.

- not a zeppelin, a vehicle: it has volume, shape, buoyancy, mass.
- not saturn, a gravitating body: it has composition, mass, spin,
  eccentricity, a vector.
- not a camera, a sensor: it has a band, a sensitivity, media, a lens,
  a vector.
- not a colour, a swatch: it has a wavelength, a band.
- not a light, an emitter: it has a band, a power, a dispersion.

build the smallest thing you can, and compose the thing you want from
smaller things.

- not `func NewVolvo() Volvo`, but `func NewVehicle(kind VehKind,
  temp VehTemp, at vec) vehicle`.
- not `func CrabNebula(loc []float64, material string, dens float64)
  Nebula`. the crab nebula is a nebula with particular values, and the
  values live in a file, not in a constructor. golang/style.md shows
  the nebula done right.

## who owns what

- almost never should a location just be an xyz. it belongs to a
  package whose job is location: one that does the maths for you and
  makes sure everyone behaves.
- if you reach for a lookup table inside your package, the thing you are
  looking up is probably big enough to be its own package somewhere.
  yes, really. golang makes this hard because it makes you think harder
  about how your code is structured. so think more, and then write the
  thing you want to write.
- an attribute like density is probably not yours to handle. you are not
  its canonical source. trust the package that is, and use the methods
  it gives you, so you don't have to write them yourself. at all times,
  look for someone else to do the maths, so you don't get caught doing
  it wrong.

## no magic numbers

a number written in code is a claim, and a bare one says nothing about where
it came from or what it is in. we don't hard code things like this. every
number is one of three things:
  - a measured constant: of nature, of the sun, of the universe. it is named
    once, in one place, with its unit and the published source it came from.
  - derived: worked out in code from the named constants, so it moves when
    they do. if it can be derived, it is. the sun's temperature follows from
    its brightness and its radius; nobody writes 5772.
  - measured across many things and not derivable: read from a published
    table, loaded as data, and cited. a fit's coefficients copied into a
    function are a table somebody threw away.

if you can't say which of the three your number is, you don't know what it
is yet.
