# Gilt Liquidity Stress Test

How much of a rise in gilt yields can a hypothetical UK pension fund absorb before it runs short of cash to meet collateral calls?

This notebook simulates 100,000 paths for a long-dated gilt yield over 10 business days. It translates yield changes into collateral requirements using an assumed hedge sensitivity and measures the largest cash shortfall on each path.

## Results

- Under the illustrative baseline, 3.29% of paths exceeded the £1m cash buffer at some point, compared with 2.45% when measured only on day 10.
- The September 2022 gilt shock produced a peak shortfall of £1.8m when replayed through the hypothetical fund.
- Sensitivity analysis shows how the breach rate changes with the size of the cash buffer and the assumed volatility of daily yield changes.

The historical replay uses the gilt-market timeline in Chen and Kemp (2023), [*Putting Out the NBFIRE*](https://www.imf.org/en/publications/wp/issues/2023/09/29/putting-out-the-nbfire-lessons-from-the-uk-s-liability-driven-investment-ldi-crisis-539683). The fund parameters and baseline volatility are illustrative, so the simulated breach rates are conditional on those assumptions.

The simulation workflow builds on my first-year epidemiology project, where I used repeated simulations to estimate the probability of crossing an outbreak threshold.

## Run the notebook

Install `jupyter`, `numpy`, `pandas`, `matplotlib` and `scipy`. Open `gilt_liquidity_stress_test.ipynb` and run the cells in order.
