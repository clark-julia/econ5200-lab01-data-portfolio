# econ5200-lab01-data-portfolio
# Data Quality Profiling — Big Mac Index

## Objective
Audit The Economist's Big Mac Index panel for structural and measurement problems, and quantify how dropping incomplete panels biases the resulting price statistics.

## Methodology
- **Corrected a PPP valuation error.** The original formula had the numerator and denominator swapped, which reversed the ranking and labelled undervalued currencies as overvalued. After the fix, the July 2024 cross-section ranks Switzerland (+41.8%), Uruguay (+24.3%), Norway (+18.9%), Argentina (+15.0%) and the Euro area (+6.5%) as most overvalued against the US dollar.
- **Diagnosed survivorship bias.** Dropping every country with any missing period retained only 25 of 57 countries. The excluded set mixes countries that left the index, joined late, or have gaps mid-run, so it is not a random subset.
- **Quantified the bias.** Compared the average dollar price per date for the 25 complete-panel countries against the average across all countries available in each period.
- **Built `profile_dataframe()`.** A reusable function that reports the number of units and periods, panel structure, count of complete units, whether the panel is balanced, and the percentage of missing values in each column.

## Key Findings
- The complete-panel average overstates the all-available average by **$0.081 (+2.1%)** on average, and is higher in **33 of 45** periods.
- The dataset is an **unbalanced panel** of **57 units and 45 periods**, with 2,056 rows against a full grid of 2,565. Only **25** countries appear in every period, and **7** columns are more than 10% missing.
- In July 2024, the median currency is **20.7% undervalued** against the US, and only 6 of 54 countries have a Big Mac dearer than the US. This reflects the US being a high-price-level benchmark, so the index mixes currency misalignment with income-driven price differences.
- Complete-case deletion cannot support claims about "all countries." Recommended practice is to use all available observations per period, report the number of countries behind each average, and use within-country changes for trend analysis.
