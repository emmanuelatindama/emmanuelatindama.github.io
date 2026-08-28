---
layout: page
title: Exploring Mechanics
description: An interactive, mathematics-first path through classical mechanics, from Newton's laws to gyroscopes and chaos.
img: assets/img/exploring-mechanics.png
importance: 2
category: work
github: https://github.com/emmanuelatindama/exploring-mechanics
_styles: >
  .em-lede p {
    font-size: 1.05rem;
  }
  .em-lede em {
    font-style: normal;
    font-weight: 600;
    color: var(--global-text-color);
  }
  .em-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1rem;
    margin: 2rem 0 1rem;
  }
  .em-card {
    background-color: var(--global-card-bg-color);
    border: 1px solid var(--global-divider-color);
    border-radius: 8px;
    padding: 1.1rem 1.25rem;
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
  }
  .em-card h3 {
    margin: 0;
    font-size: 1.05rem;
    font-weight: 600;
    color: var(--global-text-color);
  }
  .em-card p {
    margin: 0;
    color: var(--global-text-color-light);
  }
  /* The link closes the card, so the eye lands on it after the hook. It is
     underlined rather than colour-only, and pushed to the bottom so cards of
     unequal text length still line their calls-to-action up. */
  .em-card a.em-go {
    margin-top: auto;
    align-self: flex-start;
    font-weight: 600;
    text-decoration: underline;
    text-underline-offset: 2px;
  }
  .em-soon {
    margin-top: 2rem;
    padding-top: 1rem;
    border-top: 1px solid var(--global-divider-color);
    color: var(--global-text-color-light);
    font-size: 0.95rem;
  }
---

<div class="em-lede" markdown="1">

Mechanics has a reputation for being the physics you already know: things fall,
things push back, things spin. Most of that intuition holds up for a block on a
table. It stops holding up almost immediately once forces interact — a cone
that rolls <em>uphill</em>, a pulley that halves your force and doubles your
work, a spinning wheel that turns sideways instead of falling, a curve that
gets a bead downhill faster than the straight line between two points.

Each section below is one stretch of that path, building from vectors and
Newton's laws up through energy, momentum, machines, rotation, oscillation, and
a set of problems built specifically to break the intuition the earlier
sections just built. Every page starts with a prediction before it shows you
the answer.

</div>

<div class="em-grid">

  <div class="em-card">
    <h3>0. The toolkit</h3>
    <p>
      Vectors, units, coordinate systems, reference frames, free-body diagrams —
      the vocabulary everything after this section assumes you already have.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/00-toolkit/' | relative_url }}">Check out the toolkit →</a>
  </div>

  <div class="em-card">
    <h3>1. Kinematics</h3>
    <p>
      Position, velocity, and acceleration, described without yet asking what
      causes them — constant velocity, free fall, and projectile motion, up
      through relative motion between moving observers.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/01-kinematics/' | relative_url }}">Check out kinematics →</a>
  </div>

  <div class="em-card">
    <h3>2. Newton's laws</h3>
    <p>
      Inertia, F = ma, and action-reaction pairs that don't cancel because they
      act on different objects — then friction, inclines, and connected objects
      as the first place the laws get genuinely hard to apply.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/02-newtons-laws/' | relative_url }}">Check out Newton's laws →</a>
  </div>

  <div class="em-card">
    <h3>3. Work, energy, and power</h3>
    <p>
      A shortcut around messy force diagrams: track energy instead of force,
      and problems like roller coasters and pendulums stop needing calculus to
      solve.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/03-energy/' | relative_url }}">Check out energy and power →</a>
  </div>

  <div class="em-card">
    <h3>4. Momentum, impulse, and collisions</h3>
    <p>
      What survives a collision that energy doesn't. A ballistic pendulum
      solves in two stages — momentum during the crash, energy after it —
      because no single conservation law covers the whole event.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/04-momentum/' | relative_url }}">Check out momentum and collisions →</a>
  </div>

  <div class="em-card">
    <h3>5. Constraints and simple machines</h3>
    <p>
      Levers, pulleys, screws, and gears all make the same trade: less force
      for more distance, never both. A movable pulley that halves your lifting
      force doubles how far you have to pull the rope — no exceptions.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/05-simple-machines/' | relative_url }}">Check out simple machines →</a>
  </div>

  <div class="em-card">
    <h3>6. Circular motion and gravitation</h3>
    <p>
      The force that keeps something moving in a circle points inward, not
      outward — "centrifugal force" is what it feels like from inside a
      rotating frame, not what's actually happening in an inertial one.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/06-circular-motion/' | relative_url }}">Check out circular motion →</a>
  </div>

  <div class="em-card">
    <h3>7. Rotational mechanics and rolling</h3>
    <p>
      Newton's laws again, but spinning: torque instead of force, moment of
      inertia instead of mass. A hoop, disk, and sphere released from the same
      height down the same ramp do not arrive together.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/07-rotation-and-rolling/' | relative_url }}">Check out rotation and rolling →</a>
  </div>

  <div class="em-card">
    <h3>8. Oscillations, resonance, and chaos</h3>
    <p>
      Simple harmonic motion repeats forever right up until damping or a
      second coupled pendulum enters the picture — then two nearly identical
      starting angles diverge into completely different futures.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/08-oscillations/' | relative_url }}">Check out oscillations and chaos →</a>
  </div>

  <div class="em-card">
    <h3>9. Counterintuitive mechanics problems</h3>
    <p>
      A double cone that appears to roll uphill, a chain that fountains above
      the container it falls from, a straight line that loses a race to a
      curve. Predict the outcome before you read the resolution.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/09-unintuitive-problems/' | relative_url }}">Check out the unintuitive problems →</a>
  </div>

  <div class="em-card">
    <h3>10. Real-world capstones</h3>
    <p>
      Bowling, bicycles, roller coasters, bridges, bows, and catapults, each
      built up in stages from the sections above — the payoff for having
      learned the individual pieces first.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/10-capstones/' | relative_url }}">Check out the capstones →</a>
  </div>

</div>

<div class="em-soon" markdown="1">

This project is under active construction — each section currently outlines
its subtopics, with full derivations and interactive simulations landing
incrementally. Follow along on [GitHub](https://github.com/emmanuelatindama/exploring-mechanics).

</div>
