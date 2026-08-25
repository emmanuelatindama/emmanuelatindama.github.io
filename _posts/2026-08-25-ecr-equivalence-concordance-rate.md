---
layout: post
title: "Equivalence Concordance Rate (ECR): Calibrating Equivalence Acceptance Criteria"
date: 2026-08-25 10:00:00-0400
description: A simulation-based framework that scores how coherently any equivalence margin makes decisions — with a four-method case study over 10,368 scenarios, a closed-form off-center Ppk margin, and a worked example on real manufacturing data.
tags: Statistics DesignOfExperiments
categories: my-posts
giscus_comments: true
related_posts: true
pretty_table: true
tabs: true
thumbnail: assets/img/eac/baseline.png
chart:
  plotly: true
author: Padraic Nagle, Huruy Asfha, Qing Meng, and Emmanuel A. Atindama — Global Statistics, MS&T, Bristol Myers Squibb
---

<p class="post-lead">How do you know whether a chosen equivalence margin is actually a <em>good</em> one? The Equivalence Concordance Rate (ECR) framework answers that question — not by proposing yet another margin, but by measuring how coherently any proposed margin makes decisions.</p>

When a pharmaceutical process changes — a site transfer, a scale-up, a new piece of equipment — regulators expect evidence that the product is **comparable** before and after. The standard tool is the **Two One-Sided Tests (TOST)** procedure, and the whole verdict hangs on a single pre-specified number: the **Equivalence Acceptance Criterion (EAC)**, the margin $$\Delta$$ within which two process means count as "the same."

Set it too wide and a shifted process is wrongly accepted; too narrow and an acceptable process is wrongly rejected. Many recipes for setting the margin coexist — $$\sigma$$-scaled, percent-of-mean, effect-size, capability-linked — but they are seldom ranked by the **coherence of the decisions they induce**. ICH Q5E deliberately specifies no single statistical method, which leaves the choice to the analyst without a common yardstick.

> **The key idea.** This work does **not** introduce a new hypothesis test or a new margin. It is a **calibration and comparison framework** that takes *any* candidate EAC — however derived — and scores how well it supports coherent equivalence decisions, then lets you rank and tune competing margins on a level playing field.

A practical consequence worth stating up front: because the diagnostic sweeps *hypothetical* shifts around an estimated process, **a single comparability dataset is enough** to benchmark whatever margin you are currently using.

### What you'll find below

- **The ECR framework** — a 2×2 decision matrix cross-classifying a difference test against an equivalence test, yielding three diagnostic curves and one scalar score (iECR).
- **A four-method case study** — $$\sigma$$-scaled, percent-of-mean, effect-size, and Ppk-informed margins over a **constrained factorial design of 10,368 valid scenarios**.
- **A new closed-form result** — the capability-informed margin generalized to **off-center** processes, with an explicit feasibility boundary.
- **Actionable guidance** — a purpose-first decision framework, an ANOVA attribution of what really drives decision quality, and a **worked example on real manufacturing data**.

---

## 2. The ECR Framework

A well-calibrated margin maximizes agreement between two verdicts about the same data; the rate of *disagreement* — contradiction or inconclusiveness — measures its calibration. The framework turns that intuition into a measurement, and it is **method-agnostic**: feed it any candidate $$\Delta$$ and it returns a quantitative diagnostic of that margin's calibration quality and trade-offs.

### The two tests

For a quality attribute measured before and after a change, with $$X_i \sim \mathcal{N}(\mu_{pre},\sigma_{pre}^2)$$ and $$Y_j \sim \mathcal{N}(\mu_{pre}+\delta_{true},\sigma_{post}^2)$$, two tests are applied to the *same* two-sample dataset:

- **Difference test (D-test)** — a two-sided $$t$$-test of $$H_0\colon \mu_{post}-\mu_{pre}=0$$, asking *"is there any detectable difference?"*
- **Equivalence test (E-test)** — TOST, testing $$H_0\colon |\mu_{post}-\mu_{pre}|\ge\Delta$$ against $$H_a\colon |\mu_{post}-\mu_{pre}|<\Delta$$, asking *"is the shift small enough to be practically equivalent?"*

Both read the same $$\hat\delta = \bar Y - \bar X$$ and the same pooled standard error, with $$\alpha_d=\alpha_e=0.05$$ throughout.

### The decision matrix

Crossing the two pass/fail outcomes yields four mutually exclusive zones:

<table style="text-align:center; border-collapse:collapse;">
  <thead>
    <tr style="background-color:#D6EAF8;">
      <th style="padding:10px; border:1px solid #ccc;"></th>
      <th style="padding:10px; border:1px solid #ccc;">E-test pass <br><span style="font-weight:normal;">(equivalence concluded)</span></th>
      <th style="padding:10px; border:1px solid #ccc;">E-test fail <br><span style="font-weight:normal;">(equivalence not concluded)</span></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th style="padding:10px; border:1px solid #ccc; background-color:#D6EAF8;">D-test fail <br><span style="font-weight:normal;">(no significant difference)</span></th>
      <td style="padding:12px; border:1px solid #ccc; background-color:#D5F5E3;"><strong>Z₁ ✓</strong><br>Concordant-equivalent</td>
      <td style="padding:12px; border:1px solid #ccc; background-color:#FDEBD0;"><strong>Z₂ ?</strong><br>Gray zone</td>
    </tr>
    <tr>
      <th style="padding:10px; border:1px solid #ccc; background-color:#D6EAF8;">D-test pass <br><span style="font-weight:normal;">(significant difference)</span></th>
      <td style="padding:12px; border:1px solid #ccc; background-color:#FADBD8;"><strong>Z₃ !</strong><br>Paradox</td>
      <td style="padding:12px; border:1px solid #ccc; background-color:#D5F5E3;"><strong>Z₄ ✓</strong><br>Concordant-different</td>
    </tr>
  </tbody>
</table>

<div class="caption">The two green zones are coherent; the amber gray zone is inconclusive; the red paradox zone is an outright contradiction — the data are "different" yet "equivalent" at the same time. The cross-classification itself comes from three-sided testing; the contribution here is turning it into an <em>operating characteristic of the joint procedure</em>.</div>

### Three diagnostic rates

From $$N$$ Monte Carlo replicates at a given true shift, the zone counts define:

$$
ECR = \frac{Z_1 + Z_4}{N},\qquad PR = \frac{Z_3}{N},\qquad GZR = \frac{Z_2}{N},
$$

with $$ECR + PR + GZR = 1$$ at every shift. Reading them is intuitive:

- **High ECR** → the margin produces **coherent** decisions.
- **High PR (paradox rate)** → the margin is **wide relative to detectability**.
- **High GZR (gray-zone rate)** → the margin is **too narrow**, or the study is **underpowered** for a decisive outcome.

> **An important clarification — PR is not a false-acceptance rate.** Because the D-test has a *point* null and flags *any* detectable shift, a paradox can arise even when TOST **correctly** declares equivalence for a shift genuinely inside the margin. $$PR$$ measures **disagreement**, not error. Classical false-acceptance/false-rejection operating characteristics must fix externally which true differences count as acceptable; ECR instead references statistical **detectability**. Where a defensible relevance threshold exists, use it directly — the difference test is only a stand-in, and one whose validity weakens at large $$n$$.

The two disagreement modes are not defects but **opposite directions of decision risk**: a paradox is the **consumer's-risk** direction; a gray zone the **producer's-risk** direction (an acceptable process left unconfirmed — a cost to the manufacturer). Reporting them separately lets a practitioner weigh both instead of collapsing them into one verdict.

### The ECR curve and the iECR score

Sweeping the true standardized shift $$\delta/\sigma_{pre}$$ traces the **ECR curve**:

- **Small shifts** ($$\delta \ll \Delta$$): no difference detected, equivalence concluded — mostly $$Z_1$$, and $$ECR \to 1-\alpha_d$$.
- **Large shifts** ($$\delta \gg \Delta$$): difference detected, equivalence not concluded — again the tests agree, $$ECR \approx 1$$.
- **Intermediate shifts**: $$\hat\delta$$ lands between the two thresholds and the tests frequently disagree, so the curve **dips** — near, but *not exactly at*, $$\delta=\Delta$$, since the disagreement window is bounded by $$t_d\,\mathrm{se}$$ and $$\Delta - t_e\,\mathrm{se}$$ rather than by $$\Delta$$ itself.

The dip is the diagnostic signature of the method. Collapsing the curve into one number gives the **integrated ECR**, with $$u=\delta/\sigma_{pre}$$:

$$
iECR = \frac{1}{u_{max}}\int_0^{u_{max}} ECR(u)\,du,
$$

a scalar in $$[0,1]$$ that enables **direct ranking** of competing margins. Higher iECR = better calibration across the operating range. The shift limit $$u_{max}$$ changes the absolute level and can reorder the *lower*-ranked methods, but not which method ranks highest.

---

## 3. EAC Methods: A Case Study

To demonstrate the framework end-to-end, the paper applies it to four structurally distinct margins. These are **not** contributions of the paper (apart from the Ppk closed form) — they are a case study chosen because each encodes a different philosophy of a tolerable shift: process variability (A), the process mean (B), an assumed effect size with a finite-sample correction (C), and process capability (D).

| Method | Formula | Philosophy | Provenance of the default |
| :-- | :-- | :-- | :-- |
| **A. $$\sigma$$-Scaled** | $$\mathrm{EAC}_A = \lambda\,\sigma_{pre}$$ | margin scales with process noise | $$\lambda=1.5$$ from the FDA's *draft* Tier-1 analytical-similarity criterion ($$1.5\,\sigma_R$$), withdrawn in 2018 |
| **B. Percent-of-Mean** | $$\mathrm{EAC}_B = \lambda_\%\,\lvert\mu_{pre}\rvert$$ | margin is a % of the mean level | mean-referenced limits are established in bioequivalence (ICH M13A, 80–125%), though there on a log-scale ratio |
| **C. Effect-Size** | $$\mathrm{EAC}_C = ES\cdot\hat\sigma_{upper}$$ | $$\sigma$$-scaled **+** $$\chi^2$$ variance correction | $$ES=1.5$$, matched to A for a like-for-like comparison |
| **D. Ppk-Informed** | $$\mathrm{EAC}_D = \max\!\big(d_{pre}-3\,Ppk_{target}\,\sigma_{pre},\,0\big)$$ | anchored to process capability & spec limits | $$Ppk_{target}=0.8\,Ppk_{pre}$$ (retain ≥80% of capability) |

An important framing point the revised paper is explicit about: **these tuning values are illustrative, not established standards.** Only Method A's $$\lambda$$ has an external anchor; C's $$ES$$ is matched to it, and B and D take round conventional values. What the comparison delivers is *one consistent as-applied configuration* of each method — not a general ranking.

### Method C is Method A plus a variance hedge

Setting $$c=\sqrt{(n_{pre}-1)/\chi^2_{\alpha_{\chi^2},n_{pre}-1}}\ge 1$$ and evaluating at $$s_{pre}=\sigma_{pre}$$:

$$
\mathrm{EAC}_C = \underbrace{ES}_{\lambda}\cdot\underbrace{\sigma_{pre}\,c}_{\hat\sigma_{upper}} \;\xrightarrow{\;n_{pre}\to\infty\;}\; \lambda\,\sigma_{pre} = \mathrm{EAC}_A .
$$

With $$ES=\lambda$$, **Method C *is* Method A inflated by $$c$$** — widening the margin to absorb sampling variability where A takes $$\sigma_{pre}$$ at face value. That is their *only* structural difference, which makes A-vs-C a clean controlled test of the variance correction itself. The inflation is $$\approx1.6\times$$ at $$n_{pre}=10$$ and $$\approx1.3\times$$ at $$n_{pre}=30$$.

### The Ppk-informed margin, off-center — a new closed form

For a process with mean $$\mu$$ and spread $$\sigma$$ inside $$[LSL, USL]$$, the performance index is $$Ppk=\min\!\big(\tfrac{USL-\mu}{3\sigma},\tfrac{\mu-LSL}{3\sigma}\big)$$. For a **centered** process with half-width $$S=(USL-LSL)/2$$, the largest shift that still meets $$Ppk_{target}$$ is $$\max(S-3\,Ppk_{target}\,\sigma_{pre},0)$$.

Real processes are never perfectly centered, and the paper's **off-center correction** replaces $$S$$ with $$d_{pre}$$, the distance from $$\mu_{pre}$$ to the *nearest* specification limit:

$$
\mathrm{EAC}_D = \max\!\left(d_{pre} - 3\,Ppk_{target}\,\sigma_{pre},\; 0\right),\qquad d_{pre}=\min(USL-\mu_{pre},\,\mu_{pre}-LSL)
$$

which guarantees $$Ppk_{post}\ge Ppk_{target}$$ **regardless of shift direction** and reduces to the centered form when $$d_{pre}=S$$. The guarantee is conditional on unchanged spread: if $$\sigma_{post}>\sigma_{pre}$$, the worst case is $$Ppk_{post}=(d_{pre}-|\delta|)/(3\sigma_{post})$$ and the target can fail even inside the margin — which is exactly why the robustness analysis varies $$\sigma_{post}/\sigma_{pre}$$.

> **The feasibility boundary.** The margin decreases linearly in $$Ppk_{target}$$ and vanishes once $$Ppk_{target}\ge d_{pre}/(3\sigma_{pre}) = Ppk_{pre}$$. So anchoring directly to *current* capability collapses the margin to zero — and a zero-width margin leaves the TOST alternative empty, meaning **no shift can ever be declared equivalent**. The fix is a **capability retention fraction** $$\rho\in(0,1)$$ with $$Ppk_{target}=\rho\,Ppk_{pre}$$, which simplifies neatly:
>
> $$\mathrm{EAC}_D = \max\!\big(d_{pre}-3\rho\,Ppk_{pre}\,\sigma_{pre},\,0\big) = d_{pre}\,(1-\rho).$$
>
> Under a relative target, $$\mathrm{EAC}_D>0$$ reduces to $$\rho<1$$ and **always holds**. A *fixed* target (e.g. $$Ppk_{target}=1.33$$) reintroduces the cliff.

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/eac/baseline.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
<strong>Figure 1.</strong> Baseline standardized margins (\(\mathrm{EAC}/\sigma_{pre}\)): D = 0.95, A = 1.50, C = 2.06, B = 2.51. The four methods imply very different margins from the <em>same</em> data — and that difference drives everything downstream. Tightest to widest, the order is D &lt; A &lt; C &lt; B.
</div>

---

## 4. Experimental Setup

The engine is a **constrained factorial Monte Carlo** over *dimensionless* process descriptors. Because the EAC formulae use the pre-change parameters only through ratios and the $$t$$-statistics are scale-invariant, the study fixes $$\sigma_{pre}=1$$ without loss of generality and varies the ratios that actually matter.

The process mean is parameterized off-center as $$\mu_{pre}=m+\kappa S$$, where $$m$$ is the specification midpoint and $$\kappa$$ the **off-center fraction**, so the nearer-limit distance is $$d_{pre}=S(1-|\kappa|)$$.

<table style="text-align:center; border-collapse:collapse;">
  <thead>
    <tr style="background-color:#D6EAF8;">
      <th style="padding:8px; border:1px solid #ccc;">Factor</th>
      <th style="padding:8px; border:1px solid #ccc;">Grid values</th>
      <th style="padding:8px; border:1px solid #ccc;"># levels</th>
    </tr>
  </thead>
  <tbody>
    <tr><td style="padding:8px; border:1px solid #ccc;">Midpoint-to-variability $$m/\sigma_{pre}$$</td><td style="padding:8px; border:1px solid #ccc;">5, 10, 15, 25, 35, 50</td><td style="padding:8px; border:1px solid #ccc;">6</td></tr>
    <tr><td style="padding:8px; border:1px solid #ccc;">Spec-to-variability $$S/\sigma_{pre}$$</td><td style="padding:8px; border:1px solid #ccc;">2.5, 5, 10</td><td style="padding:8px; border:1px solid #ccc;">3</td></tr>
    <tr><td style="padding:8px; border:1px solid #ccc;">Pre-change sample size $$n_{pre}$$</td><td style="padding:8px; border:1px solid #ccc;">4, 8, 12, 16, 20, 24, 28, 30</td><td style="padding:8px; border:1px solid #ccc;">8</td></tr>
    <tr><td style="padding:8px; border:1px solid #ccc;">Sample-size ratio $$r = n_{post}/n_{pre}$$</td><td style="padding:8px; border:1px solid #ccc;">⅓, ½, 1, 2</td><td style="padding:8px; border:1px solid #ccc;">4</td></tr>
    <tr><td style="padding:8px; border:1px solid #ccc;">Standard-deviation ratio $$\sigma_{post}/\sigma_{pre}$$</td><td style="padding:8px; border:1px solid #ccc;">0.5, 0.75, 1.0, 1.25, 1.5, 2.0</td><td style="padding:8px; border:1px solid #ccc;">6</td></tr>
    <tr><td style="padding:8px; border:1px solid #ccc;">Off-center fraction $$\kappa$$</td><td style="padding:8px; border:1px solid #ccc;">0.05, 0.10, 0.20, 0.35</td><td style="padding:8px; border:1px solid #ccc;">4</td></tr>
  </tbody>
</table>

<div class="caption">This grid yields \(6\times3\times8\times4\times6\times4 = 13{,}824\) nominal combinations; enforcing \(4\le n_{post}\le 30\) leaves <strong>10,368 valid scenarios</strong> — only 24 of the 32 \(n_{pre}\times r\) pairs survive, which is what makes the design <em>constrained</em> rather than fully crossed. The three \(S/\sigma_{pre}\) levels correspond to centered \(Ppk \in \{0.83,\,1.67,\,3.33\}\). Each scenario is evaluated at 20 shifts over \([0,\,4\sigma_{pre}]\) with 5,000 Monte Carlo replicates per shift.</div>

Three design choices keep the comparison fair and interpretable:

- **Common random numbers.** All four methods are scored on the *same* simulated datasets with only $$\Delta_M$$ differing, so differences reflect the margin, not Monte Carlo noise.
- **Margins fixed per scenario, not per replicate.** Each margin is computed once from the pre-change *parameters*, so the analysis is dependent on those parameters but independent of any specific sample. This has one method-specific consequence: **Method C's $$\chi^2$$ inflation hedges against underestimating $$\sigma_{pre}$$, so a known $$\sigma_{pre}$$ leaves that hedge unexercised** — part of C's paradox rate is an artifact of the design. The paper therefore reruns the entire grid with margins re-estimated from each replicate's own pre-change sample (see §7).
- **Prespecified defaults *and* tuned optima.** The primary comparison uses the fixed defaults above. A separate two-stage sweep (coarse, then a 15-point fine grid centered on each method's own coarse optimum) reports the best achievable performance. Those grid-averaged optima are a **diagnostic upper bound, not recommended settings**.

The **baseline scenario** ($$m/\sigma=50$$, $$S/\sigma=5$$, $$n_{pre}=n_{post}=20$$, $$\sigma_{post}/\sigma_{pre}=1$$, $$\kappa=0.05$$) implies limits $$[45,55]$$, $$\mu_{pre}=50.25$$, $$d_{pre}=4.75$$, and $$Ppk_{pre}=1.58$$. It is one of the 10,368 cells, shown on its own only because the grid reports a single scalar per scenario — **the *shape* of $$ECR(\delta)$$ is visible only at a fixed parameterization.** The deliberately large $$m/\sigma_{pre}$$ places Method B's mean-scaled margin at the wide end of its range, making its dependence on $$\mu_{pre}$$ visible.

---

## 5. Results

### 5.1 Baseline behaviour — one scenario, four very different profiles

The operating characteristics already foreshadow the trade-offs. Where each TOST curve crosses its own dotted margin line, $$\delta=\Delta_M$$ and the chance of declaring equivalence is at most $$\alpha_e=5\%$$; the D-test is calibrated at the other end, rejecting 5% of the time at zero shift. Method D sits low even at zero shift, because its tight margin is **underpowered at $$n=20$$**.

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/eac/power_curves.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption"><strong>Figure 2.</strong> Analytical decision probabilities. Left: TOST pass probability vs. true shift; dotted lines mark each method's EAC. Right: the shared D-test power curve, with a dashed line at 80%.</div>

Running the ECR engine at this scenario (10,000 replicates at each of 40 shifts) produces the signature U-shaped curves — coherent at the extremes, dipping near each margin's boundary:

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/eac/methods_baseline_peformance.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption"><strong>Figure 3.</strong> Monte Carlo ECR, GZR, and PR curves (left to right) at baseline. A wide margin trades gray zone for paradox; a tight one does the reverse.</div>

| Method | $$\mathrm{EAC}/\sigma_{pre}$$ | iECR | min ECR | max GZR | max PR |
| :-- | :--: | :--: | :--: | :--: | :--: |
| **D. Ppk-Informed** | 0.95 | **0.945** | 0.737 | 0.259 | **0.004** |
| **A. $$\sigma$$-Scaled** | 1.50 | 0.916 | 0.606 | 0.001 | 0.394 |
| **C. Effect-Size** | 2.06 | 0.777 | 0.169 | 0.000 | 0.831 |
| **B. %-of-Mean** | 2.51 | 0.662 | 0.039 | 0.000 | 0.961 |

Notice that the **tight** Ppk-informed margin wins here, with a near-zero paradox rate — and that no method leads on all three diagnostics. **This scenario shows shape, not rank:** the iECR order here is not the grid's.

{% tabs iecr-rankings %}

{% tab iecr-rankings Baseline (single scenario) %}

```plotly
{
  "data": [
    {"x": ["D: Ppk-Informed", "A: σ-Scaled", "C: Effect-Size", "B: %-of-Mean"],
     "y": [0.945, 0.916, 0.777, 0.662],
     "type": "bar",
     "marker": {"color": ["#E91E63", "#2196F3", "#4CAF50", "#FF9800"]},
     "text": ["0.945", "0.916", "0.777", "0.662"], "textposition": "outside"}
  ],
  "layout": {
    "title": "Baseline iECR (higher = better calibrated)",
    "yaxis": {"title": "iECR", "range": [0, 1.05]},
    "margin": {"t": 40, "b": 40}
  }
}
```

{% endtab %}

{% tab iecr-rankings Across the full grid (mean) %}

```plotly
{
  "data": [
    {"x": ["A: σ-Scaled", "C: Effect-Size", "D: Ppk-Informed", "B: %-of-Mean"],
     "y": [0.872, 0.822, 0.808, 0.800],
     "type": "bar",
     "marker": {"color": ["#2196F3", "#4CAF50", "#E91E63", "#FF9800"]},
     "error_y": {"type": "data", "array": [0.107, 0.101, 0.112, 0.112], "visible": true},
     "text": ["0.872", "0.822", "0.808", "0.800"], "textposition": "outside"}
  ],
  "layout": {
    "title": "Mean iECR over 10,368 scenarios (±1 SD)",
    "yaxis": {"title": "mean iECR", "range": [0, 1.15]},
    "margin": {"t": 40, "b": 40}
  }
}
```

{% endtab %}

{% tab iecr-rankings At each method's tuned optimum %}

```plotly
{
  "data": [
    {"x": ["C: Effect-Size", "A: σ-Scaled", "D: Ppk-Informed", "B: %-of-Mean"],
     "y": [0.930, 0.908, 0.842, 0.836],
     "type": "bar",
     "marker": {"color": ["#4CAF50", "#2196F3", "#E91E63", "#FF9800"]},
     "text": ["0.930<br>ES*=1.00", "0.908<br>λ*=1.43", "0.842<br>ρ*=0.83", "0.836<br>λ%*=0.039"],
     "textposition": "outside"}
  ],
  "layout": {
    "title": "Peak iECR after tuning each method",
    "yaxis": {"title": "peak iECR", "range": [0, 1.15]},
    "margin": {"t": 40, "b": 40}
  }
}
```

{% endtab %}

{% endtabs %}

<div class="caption">Toggle the tabs: the ranking <em>reshuffles</em> as we move from one scenario, to the full grid, to tuned optima — which is exactly why a single benchmark scenario can mislead. Note the standard deviations in the middle panel: the three lower methods overlap heavily.</div>

#### Sample size for TOST power

Tighter margins demand more data. Computed analytically from the **exact joint TOST acceptance probability** (the bivariate non-central $$t$$ of Owen/Phillips, rather than the common "take the smaller one-sided power" shortcut, which ignores the shared data and only gives an upper bound):

| Method | $$\mathrm{EAC}/\sigma_{pre}$$ | $$n$$ per group for 80% power | for 90% power |
| :-- | :--: | :--: | :--: |
| A. $$\sigma$$-Scaled | 1.50 | 9 | 11 |
| B. %-of-Mean | 2.51 | 4 | 5 |
| C. Effect-Size | 2.06 | 5 | 6 |
| D. Ppk-Informed | 0.95 | **20** | **25** |

These hold at the *baseline* margins, with only sample size varying; scenario-specific planning should recompute power.

### 5.2 Ranking across the grid — and how little of it is stable

Averaged over all 10,368 scenarios at prespecified defaults, the **$$\sigma$$-scaled** Method A is the most robust general-purpose choice. But the revised analysis is careful about how much weight the rest of the ordering can bear:

| Method | mean iECR | SD | min iECR | iGZR | iPR | max GZR | max PR | mean EAC/$$\sigma$$ |
| :-- | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| **A. $$\sigma$$-Scaled** | **0.872** | 0.107 | 0.397 | 0.092 | 0.036 | 0.220 | 0.170 | 1.50 |
| **C. Effect-Size** | 0.822 | 0.101 | 0.337 | 0.013 | 0.165 | 0.028 | **0.512** | 2.35 |
| **D. Ppk-Informed** | 0.808 | 0.112 | 0.381 | 0.172 | **0.020** | **0.596** | 0.083 | 0.96 |
| **B. %-of-Mean** | 0.800 | 0.112 | 0.381 | 0.146 | 0.054 | 0.501 | 0.171 | 1.22 |

> **Only the top of the ranking is stable.** Mean iECR spans just 0.800–0.872. Method A is highest, but the other three fall **within 0.022 of one another** and their order is *not* stable — C and D differ by only 0.014 and reverse under other scenario mixes and shift limits. Per scenario, **A has the highest iECR in 47% of the grid and the lowest in only 2%**, while B, C, and D are each lowest in 28–36% of scenarios, so **none of them is reliably the weakest**.

What *is* clear is the trade-off structure: **C has the highest paradox rate** (mean max PR = 0.512) and **D the highest gray-zone rate** (mean max GZR = 0.596).

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/eac/violin_plots.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption"><strong>Figure 4.</strong> Full iECR distribution across all 10,368 scenarios. Method A places most mass near 0.95 with a long lower tail; C sits slightly lower but reaches the smallest values; D and B are broadest, centered near 0.8.</div>

### 5.3 Robustness — what makes or breaks each margin

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/eac/robustness_combined.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption"><strong>Figure 5.</strong> Mean iECR against (a) pre-change sample size and (b) the standard-deviation ratio, each marginalized over all remaining design factors.</div>

**Sample size** is the single biggest driver, and it cuts both ways. All methods improve steeply up to $$n_{pre}\approx12$$. Beyond that, B and D keep improving — but **C turns over near 16 and A near 24**, because the overpowered point-null D-test starts flagging trivially small shifts as significant, widening the paradox window for the wider margins:

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/eac/overpowered_dtest.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption"><strong>Figure 6.</strong> The overpowered-D-test effect. Left: integrated paradox rate vs. \(n_{pre}\). Right: at a fixed shift of \(0.5\,\sigma_{pre}\), every method's paradox rate approaches 1 by \(n=200\) — Method D last. Method C's integrated rate is U-shaped, bottoming out near \(n_{pre}=16\).</div>

**Unequal variance** splits the methods. As the post-change spread inflates, A, B, and D all decline — but **Method C *improves*, and overtakes A beyond $$\sigma_{post}/\sigma_{pre}\approx1.5$$**. The mechanism: inflating $$\sigma_{post}$$ enlarges the standard error, widening the threshold separation $$(t_d+t_e)\,\mathrm{se}$$ and pushing every method toward the gray zone. That *harms* tight margins but *corrects* C, whose margin is the widest and most paradox-prone. This is the Method × standard-deviation-ratio interaction — the second-largest ANOVA effect.

> **Is that just an artifact of pooling?** No. Both tests pool variances throughout, which is misspecified when $$\sigma_{post}\neq\sigma_{pre}$$. Repeating the marginal analysis with **Welch–Satterthwaite** versions of both tests lowers absolute iECR modestly under strong inflation, but C still overtakes A at $$\approx1.5$$. Method C's robustness under variance inflation is **genuine**.

Method D's feasibility cliff is worth seeing concretely. Under a *fixed* target $$Ppk_{target}=1.33$$, a centered process has **zero margin** until $$S/\sigma_{pre}=3\,Ppk_{target}\approx4$$; above the cliff iECR peaks near $$S/\sigma_{pre}=5.25$$ and then declines as the widening margin admits paradoxes. The relative target $$\rho\,Ppk_{pre}$$ avoids the cliff entirely.

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/eac/ppk_feasibility_cliff.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption"><strong>Figure 7.</strong> Method D under a fixed \(Ppk_{target}=1.33\). Left: \(\mathrm{EAC}_D/\sigma_{pre}\). Right: iECR, plotted only where the margin is positive; the gray region is infeasible.</div>

Finally, the **integration range** matters for absolute level but not for the winner:

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/eac/iecr_range_sensitivity.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption"><strong>Figure 8.</strong> iECR vs. the shift-range upper bound \(\delta_{max}/\sigma_{pre}\) at the baseline scenario.</div>

At baseline the order D > A > C > B holds for every $$\delta_{max}/\sigma_{pre}\in\{2,3,4,5,6\}$$. Across a 648-scenario grid subset, **A is highest at every limit** — but widening the range raises every level and draws the methods together, narrowing their spread from 0.113 to 0.042, with C and D coming within under 0.002 and crossing on the way:

| $$\delta_{max}/\sigma_{pre}$$ | A | B | C | D | Ranking |
| :--: | :--: | :--: | :--: | :--: | :-- |
| 2 | 0.706 | 0.593 | 0.675 | 0.604 | A > C > D > B |
| 3 | 0.787 | 0.704 | 0.732 | 0.718 | A > C > D > B |
| 4 | 0.837 | 0.775 | 0.784 | 0.786 | A > D > C > B |
| 5 | 0.869 | 0.819 | 0.826 | 0.828 | A > D > C > B |
| 6 | 0.891 | 0.849 | 0.854 | 0.857 | A > D > C > B |

Note that at $$\delta_{max}=4\sigma$$ this subset puts D above C (0.786 vs 0.784) while the full grid at the *same* limit puts C above D (0.822 vs 0.808). With the limit fixed, **the C–D order tracks which scenarios are averaged, not the shift range.** The paper adopts $$\delta_{max}=4\,\sigma_{pre}$$.

### 5.4 Tuning — the gaps are structural, the optima are broad plateaus

A natural question: once every method is tuned to its best setting, do they converge? **They don't.** A ≈9-point iECR gap persists between the best and worst, so the differences appear structural rather than artifacts of the defaults.

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/eac/parameter_tuning_optimization.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption"><strong>Figure 9.</strong> Fine-tuned iECR vs. each method's primary tuning parameter. Stars mark the iECR-maximizing value \(\theta^*\).</div>

| Method | Optimal setting $$\theta^*$$ | Peak iECR | Flat within 0.005 of peak over |
| :-- | :--: | :--: | :--: |
| C. Effect-Size | $$ES^*=1.00$$ | **0.930** | $$ES\in[0.93,\,1.07]$$ |
| A. $$\sigma$$-Scaled | $$\lambda^*=1.43$$ | 0.908 | $$\lambda\in[1.29,\,1.50]$$ |
| D. Ppk-Informed | $$\rho^*=0.83$$ | 0.842 | $$\rho\in[0.80,\,0.86]$$ |
| B. %-of-Mean | $$\lambda_\%^*=0.039$$ | 0.836 | $$\lambda_\%\in[0.030,\,0.044]$$ |

**Each optimum is a broad plateau, not a sharp point** — practically, the tuning parameter only needs to land in the right *neighborhood*. Note too that Method A's prespecified $$\lambda=1.5$$ sits inside its own optimal plateau $$[1.29,1.50]$$, which is part of why it does well at defaults.

> **The most interesting reversal.** At their respective optima, **Method C (0.930) overtakes Method A (0.908)** — even though C's optimal effect size ($$ES^*\approx1.00$$) sits *below* A's coefficient ($$\lambda^*\approx1.43$$). Because the two methods are identical apart from the $$\chi^2$$ variance correction, this is direct evidence that **the correction improves the calibrated margin.** Method C's poor showing at defaults is an artifact of naively matching $$ES$$ to A's $$\lambda=1.5$$, which over-widens the realized margin to $$2.06\sigma$$ and inflates paradoxes — not a flaw in the correction itself.

---

## 6. Discussion

### What drives decision quality? An ANOVA attribution

A Type-II ANOVA on the factorial iECR results (Type II because the $$4\le n_{post}\le30$$ constraint leaves the grid unbalanced) pinpoints the dominant effects, read against Cohen's benchmarks (0.01 small, 0.06 medium, 0.14 large):

| Effect | $$\eta^2$$ | Size | Interpretation |
| :-- | :--: | :--: | :-- |
| Sample size $$n_{pre}$$ | **0.290** | Large | the single biggest driver, by a wide margin |
| Method × $$\sigma_{post}/\sigma_{pre}$$ | 0.118 | Medium | methods diverge under heteroscedasticity |
| Method (main effect) | 0.066 | Medium | the margin formula genuinely matters |
| Method × $$r$$ | 0.056 | Small | the sample-size ratio acts only through method |
| Method × $$n_{pre}$$ | 0.043 | Small | the large-$$n$$ turnovers |
| Method × $$m/\sigma_{pre}$$ | 0.033 | Small | Method B's mean-level dependence |
| Method × $$S/\sigma_{pre}$$ | 0.026 | Small | Method D's spec-width dependence |
| *(Residual)* | 0.321 | — | |

Four terms fall below even the small-effect threshold and are omitted ($$\eta^2\le0.009$$): **$$\kappa$$, Method × $$\kappa$$, $$S/\sigma_{pre}$$, and $$r$$** as main effects. That the off-center fraction barely registers confirms the dimensionless parameterization is doing its job; the sample-size ratio matters *only* through its interaction with method. And because the grid is exhaustive with paired method–scenario rows, **$$p$$-values carry no sampling interpretation** — effect magnitudes are reported instead.

### A purpose-first decision framework

The revised paper reframes method selection around **scientific purpose rather than a numerical threshold**. That purpose is what has to be defensible; variance assumptions, sample size, and feasibility then refine it.

> **Step 1 — What is the scientific basis for the margin?**
> - **Capability preservation** → **Method D (Ppk-informed)**, with $$\rho\in[0.7,0.9]$$.
> - **Variability scaling** → **Method A ($$\sigma$$-scaled)**, with $$\lambda\in[1.0,1.5]$$.
> - **Effect-size reasoning** → **Method C**, with $$ES\approx1.0$$ and $$\alpha_{\chi^2}=0.05$$.
>
> **Step 2 — Then adjust for:**
> - **Unequal spread.** If $$\sigma_{post}/\sigma_{pre}\gtrsim1.5$$ is plausible, prefer **Method C** — the only method whose concordance *improves* under inflation.
> - **Small $$n_{pre}$$.** Method C's $$\chi^2$$ bound inflates its margin as $$n_{pre}$$ shrinks; check the realized $$\mathrm{EAC}/\sigma_{pre}$$.
> - **Capability feasibility.** A relative target ($$\rho<1$$) is always feasible; a *fixed* target requires $$d_{pre}/\sigma_{pre}>3\,Ppk_{target}$$. **If it fails, relax the target — don't switch method**, which merely sets the capability requirement aside rather than satisfying it.
> - **No dominant purpose.** Default to **Method A**: highest mean iECR on this grid, highest at every sample size and shift limit examined, and its prespecified $$\lambda=1.5$$ falls inside the iECR-optimal plateau. Reconsider if $$\sigma_{post}/\sigma_{pre}\gtrsim1.5$$ is likely.

**Method B is deliberately absent from the framework.** It is the simplest to compute, but its mean-scaled margin swings between paradox-prone (large $$m/\sigma$$) and over-tight (small $$m/\sigma$$). If you are considering it, check the margin it actually implies at your own process's $$\mu_{pre}/\sigma_{pre}$$ before adopting it.

### Two uses that should not be conflated

- **Planning** computes the curves *before* a confirmatory study, to justify a margin. The tuning sweep can also be run at a process's *own* pre-change parameters to set its tuning constant — it uses pre-change data only, as every EAC formula here does, so it adds no dependence on the comparability data. The selected value must still be **prespecified**.
- **Diagnostic benchmarking** scores an *incumbent* margin against an observed process. It is **exploratory only**, and never grounds for retrospectively changing a pre-specified margin.

The framework itself is agnostic to both the EAC method and the domain. Any candidate margin — Bayesian, data-dependent, or entirely novel — can be scored by its ECR, PR, and GZR curves, so the four methods here are a case study, not an exhaustive list. It applies to process comparability, method and site transfer, and scale-up, and extends further, from biosimilarity testing to economics.

### Relationship to existing work

- **Operating-characteristic analyses** rank margins by the equivalence test's false-acceptance and false-rejection rates against an *externally fixed* standard of which shifts are acceptable. ECR references **detectability** instead, and ranks the *construction methods*, not just candidate values. The two are **complementary**.
- **Three-sided testing / zone schemes** supply the same four-outcome logic; ECR turns it into a simulation-based operating characteristic of the joint procedure.
- **Conditional equivalence testing** reaches the same conclusions by testing equivalence only after a non-significant difference test — which **forecloses the paradox rather than measuring it**.
- **Second-generation $$p$$-values, data-dependent post-hoc margins, and Bayesian HDI–ROPE** replace the margin decision rather than scoring margins by the coherence of their verdicts.

### Limitations & future work

All methods assume normality, and Method D additionally requires specification limits. The margin is fixed and known, so the rates condition on the pre-change parameters — relaxed in §7 below, where the comparison holds. **iECR is a scalar, so it can mask crossing curves: report it *with* the curve, not instead of it.** Results depend on the grid, whose $$n_{pre}\in[4,30]$$ range reflects pharmaceutical practice and may not generalize. And at large $$n$$ the point-null D-test is overpowered, inflating the paradox rate.

That last point motivates the headline future direction: replacing the point-null D-test with a **minimum-effect gate**, declaring a difference only when the test is significant **and** the observed shift exceeds a fraction of the margin (e.g. $$0.75\,\Delta$$). This would suppress the spurious large-$$n$$ paradoxes while preserving the zone classification. Other directions: priors on shift magnitude (a Bayesian EAC), adaptive re-estimation of $$\sigma$$ from incoming data, non-normal ECR curves, and simultaneous testing across correlated attributes.

---

## 7. Two Checks Worth Highlighting

### Unconditional margins — does fixing the margin flatter Method C?

The main analysis fixes each margin at its population value. The paper reruns the **entire grid** with every margin re-estimated from each replicate's own simulated pre-change sample — same seeds, same datasets, only the margin rule differing.

| Method | mean iECR (conditional → unconditional) | min iECR |
| :-- | :--: | :--: |
| A. $$\sigma$$-Scaled | 0.872 → 0.874 | 0.397 → 0.395 |
| C. Effect-Size | **0.822 → 0.831** | **0.337 → 0.488** |
| D. Ppk-Informed | 0.808 → 0.807 | 0.381 → 0.381 |
| B. %-of-Mean | 0.800 → 0.800 | 0.381 → 0.381 |

**The ranking is unchanged.** Only Method C moves materially — exactly as predicted, since the conditional design leaves its $$\chi^2$$ hedge against an underestimated $$\sigma_{pre}$$ unexercised. The gain is concentrated at small samples ($$+0.048$$ at $$n_{pre}=4$$, $$+0.003$$ at $$n_{pre}=30$$). A, B, and D shift by less than 0.002.

### A worked example on real data

The appendix applies the diagnostic the way a practitioner would: three attributes of a real bulk-versus-packaged comparability dataset, each profiling the **ECR-recommended margin against a fixed $$3\,s_{pre}$$ user-defined margin**.

```plotly
{
  "data": [
    {"x": ["Assay", "Impurities", "Water"],
     "y": [0.961, 0.971, 0.934],
     "name": "ECR-recommended margin",
     "type": "bar",
     "marker": {"color": "#2196F3"},
     "text": ["0.961<br>(Effect-Size)", "0.971<br>(Ppk-Informed)", "0.934<br>(σ-Scaled)"],
     "textposition": "outside"},
    {"x": ["Assay", "Impurities", "Water"],
     "y": [0.557, 0.977, 0.663],
     "name": "User-defined 3·s_pre",
     "type": "bar",
     "marker": {"color": "#FF9800"},
     "text": ["0.557", "0.977", "0.663"],
     "textposition": "outside"}
  ],
  "layout": {
    "title": "iECR: recommended vs. incumbent margin on real comparability data",
    "yaxis": {"title": "iECR", "range": [0, 1.15]},
    "barmode": "group",
    "legend": {"orientation": "h", "y": -0.15},
    "margin": {"t": 40, "b": 60}
  }
}
```

For **assay** and **water** the recommended margin is decisively better (0.961 vs 0.557 and 0.934 vs 0.663) — the $$3\,s_{pre}$$ rule is simply far too wide, driving max PR to 0.990 and 0.811 respectively. For **impurities** the two are essentially tied (0.971 vs 0.977), and the choice then rests on **which error matters more**: the Ppk-informed margin gives the lower gray-zone rate (max GZR = 0.007), the user-defined margin the lower paradox rate (max PR = 0.023).

**Surfacing that trade-off — rather than declaring a winner — is the point of the diagnostic.**

---

## 8. Conclusion

The Equivalence Concordance Rate framework is a **decision-quality lens** for equivalence-margin specification — not a new test, and not a new margin.

- It cleanly separates **wide-margin failure** (paradox, the consumer's-risk direction) from **narrow-margin failure** (gray zone, the producer's-risk direction).
- It collapses a margin's full shift-response into a single, rankable score (**iECR**).
- It surfaces sample-size and robustness insight that one-off equivalence tests cannot.
- It needs only **pre-change data**, so a single comparability dataset suffices to benchmark an incumbent margin.

Applied as a case study to four common margins across 10,368 dimensionless scenarios — **not to crown a single best margin** — it finds that the methods separate **structurally rather than by tuning**, with **sample size the dominant driver**. Method A ($$\sigma$$-scaled) is the most robust general-purpose choice on this grid; Method D (Ppk-informed) has the lowest paradox rate but the widest gray zone and the largest sample-size appetite; Method C's $$\chi^2$$ correction genuinely *helps* once calibrated (highest tuned peak, 0.930) despite its poor default showing; and Method B is structurally handicapped by its dependence on the mean level. Below the top spot, though, the ordering is close enough that it should not be over-read.

The takeaway for practitioners: rather than defending a margin by tradition, you can **justify it with quantitative evidence** — run a targeted ECR study and compare the iECR of your candidate margin against the alternatives, for your own process and your own sample sizes.

---

## Appendix Summary

- **A. Proofs** — the Ppk-informed margin for centered and off-center processes.
- **B. ANOVA** — effect-size attribution of the factorial drivers of iECR.
- **C. Overpowered difference test** — the large-$$n$$ paradox mechanism.
- **D. iECR shift-range sensitivity** — ranking stability across $$\delta_{max}$$.
- **E. Welch–Satterthwaite check** — Method C's variance robustness is not a pooling artifact.
- **F. Unconditional margins** — the full grid rerun with sample-estimated margins.
- **G. Method D feasibility cliff** — behaviour under a fixed capability target.
- **H. Application to real data** — the worked bulk-versus-packaged example.

---

## Download

- Full paper PDF: [Equivalence Concordance Rate (ECR) Framework]({{ '/assets/pdf/ecr_eac_framework_paper.pdf' | relative_url }})

## Source Notes

- Foundational equivalence-testing context follows the TOST literature and pharmaceutical comparability guidance (ICH Q5E, ICH M13A) cited in the paper bibliography.
- Analytical margins and decision probabilities use the exact bivariate non-central $$t$$ formulation; everything else is Monte Carlo.
- The comparability measurements in the worked example are de-identified proprietary manufacturing release data; only summary statistics are reported.
