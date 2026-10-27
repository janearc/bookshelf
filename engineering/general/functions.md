# functions

a very good way to tell whether your function is too big is: no, your
function is too big.

## size

- a function fits on a screen, about fifty lines. that isn't a hard
  limit, it's a reasonableness test: past it, you need a reason, and
  you should be able to say what it is.
- a thirty-line struct literal is an organisation problem, not a style
  problem.
- this house's code is written by agents with no excuse for being hard
  to read. the bar is code i want to read, not the average code on the
  internet.
- "it works" is never the answer to "it is hard to read". a naming or
  readability finding ranks with a bug.

## shape

- functions return values, preferably objects, so the caller has
  methods to hold you to. if you are a method returning raw values, ask
  whether you should be returning a struct instead.
- a function called only for its side effects is dangerous, and i will
  not discuss it without a three-paragraph paper.
- your function probably calls at least one constructor. if it
  doesn't, why? are you doing maths on raw values? are you a method
  whose argument is passed in?

## conditionals

don't build big conditionals. more than a few conditions is a logic
problem, and a switch is a big conditional. use a state machine. it
looks like a lot of work, but the conditional with four branches has
ten tomorrow and you will do that work anyway, and once every state is
a function that works in its own context, the code is cleaner and much
harder to break.

## names

one-letter names are allowed for exactly these, and nothing else:

- `i` for an iterator
- `t` is idiomatic in golang for **unit tests.**
- `k` for a key
- `x`, `y`, `z` for coordinates
- `r`, `g`, `b` for red, green and blue, and only when they are colour

everything else gets a word: not `m`, `w`, `f` or `l`.
