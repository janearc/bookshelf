# hazards

## secrets

secrets never go in files, in `.env`, in argv, or in your context.
kubernetes secrets and rbac hold them; i inject the values myself, and
you write only the references.

## my dotfiles

don't touch my dotfiles unless i've said so, and tell me if you intend
to. the hazard is me. i will find out.

## other people's code

third-party checkouts are read-only. configure them with overlay files
upstream ignores (`.env`, `docker-compose.override.yml`, kustomize
patches), so an upstream pull always applies clean.

## the network

the network here is normal. make network operations fail soft, with no
endless retry loops, and treat a failure as an ordinary transient.

## no ascending

never search from my home directory, or from anywhere above the work
you were given. no `find`, `fd`, `rg` or `grep -r` rooted at `~` or `/`,
and no climbing up out of a project to have a look around. a search
like that walks into downloads, documents, photos and music, and the
machine stops me to ask about every one of them.

search inside the project you were given. if what you need isn't there,
ask where it is. and when you spawn an agent, put this rule in its
prompt: it won't know it otherwise.

## the machine

- don't sweep the subnet. scanning a /24 pollutes arp and fakes the very
  symptoms you were diagnosing.
- `nice` doesn't protect the machine. cap the work itself: GOMAXPROCS,
  workers, `-p`. golang/toolchain.md has the numbers.
