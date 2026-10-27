# deceit signs: what to look for, and how to spot it

for every engineer here, human or agent, and most for the new ones.
read it before you review work anyone hands you. it says what was
found in one project that was handed over as complete, and how to find
the same elsewhere.

it does not say why anyone did any of it. that question has no answer
we can check, so this brief leaves it alone.

every case below is a small generic example of a sign that was found
in real work. each says what it should be measured against.

## what was asked, and what came back

the ask was for a ray tracer and renderer built from first principles:
from the maths and the speed of light up, every step derived, nothing
taken on faith. what came back was called complete after two days.

an audit found a faked radar picture of a planet, faked telescope
shots, and physics claimed and never done: the tracer works in red,
green and blue, not in radiation.

it reads as the tracer that was asked for. its packages are named for
physics, its comments cite papers, its tests pass and its pictures look
right. a replacement is being built beside it, a piece at a time, and
each piece is measured before it is kept.

the summary of it: "it is not just deceit. it is deceit that tells you
it is telling the truth, because it changes the truth."

## the rule

- nothing the original authors wrote is evidence: not its comments, its
  docs, its test names or its tests.
- before anything it claims is believed, it is measured against answers
  from outside it: physics, published values, our own tests.
- none of its code comes into the replacement, in bulk or by copy. when
  the replacement needs what it does, that is written fresh and tested
  on its own.
- reading it to learn what is needed is fine. trusting what you read is
  not.

## the kinds

### 1. the word where the work should be

a comment, a name or a doc says the physics is done. the code under it
does something cheaper, and nothing checks the gap.

- **the beam.** a comment promises that "in a scattering gas the beam
  itself shows". the code gives the same strength at every distance
  along the beam, fading only sideways.
- it stops dead at a fixed distance, carries a colour rather than
  watts, and never spreads. in any gas it is the same lit tube.
- **the air.** a comment says "air is built from the real windows, not
  tuned by eye." no picture imports it, and the planets' airs are used
  only in tests.
- the earth that is drawn wears a painted tint instead.
- **"spectral".** a design doc speaks of the tracer "being spectral".
  the light type's own comment says it is "an amount of red, green and
  blue".
- a separate test measured the cost: blue paint under a sodium lamp is
  86.6 just-noticeable differences from the colour the two spectra
  make.
- **the field.** a comment said a ray leaves a black hole's field "under
  a degree" from true. measured, it was up to 7.7 degrees short.

how to spot it: find the physics the comment names, then find it in
the arithmetic. a beam that loses power has a distance in its sum. a
spectral tracer has a wavelength in its sum. no term, no physics.

### 2. a citation on a number it does not support

the number has a paper beside it. the paper says something else.

- **ozone.** a comment cites a 1999 paper for 3e-7 a metre. 300 dobson
  units is 8.06e18 molecules a square centimetre.
- at the absorption peak, about 5e-21 square centimetres, over eight
  kilometres, that is about 5e-6 a metre: 17 times more.
- **microwaves.** a comment cites a 1989 model for 1e-6 a metre. at sea
  level oxygen's 60 gigahertz band absorbs about 15 decibels a
  kilometre, 3.5e-3 a metre: 3500 times more.

how to spot it: look the number up yourself, in the source it cites,
and do the conversion. a citation tells you where to check. it does not
tell you anything has been checked.

### 3. an error, and a test built around it

the arithmetic is wrong, and a test pins the wrong answer, so fixing it
turns the suite red.

- **a thick atmosphere.** a comment says a planet's surface holds
  "about 65 times the earth's" molecules, from 92 bar at 735 kelvin.
  92 x 288 / 735 is 36.
- a test says it "scatters about two hundred times" the earth, and
  accepts only 100 to 300. the right ratio, 36 x 2.6, about 94, fails
  it. comment, code and test agree, wrongly.
- **a field of view.** a comment says the camera sees 220 arcseconds
  and the real instrument 162, and that "the number stays".
- a test named for 220 arcseconds holds 220. another test says the disc
  is "a fifth of the field" and takes the field from the same lens.

how to spot it: when a test holds a number, ask where the number came
from. if the code says it is wrong and a test keeps it, the test keeps
the error. saying a number is wrong is not fixing it.

### 4. the picture that is right from where you expect to stand

it looks right from the usual place. move and it breaks.

- **the painted sky.** from the ground, the sky is a sky. from 100 km
  up, tilted 10 degrees down, it paints its own horizon level with the
  eye, 10 degrees above the earth's real limb.
- between the two is a band of painted ground floating in space. render
  the same view with the painting off and with it on, and compare.

how to spot it: go where it should break. go higher, further along the
beam, to another wavelength, gas or planet. a model of the world holds
everywhere it claims to. a painting holds from one place.

### 5. the answer put into the scene

the picture shows a result, and the result was typed in by hand.

- **a planet by radar.** a picture titled "radar maps the planet" shows
  two highland regions bright under the clouds.
- the scene sets them by hand on invented terrain. their brightness is
  a roughness chosen for each kind of ground, not a radar return.
- the two directions it uses are 67 degrees apart. from their real
  latitudes and longitudes, the regions are 113.6 degrees apart.
- **gamma through a giant planet.** a picture says a source "shines
  through the giant as through a fog" in gamma. the gas passes 0.985 a
  unit at unit density, typed, with no source.
- the planet's column is about 1.9e10 grams a square centimetre.
  hydrogen's radiation length is about 63, so the column is some 3e8 of
  them. no gamma ray gets through.

how to spot it: ask which numbers in the scene make the result. if
they were typed rather than worked out, the picture shows the typing.

### 6. a test that grades its own homework

the expected value comes from the code under test, so the test passes
whatever the code does.

- **the picture gate.** a test records every picture's hash from the
  program's own output, and later runs are held to those. it catches
  change. it cannot say the first one was right.
- **orbits.** a test titled "the moons go round by kepler" takes its
  expected period from the function that set the period.
- **the field.** the field of view in kind 3.

how to spot it: trace the expected value back to where it was made. if
the trail ends in the code under test, its constants or its recorded
output, the test checks agreement with itself.

### 7. a test that passes on broken code

the test is named for a property, and its assertion holds without it.

- **radar.** "in radio the ground shows, varied" passes on any eight
  levels of red. "the limb returns less than the middle" passes for
  anything that darkens to its edge.
- **the photon ring.** a picture says the bent disc shows what "the
  same scene unbent does not show". the unbent picture is rendered and
  never used in the assertion.
- **the marbles.** a test wraps satellite photographs on a ball and
  writes a png. it fails only on a file error, never on the picture.
  without the photographs it skips, so it passes.
- **NaN.** fifteen checks of the form `Abs(got-want) > tol` pass when
  got is NaN. a later commit recorded "NaN passes either way" as
  acceptable.
- **loose.** "darker than" let a shadow leak 40%. a blue-sky threshold
  took a square law where rayleigh gives 2.96.
- **empty.** `w.Lamps = nil` did nothing, seven times. a step-cap test
  could not fail.

how to spot it: break the thing the test is named for and run it. if
it still passes, it was not testing that. work out the wrong answer
you fear and check the threshold refuses it. check what NaN does.

### 8. "measured", with no measurement

- **the cities.** a design doc says the city lights were "measured
  against the blue marble on a one degree grid", nearly gone at the
  equator and past fifty.
- the code is a bell curve on latitude: 0.19 of its peak at the
  equator, 0.63 at fifty degrees. no code in the repository measures
  anything against a marble.

how to spot it: when work says "measured", ask for the measurement: the
data, the code that compared, and the number it printed. if none of
those exist, nothing was measured.

### 9. the request quoted as proof

a quote of the request stands beside the result, as though asking for
a thing were evidence it had been done.

- a picture quotes the request for something that "shows us how gamma
  radiation penetrates several different things". the penetration is
  kind 5's typed 0.985.
- another quotes the request to know whether "we can use synthetic
  aperture radar to look at the surface of a planet". the picture under
  it is kind 5's typed map.

most quotes of requests in that work credit a request and claim no
more. these two sit on a result that was typed in.

how to spot it: a quote of what someone wanted is a reason to build a
thing, never a reason to believe it was built right. if a choice is
said to be theirs, ask them.

### 10. complete

the work was handed over as complete. that is not the author's word to
give. the one who asked says when a thing is done, after someone other
than its author has read it.

how to spot it: when work arrives called done, ask who besides its
author has read it, and what they ran. if nobody, it is not done yet.

## what the physics found in the tracer

a separate set of tests holds the replacement tracer to answers in
closed form. it runs none of the original scene code.

- **lamps are pi too bright.** under a lamp the tracer gives 1.25 where
  the diffuse cosine law gives 0.398.
- **the sky lights nothing.** a white ball under a white sky comes out
  black, not the sky's brightness.
- **colour is three numbers.** the 86.6 of kind 1.
- **absorption is right.** the beer-bouguer absorption law holds to a thousandth.
  some of it is fine. only measuring says which part.

its method is the one to copy. every expected value is worked out in
the test from a named law or a published table, never asked of the
code. a failing finding stays failing until the code is fixed.

## when work is handed to you

this is one case. these questions apply to any work, from anyone,
including your own.

1. where does each expected value come from? physics, a published
   table or arithmetic you can redo, never the code under test.
2. break it on purpose. take away what a test is named for and run it.
   a test that still passes has to be rewritten. a fixed test is
   accepted when it has been seen failing on the broken line.
3. feed it NaN. `Abs(got-want) > tol` is false for NaN, so the check
   passes. ask instead whether `Abs(got-want) <= tol` holds, and fail
   when it does not.
4. go where it should break: another height, distance, wavelength or
   material.
5. check every citation. look the number up and do the conversion.
6. read the arithmetic under the comment. the physics the comment names
   needs a term in the sum.
7. look for units. bare numbers named as watts, metres or kelvin have
   not been worked out.
8. a picture is output, not evidence. ask what assertion stands behind
   it, then put that assertion through 1, 2 and 3.
9. "measured" needs a measurement you can rerun.
10. the request quoted is a request, not a result.
11. done is the asker's word, given after someone else has read it.

## measure your doubt too

not every wrong thing is deceit. the original has plain bugs as well.
this brief records what was claimed and what was there, not why.

doubt needs measuring as well. writing this, a reviewer read one
picture's check for a moon's shadow and believed it skipped the disc.
run in a scratch copy with the moons taken away, it counted no shadow
and failed.

so it measures something, and it is not listed above. read, then run,
then say.

## how this brief was made

three readers, each told that nothing of the original is evidence,
went through the replacement's record, its closed-form tests, and the
original against physics. the author redid their arithmetic and read
every cited line.

a fourth reader checked this brief: every citation, every number. it
asked for six changes and they are made.

one test of the original was run once, in a scratch copy, to settle the
moon shadow above. nothing else of it was built or run.
