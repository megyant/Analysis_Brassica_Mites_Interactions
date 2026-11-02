# Fertiliser and herbivorous mites: effects on *Brassica* growth

Experiment design and analysis by Margarida Antunes (University of Lisbon, 2023).

**Report:** [`brassica_analysis.html`](brassica_analysis.html) (download and open in a browser)

## Question

How do fertiliser and spider mites from different host plants (bean or
tomato) affect the growth and reproductive potential of *Brassica*?

## Experiment

```
                 no mites   bean mites   tomato mites
control            60          60            60
fertiliser         60          60            60      → 360 plants, 90 pots, 5 blocks

measured at weeks 4, 6 and 7:  height · leaves · pistils · mite count
```

## Analysis

```
one row per plant ──reshape──► one row per plant per week
                                     │
          linear mixed-effects model per trait (lme4)
          trait ~ initial value + fertiliser × mite origin + (1 | week / ecosystem)
                                     │
          Type III F-tests (car)  →  estimated marginal means (emmeans)
```

## Key results

| Trait | Effect | P |
|---|---|---|
| Height | fertiliser: +20 mm | 0.015 |
| Leaves | fertiliser: +1.2 leaves; effect depends on mite origin, largest without mites | 0.0008; interaction 0.009 |
| Pistils | fertiliser: +2.7 pistils | 0.004 |
| Mite count | fewer tomato than bean mites (borderline) | 0.052 |

Mite origin on its own did not significantly change plant height, leaves or pistils.

## Repository structure

```
├── brassica_analysis.Rmd     full analysis (R Markdown)
├── brassica_analysis.html    knitted report
└── data/
    ├── data2.csv             analysis data: one row per plant, 3 time points (; separated)
    ├── Data.xlsx             original data entry sheets
    └── initialdata.csv       week-4 measurements only (data entry)
```

## How to run

```r
install.packages(c("tidyverse", "lme4", "car", "emmeans", "rmarkdown"))
rmarkdown::render("brassica_analysis.Rmd")
```
