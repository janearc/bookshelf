# reviews

the writer is not the reviewer. done is something someone else says.

## the flow

- branch, small commits, push, PR. never push straight to main.
- a review is a comment on the PR, from a session other than the one
  that wrote it. it names the session and says either accepted or what
  must change.
- on acceptance, the writing session merges to the target branch itself
  and checks the result.
- don't sit idle waiting for a review. put the diff up and move on to
  the next thing.

## what needs me

my sign-off is needed for:
- a contract change
- spending money
- something that moves in the physical world
- changes to a host

if it isn't in this list, it doesn't need me. i believe in you. we can revert
if something breaks. that's why we use revision control and `game`.

## before it reaches me

- never ask me to run code that another session hasn't reviewed. 
- `game` has no small changes. anything touching it is tested the way i
  use it and reviewed before it merges.
- the fold loop:
    - the maintainer and the lead agent plan and design
    - agents do much of the coding
    - one agent specializes in golang work and porting to golang
    - a reviewer does a maturity and correctness review
    - a different reviewer does a deceit review

if something has passed a correctness/maturity review and a deceit review, it
can be sent to me for a sign-off, but the lead agent can probably approve landing on
main if it has these reviews.

## fanning out

- set the effort on every agent you spawn; an agent inherits yours
  otherwise.
- use the cheapest model that can do the job and size the fleet to the
  code. the shape that works: one cheap reviewer per file, a few
  middling ones reading across areas, and one more expensive pass that
  tries to break what they found.
- don't send more than 4 sub-agents out at once.

## writing findings

a review records findings, one line each: `file:line`, what, and why.
it doesn't rewrite the code; the fixes are asked of the writer before
the next push.
