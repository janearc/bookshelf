# building

## don't build it by hand

firstly, don't. if there's a package you can use or a published image,
try that first. this doesn't mean arguing with me when i've said i need
a routing engine, but it does mean you should understand why we aren't
using the routing engines on the market. ask me. i really like that
question.

## game

every project here builds, lints, releases and publishes through
`game`, and only through `game`.

- `road` and `dist` are the canonical trees. assume road is dirty;
  dist is maintained. if dist goes anywhere other than this machine,
  know whether you are allowed to push it there before you do.
- an agent keeps its trees in its own home and points `GAME_HOME` at
  it, so game reads that config and not the shell's. a `~` inside it
  still means this machine's user, so shared roads resolve. never fake
  `HOME`: it moves the ssh keys and the gh credentials with it.
- cut from a current tree. `game release` doesn't yet compare your
  checkout to its road, so a tag cut from a stale one publishes a false
  claim. pull first.
- a binary with no provenance cuts nothing. `bootstrap.sh` and `game
  build` stamp the commit; a hand-typed `go build` doesn't, and the
  release verbs refuse it.
- if someone asks you to roll up a branch to hand to someone else, find
  out what they're doing with it first.
