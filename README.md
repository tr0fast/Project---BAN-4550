# Do earnings surprises move stock prices differently for brokers and medical instrument makers?

**Author:** Ludwig Trofast · BAN 4550, Fall 2026 · Industry: SIC 62, Security \& Commodity Brokers (client: Goldman Sachs) · Comparison industry: SIC 38, Instruments (Medical)

## The question

Goldman Sachs (SIC 62) wants to know wether the stock market reacts to earnings surprises in the same way in its own industry as in a different one, medical instruments (SIC 38). I measure the reaction as the return above the market over three days around the announcement (CAR).

## Main result

The High SUE groups do not differ clearly between the industries: brokers beat the market by 2.55 pp and medical by 1.72 pp, and the intervals overlap. The Low SUE groups differ more. Medical stocks underpeform the market by 2.01 pp on average, brokers by only 0.27 pp, and these intervals do not overlap. The High minus Low gap is larger in medical (3.72 pp against 2.82 pp), but I can´t show that this difference of 0.90 pp is real. I calculated these comparisons by hand from the confidenc intervals in Figure 1.

## Is the difference real?

A t-test of High vs Low gives a difference of 2.82 pp for brokers (t = 4.49, p < 0.0001) and 3.72 pp for medical (t = 6.03, p < 0.0001). In the regresion CAR = a + b x SUE, b is 0.125 for brokers (p < 0.0001) and 0.090 for medical (p = 0.0897). A 1 pp higher SUE goes with a 0.125 pp higher CAR in brokers. R-squared is 2.3% and 0.2%, so SUE explains little of the variation. With year fixed effects b barely changes (0.119 and 0.089). The medical slope is significant at the 10% level but not at 5%, and it is not significant in the model with the loss interaction, so I do not build a claim on it.

## Why the industries differ

I checked whether loss-making quarters explain the difference. 9.6% of broker announcements and 27.8% of medical announcements have negative EPS. If losses made SUE less informative in medical, the slopes shoud become more alike without them. They did not: the gap in slope grew from 0.035 to 0.119. The reason is not supported. The confidence intervals overlap in both samples.

## Advice for the client

* **Business implication:** The stocks with the highest earnings surprises beat the market by circa 2.6 pp in brokers and 1.7 pp in medical instruments, and the lowest group lags behind it, mostly in medical instruments. The client can use SUE as one signal around earnings announcements. But single announcements differ a lot (R-squared is 2.3% and 0.2%), so SUE should be combined with other information and not used alone."
**Limitation:** SUE compares earnings with the same quarter last year, not with analyst expectations, so a quarter can look like a surprise when the market expected it. The result also shows correlation, not cause.
* **Next questions:** Predictive: can SUE together with analyst forecast errors predict CAR over the next 30 days? This needs analyst forecast data (I/B/E/S). Prescriptive: which holding period after the announcement gives a broker's clients the best return? This needs daily returns for a longer window.

## Data

* Sources: Compustat (`comp.fundq`), CRSP (`crsp.dsf`, `crsp.dsi`), accessed through WRDS, plus the instructor's link file (`ccm\_link.csv`).
* **The data are not included in this repository** because of the WRDS license. Someone with WRDS access can rebuild the results by running the notebook with the link file in the same folder.
* Sample period and rules: Announcements between 1 Jan 2021 and 31 Dec 2024. I remove quarters with no announcement date, no SUE, a last-quarter price below $5, |SUE| above 1, or fewer than three daily returns. This leaves 933 announcements for brokers and 1,768 for medical instruments.

## How the tables fit together

Compustat quarters are linked to CRSP with gvkey and the link file, keeping the link that was valid on the quarter-end date. Last year's EPS and last quarter's price are added with gvkey and quarter number. Stock returns, market returns and the three-day window are matched on permno and trading-day number.

## How I checked the results

I expected the table to keep the same number of rows after Merge 2. For SIC 38 it grew from 3654 to 3664 because four rows had the same gvkey and quarter number. I kept one row for each, and I added a check that stops the code if the row count changes.

## Changes since Project 2

|What was wrong|How I fixed it|How the results changed|
|-|-|-|
|In Merge 2, a repeated gvkey + quarter number added rows in Merge 2 (found for SIC 38)|I keep one row per gvkey + qnum and stop if the row count changes|SIC 62: no change (0 duplicates). SIC 38: 3,664 rows before, 3,654 after.|

## Where the code came from

The code come from the class notebooks (Assignment 8, in-class 10 and 11) and my Project 2 notebook. Was changed to fit my company using Claude (Anthropic)

|AI tool|Link (or PDF in docs/)|What I used it for|
|-|-|-|
|Claude|https://claude.ai/share/a509f52d-e510-4005-841c-52f8f4228146|Coding, help with understanding \& presentation slides.|

## Files

```
notebooks/   Trofast\_Ludwig\_Project3.ipynb (runs top to bottom on WRDS JupyterHub)
figures/     figure1.png, figure2.png, figure3.png, merge\_map.png
README.md
```

