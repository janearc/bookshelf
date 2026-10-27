# golang toolchain

## the machine is shared

- an agent's go work runs with `GOMAXPROCS=4` and `go test -p 2`: one
  heavy process at a time, never the whole machine.
- renders, smokes and picture gates go through slayer's render queue,
  not your shell.
- anything that will run at full load for long, ask first and say how
  long. if i seem to be asking for hours of it, i have probably made
  a mistake; check with me.

## commands

- in the render repositories, which point at each other with
  `replace`, run go commands with `GOWORK=off`.
- never pipe `go test`, or any gate, through `grep` in a chain: the pipe
  throws away the exit code. write the output to a file, keep the exit
  code, then read the file:
  `go test ./... > test.out 2>&1; status=$?`
- a `.go` file lives inside a module tree, never in a bare scratch
  directory, or the language server reports it under every message i
  read.
- build, lint and release through `game` (general/building.md).
