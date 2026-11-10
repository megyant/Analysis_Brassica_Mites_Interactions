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
                                     │
          overall effects averaged over the other factor (emmeans contrasts)
```

## Key results

| Trait | Effect (fertilised vs control, averaged over mite groups unless stated) | P |
|---|---|---|
| Height | fertiliser: +17 mm | 0.0008 |
| Leaves | fertiliser effect depends on mite origin: +2.2 leaves without mites, +1.2 with bean mites, +0.8 with tomato mites | interaction 0.009 |
| Pistils | fertiliser: +2.2 pistils | 0.0001 |
| Mite count | about 2 fewer tomato than bean mites (averaged over fertiliser) | 0.004 |

Mite origin on its own did not significantly change plant height, leaves or pistils.

**Note.** An earlier version of this README reported +20 mm (height), +1.2 leaves and
+2.7 pistils. Those were the Type III main-effect estimates, which with R's default
treatment contrasts only describe plants with bean mites. The table above reports the
average effects from estimated marginal means; see the report for each group.

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
