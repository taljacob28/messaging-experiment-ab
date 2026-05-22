# A/B Testing: Which Message Drives the Most Action?

An A/B testing analysis of a large-scale randomized experiment. Four message
variants are compared against a holdout control to measure which one lifts a target
action the most, whether the lift is real, and which users respond best.

The data is a real field experiment (Gerber, Green & Larimer, 2008) on 305,866
people, analyzed with the exact methods used in product and marketing A/B testing:
treatment effect estimation, confidence intervals, multi-arm comparison, and
heterogeneous effects.

![Experiment design](images/experiment_design.png)

## The data and variables

Each person was randomly assigned to a control group or one of three messages of
increasing social pressure, then their action was recorded.

- `messages` the variant sent. `Control` received no message.
- `primary2006` the outcome. Did the user take the action (conversion).
- `primary2004` prior behavior. Did the user act in the comparable past event.
- `age`, `sex`, `hhsize` user attributes used for segmentation.

The data comes from an administrative registration file, so covariates are limited
to these fields. Income and similar variables were never collected.

## Headline result

The strongest message (Neighbors) lifts the action rate by 8.1 percentage points
over control, 95% CI [7.6, 8.7], a 27% relative gain. All variants are significant,
but effect size separates them.

![Action rate by message variant](images/action_rate_by_variant.png)

## Who responds most

The lift is largest among already-active users and peaks in the 31 to 75 age range.

![Lift by subgroup](images/lift_forest_plot.png)

Crossing age with prior behavior pinpoints the strongest cells: active users aged
31 to 45 and 61 to 75.

![Lift by age and prior behavior](images/lift_heatmap_age_prior.png)

The two milder messages are flat for the youngest and oldest users. At the age
extremes, only the strong message works.

![Lift by treatment across age](images/lift_by_treatment_age.png)

## Where is the opportunity

Plotting lift (efficiency) against segment size (reach) shows the trade-off. Active
users aged 31 to 45 are the most efficient large segment. The 46 to 60 group is the
largest total opportunity.

![Targeting opportunity](images/targeting_opportunity_map.png)

## Recommendation

Ship the Neighbors message. Prioritize active users aged 31 to 45 for efficiency,
or the 46 to 60 group for total volume. Avoid young dormant users, where both the
lift and the milder messages fall flat.

## Methods

Two-proportion z-test computed manually, with confidence intervals. Multi-arm
comparison with a Bonferroni correction. Heterogeneous effects across prior
behavior, age, and their combination. Business impact projection.

## Tech stack

Python, pandas, NumPy, SciPy, matplotlib, seaborn.

## How to run

```
pip install -r requirements.txt
jupyter notebook ab_analysis.ipynb
```

## Reference

Gerber, A. S., Green, D. P., & Larimer, C. W. (2008). Social pressure and voter
turnout: Evidence from a large-scale field experiment. American Political Science
Review, 102(1), 33 to 48.
