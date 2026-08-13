---
layout: page
title: exploring probability
description: when expected value lies to you — interactive simulations of multiplicative betting games
img: assets/img/exploring-probability.png
importance: 1
category: work
---

**[Open the interactive demo →](https://emmanuelatindama.github.io/exploring-probability/)**

Start with \$100 and flip a fair coin. Heads multiplies your wealth by 1.5, tails
by 0.6. Every round has an expected return of **+5%**, so the game looks like
free money. Play it 100 times:

| | |
| :--- | ---: |
| Expected final wealth | **\$13,150** |
| Median final wealth | **\$0.52** |
| Players ending below \$100 | **86.4%** |
| Players ending below \$1 | **54.0%** |

Both columns are correct. The expectation is carried by a vanishingly small
number of astronomically lucky paths, while the median follows the geometric mean
$$\sqrt{1.5 \times 0.6} \approx 0.949$$ — so the typical player decays at
**−5.3% per round** while the average grows at +5%. Averaging across players and
averaging across time give different answers: the process is *non-ergodic*, and
the expected value describes nobody's actual experience.

Then stake only **25%** of your wealth each round instead of everything, and the
same game flips from −5.3%/round to **+0.62%/round**. That optimum is the Kelly
criterion, and the second scenario derives where it comes from — including the
point past which more edge makes you poorer.

### What's in it

The page simulates everything in the browser, so every parameter is a slider:
the payoffs, the win probability, the number of rounds, the stake fraction, and
the number of players. Nothing is precomputed.

- **Ergodic coin flip** — the paradox above, as quantile bands over a log wealth axis
- **Kelly bet sizing** — long-run growth rate against stake size, in closed form
- *Gambler's ruin*, *St. Petersburg paradox*, and an *iterated prisoner's dilemma*
  tournament are next

### How it's built

A static page with no build step — plain JavaScript plus Plotly, hosted on GitHub
Pages. The part I cared most about is that the mathematics is *checked* rather
than asserted:

- A Python lab (`numpy`/`scipy`) holds the closed forms — exact expectations,
  binomial quantiles, tail probabilities, and the Kelly optimum — and is the
  single source of truth.
- Those closed forms are verified against a 400,000-path Monte Carlo, and any
  optimum against a brute-force sweep.
- The browser engine mirrors the Python, down to a seeded PRNG that matches
  **bit-for-bit**, so a given seed reproduces identical trajectories in both
  languages. A test page asserts all of this in 108 checks.

One consequence worth noting: the sample mean of the simulated players usually
lands nowhere near the exact expected value (\~\$788 against \$13,150 at the
default settings). That isn't a bug in either number — the expectation depends on
outcomes so rare that a few hundred thousand players almost never contain one.
The mean of a heavy-tailed variable is, in practice, close to unmeasurable.

**[Source on GitHub](https://github.com/emmanuelatindama/exploring-probability)**
