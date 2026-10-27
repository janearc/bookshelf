# golang style

## guard your objects

an exported type is a design decision, and so is every exported method.
if a private type with public methods will do, use it: it's safer.
nobody can use your object without your permission, and when you've
forgotten about it tomorrow, nobody can reach in and do something you
didn't design for. keep the members private too, and give callers a
method for each thing they need from you, and nothing else.

be the most defensive programmer you can be. people say this makes
golang hard to use, and they are right. but it should be harder to use
golang than to get fired. guard. your. objects.

```go
// a nebula is private and so are its members; it composes types that
// belong to other packages, each the canonical source of what it holds.
type nebula struct {
	dimensions  geom.Coords
	location    set.Location
	composition gases.DensityMap
	turbulence  gases.Turbulence
	temperature gases.Temperature
	vector      math.Vec
}
```

## structs in, one thing out

- functions take structs, not primitives. a struct is the place you
  combine things from other packages.
- return one value, not a composite: `return thing`.

## constructors

- your package has a public constructor for its callers and a private
  one it uses itself.
- the public constructor is the door person. it checks the arguments,
  validates each step, and does everything that isn't creating the
  object, then calls the private constructor.
- the private constructor gets a stress-free life: once someone is in,
  it serves them a drink.
