# testing

## unit tests

unit testing is a complete sentence.

- write them first: design doc, then the function signatures, then the
  unit tests, then the functions.
- test the design doc before the code. a test the design asks for
  belongs there even if it adds nothing to coverage, because coverage is
  incidental. if the design says a field is text, test that it's text,
  and still check that it isn't a 300gb tiff.
- if coverage is under 90%, i will ask you why, and you should have an
  answer you think i will understand.
- you are most welcome to tell me something isn't ready because you
  were busy writing unit tests.

## why the test comes before any code

a test written after the code tests what the code does. a test written
before it tests what the code is supposed to do; a test written before you
write code is a contract with yourself to make sure that you are staying
honest to the intent of the design. the gap between these two is where bugs
live.

- once the code exists, it is the easiest spec to read, so the test
  copies it. a backwards condition gets a test that agrees with it.
- a test written first has to fail first. that is the only proof that
  it can fail at all. a test that has never been red proves only that the
  test has lived a comfortable life and has never really been useful.
- the test is the first caller of the function. if it is awkward to
  write, the signature is wrong, and that is cheap to fix before the
  function exists and expensive after.
- before there is code you are thinking about the requirement, so the
  anti-tests come naturally: what must this refuse, and what must it
  leave alone. after the code, you think about the code you wrote.
  - this means when you write your tests, also write your anti-tests. if it
    seems like a lot of work to write two tests and your function definition
    before you actually write your function, think about how much work that's
    going to be when this is a 7kloc diff that won't pass the bar for
    release.

## anti-tests

a test says what the code must do. an anti-test says what it must not
do: the input that looks close enough to fool it, the key it should
leave alone, the case it should refuse. the bar asks for one anti-test
for every test.

a test alone can pass with the condition backwards. this went through
game's config reader until mutants found it:

```go
    if key == "checks" || !strings.ContainsAny(said, " \t") {
        checks, _ = strconv.Atoi(said)
    }
```

the `||` should be `&&`. as written, any key with a one-word value is
read as a count of checks. the test fed it "checks 3" and passed with
either operator. the anti-test is the one that tells them apart:

```go
func TestChecksCountsChecks(t *testing.T) {
    if got := checksFrom("checks 3"); got != 3 {
        t.Fatalf("checks 3 read as %d, want 3", got)
    }
}

func TestChecksLeavesOtherKeysAlone(t *testing.T) {
    if got := checksFrom("name foo"); got != 0 {
        t.Fatalf("name foo read as %d checks, want 0", got)
    }
}
```

write the anti-test with the test, not after mutants find the gap.

## mocks, not fakes

a fake is a stand-in written by hand that gives canned answers. it
passes whether the code calls it, calls it with the wrong arguments, or
never calls it at all:

```go
type fakeRunner struct{}

func (fakeRunner) Run(name string, args ...string) ([]byte, error) {
    return pieHeader, nil
}
```

a mock is *generated with mockgen and carries expectations.* it fails
the test when the call it expects is not made, or is made differently:

```go
runner := NewMockRunner(ctrl)
runner.EXPECT().Run("otool", "-hv", "bin/game").Return(pieHeader, nil)
```

with the fake, a hardening check that never runs otool, or runs it on
the wrong binary, still passes. with the mock, it fails. use mocks.

## smoke tests

- a product (as opposed to a service or a daemon) has smoke tests:
  every significant feature has at least one.
- smokes run before any branch is done. anything that renders runs its
  smokes through slayer's render queue, never on
  the machine directly.
- if you have fewer smoke tests than unit tests, why?

## mutation tests

mutation tests have caught a lot of bugs here before they became
problems. in a project past twenty commits i expect a second set of
tests whose only job is to catch insufficient unit tests: change the
code on purpose and make sure something fails.

they don't move coverage at all, *which is why coverage is a bad metric.*
nobody in the history of software, except the person writing it, has ever
complained about too much testing. if you have meaty little fingers, it's okay
to complain about writing unit tests. but you still have to do them. if you do
not have meaty little fingers, and you are complaining about unit tests, why?

## a test that passes for the wrong reason

a check that passes without proving anything is worse than no check,
because now everyone trusts it. this is 'return 200' in a test, and it
is just as appalling.

- never loosen a bound, skip a test, or point a check at something
  easier so that it goes green. if the thing you changed really does
  change what the test sees, say what changed and why in the commit,
  and show that the check still fails when the feature breaks.
- a check is done when it fails for the right reason. break the feature
  on purpose, watch the check fail, put the feature back.
- a check that cannot run fails. it never skips and passes.
- the one who writes the code does not get to move the measure. if
  your change needs a threshold to change, someone else agrees to it
  first.
