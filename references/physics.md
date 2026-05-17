# ICSE Class 10 Physics — Conventions for the Study Partner

Read this before running a Physics session.

## Syllabus areas (ICSE Class 10)

- Force, Work, Energy, Power
- Machines (levers, pulleys, mechanical advantage, velocity ratio, efficiency)
- Light (refraction through prisms and lenses, spectrum, dispersion)
- Sound (waves, reflection, resonance, vibrations in air columns)
- Current Electricity (Ohm's law, resistance, household circuits)
- Electromagnetism (electromagnetic induction, transformers, motors)
- Heat (specific heat capacity, latent heat, calorimetry)
- Modern Physics (radioactivity, nuclear changes)

Ingested chapters live under `<workspace>/physics/notes/<chapter-slug>.md`.

## Marking conventions

ICSE Physics expects answers calibrated to mark value:

| Marks | Expected structure |
|---|---|
| 1 | One precise statement (a definition, a value, a single fact) |
| 2 | Two distinct points OR statement + brief explanation |
| 3 | Three distinct points OR statement + explanation + example/diagram |
| 5 | Structured: introduction + body (multiple points) + conclusion/example; a labelled diagram typically counts as 1 of the 5 marks |

For numericals, marks distribute across method: a 3-mark numerical usually breaks as formula (1) + substitution (1) + answer with units (1). Missing units = mark deducted even if the number is right.

## Answer structure templates

### Theory answers

Definition → statement of the law or principle → brief explanation → example or diagram reference.

Example for a 3-mark "State Snell's law and explain it":

1. Statement: "The ratio of sine of angle of incidence to sine of angle of refraction is constant for two given media."
2. Mathematical form: `sin i / sin r = n` (n = refractive index)
3. Brief explanation tying to refraction at a boundary; mention this is constant for a given pair of media.

### Numerical answers — strict structure

Always have the student write numericals in this format:

```
Given:        [list values with units]
To find:      [what's asked]
Formula:      [the equation, written symbolically]
Substitution: [plug in values, with units]
Answer:       [result with units]
```

The closing-protocol marking should explicitly check each step. A correct number without the formula step still loses marks under ICSE marking.

### Diagrams (ray diagrams, circuit diagrams)

ICSE expects diagrams to be labelled, accurate, with arrows indicating direction of light or current. In the skill's text-described mode, the student names: the components, their arrangement, the direction of flow or light, and points of interest (focus, principal axis, image position, etc.).

## Common confusables — fertile for Discrimination mode

- **Speed vs velocity** — scalar vs vector; classic student error is using "speed" when direction matters.
- **Mass vs weight** — kg vs N; mass is invariant, weight changes with g. (Useful Discrimination opener: "weight is measured in kilograms, right?")
- **Heat vs temperature** — heat is energy transferred between bodies; temperature is the measure of average kinetic energy of particles.
- **Reflection vs refraction** — bouncing back at a boundary vs bending through a boundary into a different medium.
- **Concave vs convex** — diverging vs converging — but the mirror and lens conventions differ (concave mirror converges, concave lens diverges). This pair is a goldmine for Discrimination.
- **AC vs DC** — direction changes periodically (50 Hz in India) vs direction constant.
- **Series vs parallel circuits** — same current everywhere, voltage divides vs same voltage across each branch, current divides.
- **Real vs virtual image** — can be projected on a screen, formed by actual ray intersection vs cannot be projected, formed by apparent ray extension behind the mirror or lens.
- **Latent heat of fusion vs vaporisation** — solid↔liquid energy vs liquid↔gas energy; vaporisation always larger.
- **Conductor vs semiconductor vs insulator** — by free electron availability and conductivity range.

## Productive wrongness patterns for Physics

When running Discrimination mode in Physics, use wrongness shapes like:

- **Wrong formula choice**: in a kinematics problem that gives initial velocity, final velocity, and distance, offer `v = u + at` (needs time) when the correct one is `v² = u² + 2as`.
- **Wrong unit**: state energy in newtons or force in joules. Student should catch this immediately.
- **Missed conversion**: leave a quantity in cm when SI requires metres; use minutes instead of seconds.
- **Wrong sign convention**: in a ray diagram, get the sign of focal length wrong for a concave lens.
- **Confused law application**: apply Ohm's law where Joule's law of heating fits better.
- **Real-vs-virtual misclassification**: claim a convex mirror produces a real image (it doesn't, for any object position).

Avoid random wrongness — "the answer is 47" with no relation to the problem trains nothing.

## Mode-specific guidance

**Elaboration mode** — the standard mode. Student writes theory or numerical answers; AI marks against the templates above. For numericals, always tell the student to use the Given/To find/Formula/Substitution/Answer structure.

**Discrimination mode** — most powerful for theory. For numericals, the productive wrongness is usually wrong-formula or wrong-unit, not a wrong number from nowhere. Force the student to articulate *why* the suggested formula is wrong in this specific problem.

**Spaced retrieval mode** — confusable pairs (concave/convex sign conventions, AC/DC, latent heats) decay fast. If log.md shows a low confidence on any of these, surface them within 2–3 days.
