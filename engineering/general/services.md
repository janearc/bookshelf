# services

a service exposes:

- `/health`
- `/metrics`
- `/api`

and is built with:

- structured json logging
- context passed through the whole stack
- no state of its own: state lives outside it
- idempotent mutations
- aggressive timeouts on every operation, all of them
- backoff with jitter
- circuit breaking
- the smallest implementation that meets every requirement in the
  design

## failing open or closed

failing closed is generally best, but some services have to fail open
and report a degraded status. decide which way yours fails, and why,
and write it down. you'll know where, because it's the first place
someone looks when the thing you are doing right now fails. help that
person.

if you aren't sure which to use, ask the maintainer.

flipr is the example. its `/health` answers 200 when it is degraded,
on purpose, and its OPERATION.md says why and what to do about it. a
200 that was decided and written down is a design. a 200 that is there
so the check goes green is the thing praxis.md calls appalling. because it is
appalling.
