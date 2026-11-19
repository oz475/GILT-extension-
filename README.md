# Gilt liquidity stress test

**Question:** how large a rise in gilt yields can a hypothetical pension fund absorb before it runs short of cash to meet collateral calls?

A pension fund that hedges its interest-rate risk loses money on the hedge when gilt yields rise, and has to post cash collateral straight away. This notebook simulates 100,000 paths of a long-dated gilt yield over a 10-business-day horizon. It runs each path through a simple collateral model of one hypothetical fund and counts how often the collateral needed exceeds the fund's cash buffer.

This project adapts the threshold-based Monte Carlo approach I used in a first-year epidemiology project to examine liquidity risk from collateral calls under gilt yield shocks.

## Main chart

![Breach rate vs cash buffer](figures/breach_rate_vs_buffer.png)

## Main results (hypothetical fund: £1m cash buffer, hedge loses £20,000 per bp)

| Assumption | Horizon | Share of paths breaching the £1m buffer |
|---|---|---|
| Daily yield volatility 8 bp (baseline) | 10 business days | 3.3% |
| Daily yield volatility 15 bp (high) | 10 business days | 22.1% |

* The buffer absorbs a 50 bp rise. A 60 bp rise leaves a £200,000 shortfall.
* Buffer size and hedge size matter only through their ratio, the headroom in basis points. Doubling the hedge has the same effect as halving the buffer.
* Replaying 21–28 September 2022 through the same fund gives a £1.8m shortfall within 4 business days. The baseline normal model essentially never generates a move that large, which shows how much the result depends on the shock distribution.

All fund parameters and volatilities are hypothetical. The model uses independent normal daily yield changes, a single yield, a constant hedge sensitivity and a fixed cash buffer. It has no feedback from forced selling and does not model liabilities. Section 6 of the notebook discusses these limits.

## How to run

```bash
pip install numpy pandas matplotlib scipy jupyter
jupyter notebook gilt_liquidity_stress_test.ipynb
```

Run all cells; the notebook takes a few seconds to run. The random seed is fixed, so results are reproducible, and the main chart is saved to `figures/breach_rate_vs_buffer.png`.

## Data

The historical replay uses the cumulative change in long-term gilt yields since 21 September 2022, as reported in the crisis timeline of Chen, R. & Kemp, E. (2023), *Putting Out the NBFire: Lessons from the UK's Liability-Driven Investment (LDI) Crisis*, IMF Working Paper 23/210.
