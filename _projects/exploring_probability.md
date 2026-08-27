---
layout: page
title: Exploring Probability
description: Interactive simulations of games where the average outcome and the typical outcome disagree.
img: assets/img/exploring-probability.png
importance: 1
category: work
github: https://github.com/emmanuelatindama/exploring-probability
_styles: >
  .ep-lede p {
    font-size: 1.05rem;
  }
  .ep-lede em {
    font-style: normal;
    font-weight: 600;
    color: var(--global-text-color);
  }
  .ep-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1rem;
    margin: 2rem 0 1rem;
  }
  .ep-card {
    background-color: var(--global-card-bg-color);
    border: 1px solid var(--global-divider-color);
    border-radius: 8px;
    padding: 1.1rem 1.25rem;
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
  }
  .ep-card h3 {
    margin: 0;
    font-size: 1.05rem;
    font-weight: 600;
    color: var(--global-text-color);
  }
  .ep-card p {
    margin: 0;
    color: var(--global-text-color-light);
  }
  /* The link closes the card, so the eye lands on it after the hook. It is
     underlined rather than colour-only, and pushed to the bottom so cards of
     unequal text length still line their calls-to-action up. */
  .ep-card a.ep-go {
    margin-top: auto;
    align-self: flex-start;
    font-weight: 600;
    text-decoration: underline;
    text-underline-offset: 2px;
  }
  .ep-soon {
    margin-top: 2rem;
    padding-top: 1rem;
    border-top: 1px solid var(--global-divider-color);
    color: var(--global-text-color-light);
    font-size: 0.95rem;
  }
---

<div class="ep-lede" markdown="1">

Ask what a gamble is worth and you will usually be handed one number: the
average. It is a good number. It is also a summary of something much larger — a
whole distribution of futures, most of which you will never see — and summaries
leak. An average assumes the outcomes add up: that the good years and the bad
years sit side by side and cancel. Real games rarely oblige. Outcomes
<em>multiply</em>, so one bad round scales everything that comes after it.
Losses <em>absorb</em>, so \$0 is a place you can arrive at but never leave.
Tails run off toward <em>infinity</em>, so the average ends up carried entirely
by outcomes that will never actually happen to you.

When any of that is true, the average stops describing anybody. The typical
player and the average player part company, and the gap between them is where
the interesting mathematics lives — and where most bad financial decisions get
made. Each game below is one place that gap opens up. They are simulated live
in your browser, so you can push the numbers around and watch the gap open and
close yourself.

</div>

<div class="ep-grid">

  <div class="ep-card">
    <h3>Too good to be true</h3>
    <p>
      Heads pays +50%, tails costs 40% — that's +5% a round forever, in
      expectation. Play it yourself and you go broke almost surely. Both are
      true at once, and reconciling them is the whole subject.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#ergodic-coin' | relative_url }}">Check out the ergodic coin flip →</a>
  </div>

  <div class="ep-card">
    <h3>How much to bet</h3>
    <p>
      With the odds fixed, bet size alone decides whether you finish ahead or
      broke. Bet too little and you barely grow; too much and swings wipe you
      out. The right size is a formula, not a feeling.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#kelly' | relative_url }}">Check out Kelly bet sizing →</a>
  </div>

  <div class="ep-card">
    <h3>Nearly fair is not fair</h3>
    <p>
      With $100 against a house with millions, even a nearly fair coin ruins
      you almost certainly — and a perfectly fair one ruins you with
      certainty. Against a losing edge, betting bigger is safer than betting
      small.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#gamblers-ruin' | relative_url }}">Check out gambler's ruin →</a>
  </div>

  <div class="ep-card">
    <h3>A ticket worth infinity</h3>
    <p>
      A coin is tossed until it lands tails, doubling the pot each time it
      doesn't. The expected payout is infinite, yet almost nobody would pay
      more than a few dollars — and they're right not to.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#st-petersburg' | relative_url }}">Check out the St Petersburg paradox →</a>
  </div>

  <div class="ep-card">
    <h3>Winning by never winning</h3>
    <p>
      Betraying beats cooperating no matter what the other player does, so
      both betray and both lose. Play it hundreds of times against every
      strategy imaginable, and the winner is four lines long — and never once
      outscores an opponent.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#prisoners-dilemma' | relative_url }}">Check out the iterated prisoner's dilemma →</a>
  </div>

  <div class="ep-card">
    <h3>Should you switch?</h3>
    <p>
      Three doors, one prize; the host, who knows where it is, opens a goat
      and offers a switch. It looks like fifty-fifty. It isn't: switching
      wins two times out of three, and thousands of readers refused to
      believe it.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#monty-hall' | relative_url }}">Check out Monty Hall →</a>
  </div>

  <div class="ep-card">
    <h3>Money from a stock going nowhere</h3>
    <p>
      Split your money between a stock and cash. The stock ends the year
      exactly where it started, yet regularly rebalancing back to half and
      half leaves you ahead anyway — you've harvested its volatility, not its
      direction.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#shannon-demon' | relative_url }}">Check out Shannon's demon →</a>
  </div>

  <div class="ep-card">
    <h3>A bad bet both sides are right to take</h3>
    <p>
      Insurance premiums always exceed the expected payout, so buyers who
      maximize expected value should never buy any. Yet a band of premiums
      exists where both buyer and seller come out ahead — expected value
      alone misses it.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#insurance' | relative_url }}">Check out insurance and risk pooling →</a>
  </div>

  <div class="ep-card">
    <h3>Two losing games, mixed into a winner</h3>
    <p>
      Two games, each individually guaranteed to lose. Alternate between them
      and your capital climbs. It's not a trick — Juan Parrondo built it from
      the same physics as Feynman's ratchet: "losing" isn't a property a game
      carries by itself.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#parrondo' | relative_url }}">Check out Parrondo's paradox →</a>
  </div>

  <div class="ep-card">
    <h3>A 95% accurate test, and a 2% chance you're sick</h3>
    <p>
      A 95%-accurate test comes back positive. Harvard staff and students,
      asked the odds you're actually sick, mostly guessed 95%. The real
      answer is about 2% — the missing piece is how rare the disease was to
      begin with.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#base-rates' | relative_url }}">Check out base rates and the 95% test →</a>
  </div>

  <div class="ep-card">
    <h3>Twenty-three people, better than even odds</h3>
    <p>
      How many people need to be in a room before two probably share a
      birthday? Intuition says 183; the real answer is 23, because every pair
      is compared against every other pair — 253 comparisons, not one.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#birthday' | relative_url }}">Check out the birthday problem →</a>
  </div>

  <div class="ep-card">
    <h3>Reject the first 37%, then take the next record</h3>
    <p>
      Candidates arrive one at a time; accept or reject on the spot, no going
      back. Skip the first 37% no matter how good they look, then take the
      next one better than all of them — nothing does better.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#secretary' | relative_url }}">Check out the secretary problem →</a>
  </div>

  <div class="ep-card">
    <h3>Whatever you find, swapping looks 25% better</h3>
    <p>
      One envelope holds twice what the other does. Find $100, and swapping
      looks worth $125 — but the same logic applies to any amount, even
      before you look, so you'd swap forever. The flaw hides in an unstated
      prior.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#two-envelopes' | relative_url }}">Check out the two-envelope paradox →</a>
  </div>

  <div class="ep-card">
    <h3>Keep testing until it works</h3>
    <p>
      Test as you go, adding data until the result is significant. It feels
      diligent; it's actually a false-positive machine — a nominal 5% error
      rate can climb past 60% once you're allowed to keep looking.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#optional-stopping' | relative_url }}">Check out optional stopping →</a>
  </div>

</div>
