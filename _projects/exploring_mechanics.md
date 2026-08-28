---
layout: page
title: Exploring Mechanics
description: Interactive simulations of physical systems, mechanical principles, and dynamical behavior.
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

The physical world follows rules, but intuition about those rules breaks down
when variables interact. Friction and inertia seem simple until you pair them
with angles. Oscillators seem predictable until you couple them. Fluids seem
passive until you watch them self-organize into vortices and patterns.

Real mechanisms reveal their secrets through simulation: watch what happens when
you change a single parameter. Most systems hide their behavior until you build
them. Each exploration below is one place where the map and the territory
diverge — where equations hide counterintuitive dynamics that only emerge when
you <em>see</em> the motion. They are simulated live in your browser, so you can
adjust the forces and watch how the system responds.

</div>

<div class="em-grid">

  <div class="em-card">
    <h3>Pendulum at large angles</h3>
    <p>
      Small-angle approximation works well for shallow swings, but release a
      pendulum from near-horizontal and the period jumps. The small-angle
      assumption that makes teaching easy vanishes once you actually let it
      swing.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/#pendulum' | relative_url }}">Explore the pendulum →</a>
  </div>

  <div class="em-card">
    <h3>Coupled oscillators and resonance</h3>
    <p>
      Two pendulums coupled by a spring trade energy back and forth. Adjust the
      coupling strength or drive one at the right frequency, and the whole
      system responds with amplitudes that seem to come from nowhere.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/#coupled-oscillators' | relative_url }}">Explore coupled oscillators →</a>
  </div>

  <div class="em-card">
    <h3>Friction and sliding angles</h3>
    <p>
      A block on an incline either stays put or slides, but the threshold
      depends on static versus kinetic friction — two different numbers nobody
      thinks about. Watch the stick-slip transition as you tilt the plane.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/#friction' | relative_url }}">Explore friction →</a>
  </div>

  <div class="em-card">
    <h3>Rolling vs. sliding motion</h3>
    <p>
      A sphere rolled down one ramp and slid down another will split, even
      though both start at the same height. Rolling dissipates energy into
      rotational motion — a fact that lives in the moment of inertia, not the
      height.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/#rolling' | relative_url }}">Explore rolling motion →</a>
  </div>

  <div class="em-card">
    <h3>Centripetal force and banking</h3>
    <p>
      Cars on banked curves feel different forces depending on speed. Too slow
      and friction points uphill; too fast and it points downhill. There is one
      speed where friction doesn't matter at all.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/#banking' | relative_url }}">Explore centripetal force →</a>
  </div>

  <div class="em-card">
    <h3>Fluid drag and terminal velocity</h3>
    <p>
      Things falling through air accelerate until drag matches weight, then move
      at constant speed. Heavier or larger objects reach different terminal
      velocities — a race where both the rules and the answer flip with shape.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/#drag' | relative_url }}">Explore drag and terminal velocity →</a>
  </div>

  <div class="em-card">
    <h3>Double pendulum chaos</h3>
    <p>
      A pendulum hanging from another pendulum looks chaotic, and it is —
      sensitive to starting position in a way single pendulums are not. Tiny
      differences in initial angle lead to wildly different futures.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/#double-pendulum' | relative_url }}">Explore the double pendulum →</a>
  </div>

  <div class="em-card">
    <h3>Moment of inertia shapes</h3>
    <p>
      A ring and a disk with the same mass and radius behave differently when
      spun — the ring's mass sits farther from the axis, so it takes more
      torque to speed up. Distribution matters more than total mass.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/#inertia' | relative_url }}">Explore moment of inertia →</a>
  </div>

  <div class="em-card">
    <h3>Projectile motion and air resistance</h3>
    <p>
      The parabolic arc you learned about is only true in a vacuum. Add air
      resistance and the trajectory compresses, the landing spot moves closer,
      and the optimal angle stops being 45°.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/#projectile' | relative_url }}">Explore projectile motion →</a>
  </div>

  <div class="em-card">
    <h3>Gyroscopic precession</h3>
    <p>
      Spin a wheel and try to tip it sideways — instead of falling, it turns.
      Gravity applies torque perpendicular to the spin, and the result is motion
      that seems to ignore the force entirely.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/#gyroscope' | relative_url }}">Explore gyroscopic precession →</a>
  </div>

  <div class="em-card">
    <h3>Spring-mass systems and energy</h3>
    <p>
      Compression and extension trade places in a spring-mass system. The mass
      oscillates, and at different points in the cycle, all the energy is
      kinetic, all is potential, or shared between them.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/#spring-mass' | relative_url }}">Explore spring-mass systems →</a>
  </div>

  <div class="em-card">
    <h3>Damping and energy loss</h3>
    <p>
      Real oscillators have friction or air resistance, and energy bleeds away.
      Adjust the damping and watch the system go from bouncy to overdamped —
      critical damping sits precisely between them.
    </p>
    <a class="em-go" href="{{ '/exploring-mechanics/#damping' | relative_url }}">Explore damping →</a>
  </div>

</div>

<div class="em-soon" markdown="1">

More simulations coming soon. If you'd like to explore a particular mechanism or
system, [get in touch](mailto:emmanuel.atindama@bms.com).

</div>
