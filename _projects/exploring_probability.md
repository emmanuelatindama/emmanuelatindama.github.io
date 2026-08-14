---
layout: page
title: Exploring Probability
description: Interactive simulations of games where the average outcome and the typical outcome disagree.
importance: 1
category: work
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
Losses <em>absorb</em>, so $0 is a place you can arrive at but never leave.
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
      Have you ever been offered a game that seemed too good to be true? Heads,
      your money grows by 50%; tails, you only lose 40%. The arithmetic is not
      in dispute — that is +5% a round, on average, forever, and the house is
      apparently handing out free money. Sit down and play it and you go broke
      almost surely. Wait just a minute. Both of those sentences are true at
      the same time, and the reason they can be is the whole subject.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#ergodic-coin' | relative_url }}">Check out the ergodic coin flip →</a>
  </div>

  <div class="ep-card">
    <h3>How much to bet</h3>
    <p>
      Did you know that with the odds held exactly fixed, the size of your bets
      alone decides whether you walk away a winner or a loser? Say your team
      wins x% of the time and loses the rest. You are going to back them week
      after week, out of the same pot. How much of it should go in each week to
      be ahead at the end of the season? Too little and you crawl; too much and
      the swings eat you alive — and the crossover point is a formula, not a
      feeling.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#kelly' | relative_url }}">Check out Kelly bet sizing →</a>
  </div>

  <div class="ep-card">
    <h3>Nearly fair is not fair</h3>
    <p>
      You have $100, the house has millions, and the coin is very nearly fair —
      49 wins for every 51 losses, say. Surely a coin that close to even gives
      you a fighting chance of doubling up before you bust? Now make the coin
      perfectly fair and take away your target, so you simply play forever:
      what are your chances then? And here is the part nobody guesses — with
      the odds against you, is it safer to bet $1 a round, or $50?
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#gamblers-ruin' | relative_url }}">Check out gambler's ruin →</a>
  </div>

  <div class="ep-card">
    <h3>A ticket worth infinity</h3>
    <p>
      A casino tosses a coin until it comes up tails, and the pot doubles on
      every toss that isn't. Work out the expected payout and it is not large —
      it is infinite. A ticket of unlimited value, on sale. What would you pay
      for it? Almost nobody will go past a few dollars, and almost nobody can
      say why they are right to refuse. They are right. Half of all games pay
      exactly $1.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#st-petersburg' | relative_url }}">Check out the St Petersburg paradox →</a>
  </div>

  <div class="ep-card">
    <h3>Winning by never winning</h3>
    <p>
      Two suspects, two separate rooms. Betraying the other pays better
      whatever they choose — so both betray, and both end up worse off than if
      they had kept quiet. That is one round. Now play it hundreds of times
      against every kind of opponent, from the relentless defector to the saint
      who never retaliates. Which one comes out on top? The answer is four
      lines long, and it never once outscores an opponent.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#prisoners-dilemma' | relative_url }}">Check out the iterated prisoner's dilemma →</a>
  </div>

  <div class="ep-card">
    <h3>Should you switch?</h3>
    <p>
      Three doors, one prize. You pick one; the host, who knows exactly
      where the prize is, opens another to show you a goat, then offers you
      the switch. Nearly everyone's gut says it can't matter — two doors
      left, fifty-fifty. A magazine columnist said switch, and win two times
      in three. Ten thousand readers, many with doctorates, wrote in to tell
      her she was wrong. She wasn't.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#monty-hall' | relative_url }}">Check out Monty Hall →</a>
  </div>

  <div class="ep-card">
    <h3>Money from a stock going nowhere</h3>
    <p>
      Split your money evenly between a stock and cash. The stock ends the
      year exactly where it started — up as often as down, no trend at all.
      Rebalance back to half and half every so often, selling a little after
      it rises and buying a little after it falls, and you finish ahead
      anyway. Nothing about the stock changed; what you harvested was its
      volatility, not its direction.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#shannon-demon' | relative_url }}">Check out Shannon's demon →</a>
  </div>

  <div class="ep-card">
    <h3>A bad bet both sides are right to take</h3>
    <p>
      The premium you pay for insurance is always more than the payout is
      worth on average — that's how insurers stay solvent. A player who
      only cares about expected value should never buy a policy. Everyone
      does anyway, and it isn't a mistake: there's a real band of premiums
      where the buyer and the seller both come out ahead in the long run,
      and expected value alone cannot see it.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#insurance' | relative_url }}">Check out insurance and risk pooling →</a>
  </div>

  <div class="ep-card">
    <h3>Paid either way</h3>
    <p>
      Sell a put below a recent dip and you get paid whichever way it goes —
      keep the premium if the stock recovers, or buy the shares at a price you
      already liked if it doesn't. Take delivery, keep them for good, and sell
      a call at every new high: paid again. Traders call the cycle "the
      wheel," and getting paid on both sides of every move sounds like it must
      beat simply owning the stock. Run it on what the S&amp;P, Apple or the
      Nikkei actually did since 2009 and it sometimes does, sometimes loses
      badly — and the win rate on the individual trades tells you nothing
      about which.
    </p>
    <a class="ep-go" href="{{ '/exploring-probability/#the-wheel' | relative_url }}">Check out the wheel strategy →</a>
  </div>

</div>

<p class="ep-soon">
  Queued up next, and visible as a roadmap inside the app itself: Parrondo's
  paradox, base rates and the 95% test, the birthday problem, the secretary
  problem, the two-envelope paradox, and optional stopping.
</p>
